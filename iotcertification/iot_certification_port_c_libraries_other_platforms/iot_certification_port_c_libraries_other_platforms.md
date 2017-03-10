<a name="how-to-certify-iot-devices-on-non-supported-platforms-with-azure-iot-sdk"></a>如何使用 Azure IoT SDK 认证不支持的平台上的 IoT 设备
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：注册 Azure IoT 中心](#Step_1)
-   [步骤 2：注册设备](#Step_2)
-   [步骤 3：使用 C 客户端库生成并验证示例](#Step_3)
    -   [3.1 将 C 库移植到其他平台](#Step_3_1)
    -   [3.2 运行并验证示例](#Step_3_2)
-   [步骤 4：打包并共享](#Step_4)
    -   [4.1 打包生成日志和示例测试结果](#Step_4_1)
    -   [4.2 与 Azure IoT 认证团队共享](#Step_4_2)
    -   [4.3 后续步骤](#Step_4_3)
-   [步骤 5：故障排除](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT C SDK 认证已启用 IoT 的硬件的分步指南。 此过程由多个步骤组成，其中包括： 
-   配置 Azure IoT 中心 
-   注册 IoT 设备
-   在设备上生成并部署 Azure IoT SDK
-   打包并共享日志

**准备**

在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。

在开始过程前，应已准备好以下项目：

-   准备好一台装有 GitHub 并且可以访问 [azure-iot-sdks](https://github.com/Azure/azure-iot-sdks) GitHub 公共存储库的计算机。
-   配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。
-   用于认证的所需硬件。

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a>步骤 1：注册 Azure IoT 中心

遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。

在注册过程中，你将收到连接字符串。 

-   **IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a>步骤 2：注册设备

在本部分，将要使用 DeviceExplorer 注册设备。 DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：

-   设备管理
    -   创建新设备
    -   列出现有设备，公开设备中心内存储的设备属性
    -   可更新设备密钥
    -   可删除设备
-   监视设备的事件
-   向设备发送消息

若要运行 DeviceExplorer 工具，请根据[步骤&1;](#Step_1) 中所述使用以下配置字符串：

-   IoT 中心连接字符串
    

**步骤：**
1.  单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。

2.  添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。

3.  根据以下说明创建设备并将其注册到 IoT 中心。

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。 单击“管理”选项卡。

    b.保留“数据库类型”设置，即设置为“共享”。 注册的设备将显示在列表中。 如果你的设备未显示在列表中，请单击“刷新”按钮。 如果这是第一次注册设备，请不要检索任何信息。

    c. 单击“创建”按钮创建设备 ID 和密钥。

    d.单击“下一步”。 成功创建设备后，该设备将列在 DeviceExplorer 中。

    e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。 右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。

    f. 在记事本中保存此信息。 后面的步骤需要用到此信息。

***不是在电脑上运行 Windows？*** - 请遵照[此处](<https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md>)的说明预配设备并获取其凭据。

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a>步骤 3：使用 C 客户端库生成并验证示例

<a name="Step_3_1"></a>
## <a name="31-port-the-c-libraries-to-other-platforms"></a>3.1 将 C 库移植到其他平台

以下文档提供有关如何将 C 物联网 (IoT) 客户端库移植到不现成支持的平台的指南。 该文档包含有关任何特定平台的具体信息。

<https://github.com/Azure/azure-iot-sdks/blob/master/c/doc/porting_guide.md>

<a name="Step_3_2"></a>
## <a name="32-run-and-validate-the-samples"></a>3.2 运行并验证示例

在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。 我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。 

***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2) 中需要用到这些屏幕截图。*

<a name="Step_3_2_1"></a>
### <a name="321-send-device-events-to-iot-hub"></a>3.2.1 向 IoT 中心发送设备事件

1.  如[步骤 2](#Step_2) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。 从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。

    ![DeviceExplorer\_Monitor](images/3_2_1_01.png)

2.  现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。

3.  使用移植客户端库之后创建的、用于将设备事件发送到 IoT 中心的简单示例。

<a name="Step_3_2_2"></a>
### <a name="322-receive-messages-from-iot-hub"></a>3.2.2 从 IoT 中心接收消息

1.  若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。

2.  使用设备 ID 下拉列表选择创建的设备。

3.  在“通知”字段中添加一些文本，然后单击“发送”。

    ![DeviceExplorer\_NotificationSend](images/3_2_2_01.png)

4.  使用移植客户端库之后创建的、用于从 IoT 中心接收通知消息的示例。 应会看到收到的命令。

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a>步骤 4：打包并共享

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a>4.1 打包生成日志和示例测试结果

从设备打包以下项目：

1.  来自平台的生成日志和测试结果。

2.  “**向 IoT 中心发送设备事件**”部分中所示的所有屏幕截图。

3.  “**从 IoT 中心接收消息**”部分中所示的所有屏幕截图。

4.  创建一个文档，说明如何在硬件上运行示例（具体强调客户所要执行的新步骤）。 有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-sdks/tree/master/doc/get_started>) GitHub 存储库中发布的示例。

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a>4.2 与 Azure IoT 认证团队共享

1.  转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)
2.  单击设备右上角的“上载”图标。

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  此时将打开上载对话框。 单击“上载”按钮浏览文件。

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    可以上载同一个设备的多个文件。

4.  上载所有文件后，单击“提交审查”按钮。

    ***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a>4.3 后续步骤

与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：故障排除

如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。