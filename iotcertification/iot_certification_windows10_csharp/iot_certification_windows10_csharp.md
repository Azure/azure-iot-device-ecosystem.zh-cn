<a name="how-to-certify-iot-devices-running-windows-10-with-azure-iot-sdk"></a>如何使用 Azure IoT SDK 认证运行 Windows 10 的 IoT 设备 
===
---


# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：注册 Azure IoT 中心](#Step_1:_Sign_Up)
-   [步骤 2：注册设备](#Step_2:_Register)
-   [步骤 3：使用 C# 客户端库生成并验证示例](#Step_3:_Build_and_Validate)
    -   [3.1 准备开发环境](#Step_3_1:_Development)
    -   [3.2 生成示例](#Step_3_2:_Build)
    -   [3.3 运行并验证示例](#Step_3_3:_Run)
-   [步骤 4：打包并共享](#Step_4:_Package_Share)
    -   [4.1 打包生成日志和示例测试结果](#Step_4_1:_Package)
    -   [4.2 与工程支持人员共享包](#Step_4_2:_Share)
    -   [4.3 后续步骤](#Step_4_3:_Next)
-   [步骤 5：故障排除](#Step_5:_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。 此过程由多个步骤组成，其中包括：
-   配置 Azure IoT 中心 
-   注册 IoT 设备
-   在设备上生成并部署 Azure IoT SDK
-   打包并共享日志  

**准备**

在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。

在开始过程前，应已准备好以下项目：

-   准备好一台装有 GitHub 并且可以访问 [azure-iot-sdks](https://github.com/Azure/azure-iot-sdks) GitHub 公共存储库的计算机。
-   安装 Visual Studio 2015 和工具。 可以安装任意版本的 Visual Studio，包括免费的 Community 版。

<a name="Step_1:_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a>步骤 1：注册 Azure IoT 中心

遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。

在注册过程中，你将收到连接字符串。

-   **IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2:_Register"></a>
# <a name="step-2-register-device"></a>步骤 2：注册设备

在本部分，将要使用 DeviceExplorer 注册设备。 DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：

-   设备管理
    -   创建新设备
    -   列出现有设备，公开设备中心内存储的设备属性
    -   可更新设备密钥
    -   可删除设备
-   监视设备的事件
-   向设备发送消息

若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1:_Sign_Up) 中所述使用以下配置字符串：

-   IoT 中心连接字符串

**步骤：**

1.  单击[此处](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md)下载并安装 DeviceExplorer。

2.  添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。

3.  根据以下说明创建设备并将其注册到 IoT 中心。

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。 单击“管理”选项卡。    
    
    b.保留“数据库类型”设置，即设置为“共享”。 注册的设备将显示在列表中。 如果你的设备未显示在列表中，请单击“刷新”按钮。 如果这是第一次注册设备，请不要检索任何信息。
       
    c. 单击“创建”按钮创建设备 ID 和密钥。 
    
    d.单击“下一步”。 成功创建设备后，该设备将列在 DeviceExplorer 中。 
    
    e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。 右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。
    
    f. 在记事本中保存此信息。 后面的步骤需要用到此信息。

**不是在电脑上运行 Windows？** - 请通过 <iotcert@microsoft.com> 向我们发送电子邮件，我们将会跟进你的问题，并提供 Azure IoT SDK 的操作说明。

<a name="Step_3:_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a>步骤 3：使用 C# 客户端库生成并验证示例 

本部分逐步讲解如何在运行 Windows 10 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。 我们将在设备上安装必备组件。 完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。

<a name="Step_3_1:_Development"></a>
## <a name="31-prepare-your-development-environment"></a>3.1 准备开发环境

本文档介绍如何准备开发环境，以便能够使用适用于 C# 的 Microsoft Azure IoT 设备 SDK。

- 安装 [Visual Studio 2015](https://www.visualstudio.com/)。 可以使用任意版本的 Visual Studio 2015，包括 Community 版。

- 安装用于 .NET 的 Azure SDK
    -    [VS 2015](http://go.microsoft.com/fwlink/?LinkId=518003)
    -    [VS 2013](http://go.microsoft.com/fwlink/?LinkId=323510)
    -    [VS 2012](http://go.microsoft.com/fwlink/?LinkId=323511)

<a name="Step_3_2:_Build"></a>
## <a name="32--build-the-samples"></a>3.2 生成示例

1.  启动 Visual Studio 2015 的新实例。 打开本地 SDK **azure-iot-sdks** 目录中 **csharp\device** 文件夹内的 **iothub_csharp_deviceclient.sln** 解决方案。

2.  在 Visual Studio 的“解决方案资源管理器”中，根据所选的协议导航到相应的项目：

    **对于 AMQP 协议：**

    导航到“DeviceClientAmqpSample”项目并打开“Program.cs”文件。

    **对于 HTTP 协议：**
    
    导航到“DeviceClientHttpSample”项目并打开“Program.cs”文件。

    **对于 MQTT 协议：**
    
    导航到“DeviceClientMqttSample”项目并打开“Program.cs”文件。

    ![Navigation\_terminal](images/navigation_2.png)


3.  根据协议，在任一示例应用程序中的 **Program.cs** 内找到以下代码：

          private const string DeviceconnectionString = "[device connection string]";
    
4.  将 [device connection string] 替换为设备的连接字符串，然后**保存**更改。 如[步骤 2](#Step_2:_Register) 中所述，可从 DeviceExplorer 获取连接字符串。

<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-samples"></a>3.3 运行并验证示例
    
在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。 我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。 此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。

***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2:_Share) 中需要用到这些屏幕截图。*

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1 向 IoT 中心发送设备事件

1.  如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。 从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。

    ![DeviceExplorer\_Monitor](images/3_3_1_01.png)

2.  现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。
     

3.  在 Visual Studio 的“解决方案资源管理器”中，右键单击“DeviceClientAmqpSample”、“DeviceClientHttpSample”或“DeviceClientMqttSample”项目，单击“调试”，然后单击“启动新实例”生成并运行示例。 
   
4. 成功执行后，设备控制台中应会显示收到的事件。

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

1.  若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。

2.  使用设备 ID 下拉列表选择创建的设备。

3.  在“消息”字段中添加一些文本，然后单击“发送”。

       ![DeviceExplorer\_Notification\_Send](images/device_message_receive_from_device_http.png)

4. 设备控制台窗口中应会显示收到的消息。
    
    **如果使用 HTTP 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

    **如果使用 MQTT 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_mqtt.png)

    **如果使用 AMQP 协议：**

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_amqp.png)
    
<a name="Step_4:_Package_Share"></a>
# <a name="step-4-package-and-share"></a>步骤 4：打包并共享

<a name="Step_4_1:_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a>4.1 打包生成日志和示例测试结果
  
从设备打包以下项目：

1.  第 3.2 部分中所述的生成日志。
2.  前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。
3.  前面“**从 IoT 中心接收消息**”部分中显示的所有屏幕截图。
4.  向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。 请使用[此处](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-csharp.md)提供的模板创建特定于设备的说明。

    有关说明形式的指导，请参考[此处](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started) github 存储库中发布的示例。

<a name="Step_4_2:_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a>4.2 与 Azure IoT 认证团队共享包

1.  转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)
2.  单击设备右上角的“上载”图标。

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  此时将打开上载对话框。 单击“上载”按钮浏览文件。

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    可以上载同一个设备的多个文件。

4.  上载所有文件后，单击“提交审查”按钮。

    ***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*
 

<a name="Step_4_3:_Next"></a>
## <a name="43-next-steps"></a>4.3 后续步骤

与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。

<a name="Step_5:_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：故障排除

如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。
