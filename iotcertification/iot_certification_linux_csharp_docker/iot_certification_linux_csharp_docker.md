<a name="how-to-certify-arm-32-iot-devices-running-net-core-within-a-linux-docker-container-linux-is-also-the-host-os"></a>如何认证在 Linux Docker 容器中运行 .NET Core 的 ARM 32 IoT 设备（Linux 也是主机 OS）。
===
---

# <a name="table-of-contents"></a>目录

-   [简介](#Introduction)
-   [步骤 1：配置 Azure IoT 中心](#Step-1-Configure)
-   [步骤 2：注册设备](#Step-2-Register)
-   [步骤 3：使用 C 客户端库生成并验证示例](#Step-3-Build)
    -   [3.1：在设备上加载 Azure IoT 代码和必备组件](#Step-3-1-Load)
    -   [3.2 生成示例](#Step-3-2-Build)
    -   [3.3：运行并验证示例](#Step-3-3-Run)
-   [步骤 4：打包并共享](#Step-4-Package_Share)
    -   [4.1：打包生成日志和示例测试结果](#Step-4-1-Package)
    -   [4.2 与工程支持人员共享包](#Step-4-2-Share)
    -   [4.3：后续步骤](#Step-4-3-Next)
-   [步骤 5：故障排除](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a>简介

**关于本文档**

本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。 此过程由多个步骤组成，其中包括：

-   配置 Azure IoT 中心
-   注册 IoT 设备
-   在设备上生成并部署 Azure IoT SDK
-   打包并共享日志

**准备**

在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。

在开始过程前，应已准备好以下项目：

-   准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) GitHub 公共存储库的计算机。
-   安装 Visual Studio 2015 和工具。 可以安装任何版本的 Visual Studio，包括免费的社区版。
-   用于访问设备命令行的 SSH 客户端，例如 PuTTY。
-   在开发计算机和设备上安装 Docker： https://www.docker.com/get-started

***注意：****如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://catalog.azureiotsuite.com/>)请求此身份，然后遵照本文中的说明操作。*

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a>步骤 1：注册 Azure IoT 中心

遵照[此处](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub)所述的说明[注册](https://account.windowsazure.com/signup?offer=ms-azr-0044p) Azure IoT 中心服务。 若要了解如何查找 IoT 中心的连接字符串，请参阅[此文档](https://devblogs.microsoft.com/iotdev/understand-different-connection-strings-in-azure-iot-hub/)。

-   **IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a>步骤 2：注册设备

在本部分，我们将使用 DeviceExplorer 注册设备。 DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：

-   设备管理
    -   创建新设备
    -   列出现有设备，公开设备中心内存储的设备属性
    -   可更新设备密钥
    -   可删除设备
-   监视设备的事件
-   向设备发送消息

若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step-1-Configure) 中所述使用以下配置字符串：

-   IoT 中心连接字符串

**步骤：**
1.  单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。

2.  添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。 

3.  根据以下说明创建设备并将其注册到 IoT 中心。

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。 单击“管理”选项卡。 

    b.保留“数据库类型”设置，即设置为“共享”。 注册的设备将显示在列表中。 如果你的设备未显示在列表中，请单击“刷新”按钮。  如果这是第一次注册设备，请不要检索任何信息。

    c. 单击“创建”按钮创建设备 ID 和密钥。 

    d.单击“下一步”。 成功创建设备后，该设备将列在 DeviceExplorer 中。

    e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。 右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。 

    f. 在记事本中保存此信息。 后面的步骤需要用到此信息。

***不是在电脑上运行 Windows？*** - 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。

<a name="Step-3-Build"></a>
# <a name="step-3-build-a-linux-docker-image-that-includes-the-net-core-runtime-and-the-sample-used-for-validating-your-device"></a>步骤 3：生成一个 Linux Docker 映像，其中包含 .NET Core 运行时和示例，用于验证设备。

本部分逐步讲解如何生成并运行 Linux Docker 映像，以便在 ARM 32 设备上验证 IoT 客户端 SDK。  除非另有说明，否则 Docker 映像会包含运行示例测试所需的所有必备组件。这些测试是在设备上进行 IoT 认证所需的。

<a name="Step_3_1:_Development"></a>
## <a name="31-prepare-your-development-environment"></a>3.1：准备开发环境

- 从 https://dot.net 安装最新的 .NET Core
- 安装 .NET Framework 4.7 开发人员包： https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs
- 安装 .NET Framework 4.5.1 开发人员包： https://www.microsoft.com/en-us/download/details.aspx?id=40772

<a name="Step_3_2:_Build"></a>
## <a name="32-build-and-push-the-docker-image-to-your-registry"></a>3.2：生成 Docker 映像并将其推送到注册表

使用[此 Dockerfile](./Dockerfile) 生成一个基于 [.NET Core Arm32 Linux 映像](https://hub.docker.com/_/microsoft-dotnet-core-samples/)的 Docker 映像：

-   在开发环境中打开包含 [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) 的目录，具体说来就是打开以下目录：

        iot-hub\Samples\device\MessageSample

-   复制[此 Dockerfile](./Dockerfile) 并将其粘贴到如上所示的 MessageSample 目录。
-   在 Dockerfile 中以环境变量的形式添加 IoT 中心设备连接字符串。  具体说来，请打开 Dockerfile 并将“<your_device_connection_string>”替换为你的设备连接字符串，然后保存所做的更改。
-   使用 Docker 和 Dockerfile，生成一个将 .NET Core 消息示例应用容器化的 Docker 映像。  接下来，将此映像推送到 Docker 注册表。  例如：

        cd iot-hub\Samples\device\MessageSample
        docker build -t <your_docker_account>/<your_docker_repo>:<your_img_tag> .
        docker push <your_docker_account>/<your_docker_repo>:<your_img_tag>

此示例包含两类测试 - 一类用于向 IoT 中心发送消息，另一类用于从 IoT 中心接收消息。 两类测试都支持不同的协议。 在生成 Docker 映像之前，可以修改测试，以便使用所选协议。 默认情况下，将会使用 AMQP 协议生成测试。

若要运行不同的协议，请执行以下操作：

-   在开发环境中，使用记事本打开以下文件：

        iot-hub\Samples\device\MessageSample\Program.cs

-   向下滚动到包含协议信息的代码节。

-   找到以下代码：

        private static TransportType s_transportType = TransportType.Amqp;

    使用的默认协议为 AMQP。 脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。 根据要使用的协议对该行进行注释/取消注释操作，然后保存所做的更改。

-   使用在步骤 3.2 开头介绍的步骤重新生成 Docker 映像。

<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-sample"></a>3.3：运行并验证示例

在本部分，我们将运行此示例来验证设备与 Azure IoT 中心之间的通信。 我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。 此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。

***注意：****请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2:_Share) 中需要使用这些屏幕截图。

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1 向 IoT 中心发送设备事件

1.  如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。  从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。 

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  DeviceExplorer 现在正在监视从所选设备发送到 IoT 中心的数据。

3.  打开 PuTTY 会话并连接到设备，然后通过拉取并运行 Docker 映像来运行示例。  例如：
        
        docker run --rm <your_docker_account>/<your_docker_repo>:<your_img_tag>
    
4. 成功执行后，应会看到设备控制台中收到的事件。

    **如果使用 HTTP 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_http.png)

    **如果使用 MQTT 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_mqtt.png)

    **如果使用 AMQP 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_amqp.png)

5. DeviceExplorer 的数据选项卡中应会显示收到的事件。

    **如果使用 HTTP 协议：**   

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_http.png)

    **如果使用 MQTT 协议：**

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_mqtt.png)

    **如果使用 AMQP 协议：**
    
     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_amqp.png)

### <a name="332-receive-messages-from-iot-hub"></a>3.3.2 从 IoT 中心接收消息

1.  若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。   注意，需在设备上再次运行此示例应用，所使用的命令与上一步的相同，例如：docker run --rm <your_docker_account>/<your_docker_repo>:<your_img_tag>

2.  使用“设备 ID”下拉列表选择创建的设备。

3.  在“消息”字段中添加一些文本，然后单击“发送”。

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

4. 设备控制台窗口中应会显示收到的消息。
    
    **如果使用 HTTP 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

    **如果使用 MQTT 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_mqtt.png)

    **如果使用 AMQP 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_amqp.png)
    
### <a name="333-verify-device-configuration"></a>3.3.3 验证设备配置

-   请通过执行以下命令安装 python。

    **Debian 或 Ubuntu**

        sudo apt-get install python

    **Fedora**

        sudo dnf install python

-    *此库还需要 Python 版本 2.7.x。* 可使用以下命令来验证环境中当前安装的版本：
    
          python --version

-   在运行 `platform_data.py` 之前，请安装以下模块

    **Debian 或 Ubuntu** 

        sudo apt-get install python-requests
        sudo apt-get install python-netifaces

    **Fedora**

        sudo dnf install python-requests
        sudo dnf install python-netifaces

-   发出以下命令下载 SDK：

        git clone https://github.com/Azure/azure-iot-sdk-python.git

-   通过执行以下命令导航到 tools 文件夹：

        cd azure-iot-sdk-python/Tools

-   在设备上运行以下命令
        
        python platform_data.py

    ![deviceinfo\_screenshot](images/python_modified_output.PNG)

-   请保存设备配置屏幕截图，然后按[步骤 4](#Step-4-1-Package) 所述上传该屏幕截图。

<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a>步骤 4：打包并共享

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a>4.1：打包生成日志和示例测试结果

打包设备中的以下项目：

1.  在生成运行期间记录在日志文件中的生成日志。

2.  前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。 

3.  前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。 

4.  前面“设备配置”  部分中的所有屏幕截图。

5.  请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。 请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>)提供的模板创建特定于设备的说明。
    
    有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a>4.2 与 Microsoft Azure IoT 团队共享包

1.  转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)
2.  单击设备右上角的“上载”图标。

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  此时将打开上载对话框。 单击“上载”按钮浏览文件。 

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    可以上载同一个设备的多个文件。

4.  上传所有文件后，单击“提交审查”按钮。 

    ***注意：****提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a>4.3：后续步骤

与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：疑难解答

如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。
