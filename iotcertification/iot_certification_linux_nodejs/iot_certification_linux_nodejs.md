<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a>如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备
===
---


# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：配置 Azure IoT 中心](#Configure)
-   [步骤 2：注册设备](#Register)
-   [步骤 3：使用 Node JS 客户端库生成并验证示例](#Build)
    -   [3.1 在设备上加载 Azure IoT 代码和必备组件](#Load)
    -   [3.2：生成示例](#BuildSamples)
    -   [3.3：运行并验证示例](#Run)
-   [步骤 4：打包和共享](#PackageShare)
    -   [4.1：打包生成日志和示例测试结果](#Package)
    -   [4.2：与工程支持人员共享包](#Share)
    -   [4.3：后续步骤](#Next)
-   [步骤 5：故障排除](#Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。 此过程由多个步骤构成，具体包括：

-   配置 Azure IoT 中心
-   注册 IoT 设备
-   在设备上生成和部署 Azure IoT SDK
-   打包并共享日志


**准备**

在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。 在开始过程前，应已准备好以下项目：

-   准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-node](https://github.com/Azure/azure-iot-sdk-node) GitHub 专用存储库的计算机
-   配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行
-   用于认证的所需硬件

***注意：****如果你尚未咨询 Microsoft 如何成为 Azure 认证的 IoT 合作伙伴，请先提交此[表单](<https://iotcert.cloudapp.net/>)来提出请求，然后遵照本文中的说明。*

<a name="Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a>步骤 1：注册 Azure IoT 中心

遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。

在注册过程中，将会收到连接字符串。

-   **IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：

          HostName=[YourIoTHubName];CredentialType=SharedAccessSignature;CredentialScope=[ContosoIotHub];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Register"></a>
# <a name="step-2-register-device"></a>步骤 2：注册设备

在本部分，我们将使用 DeviceExplorer 注册设备。 DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：

-   设备管理
    -   创建新设备
    -   列出现有设备并公开设备中心存储的设备属性
    -   提供更新设备密钥的功能
    -   可删除设备
-   监视设备的事件。
-   向设备发送消息。

若要运行 DeviceExplorer 工具，请根据[步骤 1](#Configure) 中所述使用配置字符串：

-   IoT 中心连接字符串

**步骤：**
1.   单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。

2.  在“配置”选项卡下添加连接信息，并单击“更新”按钮。

3.  根据以下说明创建设备并将其注册到 IoT 中心。

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。 单击“管理”选项卡。

    b.保留“数据库类型”设置，即设置为“共享”。 注册的设备将显示在列表中。 如果该设备未显示在列表中，请单击“刷新”按钮。 如果这是第一次注册设备，请不要检索任何信息。

    c. 单击“创建”按钮创建设备 ID 和密钥。

    d.单击“下一步”。 成功创建设备后，该设备将列在 DeviceExplorer 中。

    e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。 右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。

    f. 在记事本中保存此信息。 后面的步骤需要用到此信息。

***不是在电脑上运行 Windows？*** - 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。

<a name="Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-node-js-client-libraries"></a>步骤 3：使用 Node JS 客户端库生成并验证示例

本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。 我们将在设备上安装必备组件。  完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a>3.1 在设备上加载 Azure IoT 代码和必备组件

-   打开 PuTTY 会话并连接到设备。

-   在后续步骤中根据设备上运行的 OS 选择命令。

-   运行以下命令检查是否已安装 NodeJS

        node --version

    如果版本为 **0.12.x 或更高**，可跳过有关安装必备组件包的后续步骤。 否则，请在设备上的命令行中发出以下命令来卸载该版本。

    **Debian 或 Ubuntu**

        sudo apt-get remove nodejs

    **Fedora**

        sudo dnf remove nodejs

    **其他任何 Linux OS**

        Use equivalent commands on the target OS

-   在设备上的命令行中发出以下命令，安装必备组件包。 根据设备上运行的 OS 选择命令。

    **Debian 或 Ubuntu**

        curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -

        sudo apt-get install -y nodejs

    **Fedora**

        wget http://nodejs.org/dist/v4.2.1/node-v4.2.1-linux-x64.tar.gz

        tar xvf node-v4.2.1-linux-x64.tar.gz

        sudo mv node-v4.2.1-linux-x64 /opt

        echo "export PATH=\$PATH:/opt/node-v4.2.1-linux-x64/bin" >> ~/.bashrc

        source ~/.bashrc

    **其他任何 Linux OS**

        Use equivalent commands on the target OS

    **注意：** 若要测试 Node JS 是否成功安装，请尝试运行以下命令获取其版本信息：

        node --version

-   在 PuTTY 中发出以下命令，将 SDK 下载到开发板：

        git clone --recursive https://github.com/Azure/azure-iot-sdk-node.git

-   验证 ~/azure-iot-sdk-node 目录中现在是否有源代码的副本。

<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a>3.2 生成示例

-   若要验证源代码，请在设备上运行以下命令。

        export IOTHUB_CONNECTION_STRING='<iothub_connection_string>'

    将 `<iothub_connection_string>` 占位符替换为在[步骤 1](#Configure) 中获取的 IoT 中心连接字符串。    

-   运行以下命令 

        cd ~/azure-iot-sdk-node
        build/dev-setup.sh
        build/build.sh | tee LogFile.txt

    ***注意：****应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*

-   安装 npm 包以运行示例。

        cd ~/azure-iot-sdk-node/device/samples

    **对于 AMQP 协议：**
    
        npm install azure-iot-device-amqp
    
    **对于 HTTP 协议：**
    
        npm install azure-iot-device-http
    
    **对于 MQTT 协议：**

        npm install azure-iot-device-mqtt   

    **对于将 Web Socket 与 AMQP 协议配合使用：**

        npm install azure-iot-device-amqp

    **对于将 Web Socket 与 MQTT 协议配合使用：**

        npm install azure-iot-device-mqtt

-   若要更新示例，请在设备上运行以下命令。

        cd ~/azure-iot-sdk-node/device/samples
        nano simple_sample_device.js

-   此时会启动基于控制台的文本编辑器。 向下滚动到协议信息。
    
-   找到以下代码：

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    使用的默认协议为 AMQP。 脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。
    请根据想要使用的协议取消注释相应的代码行。


-   向下滚动到连接信息。
    找到 IoT 连接字符串的以下占位符：

        var connectionString = "[IoT Device Connection String]";

-   将上述占位符替换为设备连接字符串。 可根据[步骤 2](#Register) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。

-   按 Ctrl+O 保存更改，当 nano 提示是否保存到同一文件时，按 ENTER 即可。

-   按 Ctrl+X 退出 nano。

-   在退出 **~/azure-iot-sdk-node/device/samples** 目录之前运行以下命令

        npm link azure-iot-device

<a name="Run"></a>
## <a name="33-run-and-validate-the-samples"></a>3.3 运行并验证示例

在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心服务之间的通信。 我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。 此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。

**注意：** 请针对以下部分中执行的所有操作创建屏幕截图，如示例屏幕截图。 [步骤 4](#Share) 中需要用到这些屏幕截图

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1：向 IOT 中心发送设备事件：

1.  如[步骤 2](#Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。

    ![DeviceExplorer_Monitor](images/3_3_1_01.png)

2.  现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。

3.  发出以下命令运行该示例：

        node ~/azure-iot-sdk-node/device/samples/simple_sample_device.js

4. 检查是否已成功发送和接收数据。 如果出现任何问题，则可能表示未正确复制设备中心连接信息。

   ![Simple_Sample_result_terminal](images/3_3_1_02.png)

5.  DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。

    ![Simple_Sample_result_DeviceExplorer](images/3_3_1_03.png)


### <a name="332-receive-messages-from-iot-hub"></a>3.3.2 从 IoT 中心接收消息

1.  若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。

2.  使用设备 ID 下拉列表选择创建的设备。

3.  在“消息”字段中添加一些文本，然后单击“发送”按钮。

    ![MessageSend_DeviceExplorer](images/3_3_2_01.png)

4.  应会在客户端示例的控制台窗口中看到收到的命令。

    ![MessageSend_terminal](images/3_3_2_02.png)

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

-   请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。

<a name="PackageShare"></a>
# <a name="step-4-package-and-share"></a>步骤 4：打包和共享

<a name="Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a>4.1：打包生成日志和示例测试结果

从设备打包以下项目：

1.  生成运行过程中在日志文件记录的生成日志和 E2E 测试结果。

2.  前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。

3.  前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。

4.  前面“设备配置”部分中的所有屏幕截图。

5.  请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。 请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-nodejs.md>)提供的模板创建设备特定的说明。
    
    有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。

<a name="Share"></a>
## <a name="42-share-package-with-engineering-support"></a>4.2 与工程支持人员共享包

1.  转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。
2.  单击设备右上角的“上传”图标。

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  此时会打开上传对话框。 单击“上传”按钮浏览文件。

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    可以上传同一设备的多个文件。

4.  上传所有文件后，单击“提交审查”按钮。

    ***注意：*** 提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。
 

<a name="Next"></a>
## <a name="43-next-steps"></a>4.3：后续步骤

与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。

<a name="Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：故障排除

如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。
