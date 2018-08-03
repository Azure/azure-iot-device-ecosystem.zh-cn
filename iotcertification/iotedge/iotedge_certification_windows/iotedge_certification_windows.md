<a name="how-to-certify-iot-edge-devices-running-windows"></a>如何认证运行 Windows 的 IoT Edge 设备
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：配置 Azure IoT Edge](#Step-1-Configure)
-   [步骤 2：注册设备](#Step-2-Register)
-   [步骤 3：在设备上对 Azure IoT Edge 进行手动测试](#Step-3-Manual)
    -   [3.1：IoT Edge 运行时](#Step-3-1-IoTEdgeRunTime)
    -   [3.2：设备管理](#Step-3-2-DeviceManagement)
    -   [3.3：安全性](#Step-3-3-Security)
-   [步骤 4：打包和共享](#Step-4-Package_Share)
    -   [4.1：在原始包装中打包生成日志和设备](#Step-4-1-Package-build)
    -   [4.2：与 Microsoft Azure IoT 团队成员共享包](#Step-4-2-Share-Package)
    -   [4.3：后续步骤](#Step-4-3-Next-Step)
-   [步骤 5：故障排除](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT Edge 的硬件。 此过程由多个步骤构成，具体包括：

-   配置 Azure IoT Edge
-   注册 IoT Edge 设备
-   在设备上对 Azure IoT Edge 进行手动测试
-   打包和共享日志

**准备工作：**

在执行以下任何步骤之前，请仔细阅读每个步骤，确保对整个过程有全面的了解。

在开始过程前，应已准备好以下项目：

-   一台装有 GitHub 的计算机，并且能够访问 [azure-iot-sdk](https://github.com/Azure/azure-iot-sdks) GitHub 公共存储库。
-   安装 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，以及[系统要求](https://github.com/ms-iot/iot-core-azure-dm-client)中指出的所需包。 可以安装任何版本的 Visual Studio，包括免费的社区版。

注意：如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](https://catalog.azureiotsolutions.com/)请求此身份，然后遵照本文中的说明操作。

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a>步骤 1：注册 Azure IoT 中心

遵照[此处](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart)所述的说明[注册](https://account.windowsazure.com/signup?offer=ms-azr-0044p) Azure IoT 中心服务。 在注册过程中，将会收到连接字符串。

-   **IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a>步骤 2：注册设备

在本部分，我们将使用 DeviceExplorer 注册 Edge 设备。 DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：

-   设备管理
    -   创建新设备
    -   列出现有设备并公开设备中心存储的设备属性
    -   提供更新设备密钥的功能
    -   提供删除设备的功能
-   监视设备的事件
-   将消息发送到设备

若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step-1-Configure) 中所述的以下配置字符串：

-   IoT 中心连接字符串

**步骤：**
1.  单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。

2.  在“配置”选项卡下添加连接信息，并单击“更新”按钮。

3.  根据以下说明创建设备并将其注册到 IoT 中心。

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。 单击“管理”选项卡。

    b.保留“数据库类型”设置，即设置为“共享”。 注册的设备将显示在列表中。 如果该设备未显示在列表中，请单击“刷新”按钮。 如果这是第一次注册设备，请不要检索任何信息。

    c. 单击“创建”按钮创建设备 ID 和密钥。

    d.单击“下一步”。 成功创建设备后，该设备将列在 DeviceExplorer 中。

    e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。 右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。

    f. 在记事本中保存此信息。 后面的步骤需要用到此信息。

***不是在电脑上运行 Windows？*** - 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。
<a name="Step-3-Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a>步骤 3：在设备上对 Azure IoT Edge 进行手动测试

本部分将引导你在运行 Windows 操作系统的 Edge 设备上执行测试，使该设备符合 Azure IoT Edge 认证的要求 

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a>3.1：Edge RuntimeEnabled（必需）

级别总数：1

**说明：** 一个包含 Azure IoT Edge 运行时和依赖项的设备。请从以下途径下载 Azure IoT Edge 运行时：

对于 Windows IoT Core，请从该[链接](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-core.md)安装运行时。

对于要用于 Linux 容器的 Windows x64 (AMD/Intel)，请从该[链接](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-edge-windows-with-linux.md)安装运行时。

对于要用于 Windows 容器的 Windows x64 (AMD/Intel)，请从该[链接](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-edge-windows-with-windows.md)安装运行时。

**要求详细信息：**

预装以下组件，或者由分销点在设备上为客户安装这些组件：

-   Azure IoT Edge 安全守护程序
-   守护程序配置文件
-   Moby 容器管理系统
-   版本 `hsmlib` 

在通过 DPS 集成启动时，或者当用户在 **config** 文件中输入设备凭据后，IoT Edge 运行时将正常运行。

**测试步骤：**

-   公司必须将 Edge 设备寄送到 Microsoft 进行额外的验证。 当公司提交设备进行 Azure IoT Edge 认证时，我们会发送详细说明和我们所需的信息。
-   公司需确保 Edge 设备上同时预装了 Azure IoT Edge 安全守护程序和 Moby 容器管理系统
    -   Microsoft 会检查 Edge 设备上是否附带 Azure IoT Edge 安全守护程序
    -   Microsoft 会检查 Edge 设备上是否附带 Moby 容器管理系统
-   公司需向 Microsoft 提供有关如何通过电子邮件连接到 IoT 中心的说明
    -   用于连接的配置文件
    -   设备的预配方式
    -   其他重要信息 
-   请等待一段时间，让 Microsoft 处理和完成认证过程。 审批后，Microsoft 会寄回 Edge 设备。

<a name="Step-3-2-DeviceManagement"></a>
## <a name="32-device-management-mandatory"></a>3.2：设备管理（必需）
级别总数：1

**先决条件：** 设备连接。

**说明：** 可以执行由 IoT 中心发出的消息触发的基本设备管理操作的设备。

**要求详细信息：**

设备中必须配备具有以下功能的组件：

1.  支持使用设备孪生来触发固件或操作系统更新，以及报告状态（包括错误消息或详细信息）
2.  支持使用直接方法来触发重新启动，并使用设备孪生来报告上次启动时间。

组件可以预装，或者在分销点为客户安装。

**手动测试：** 

以下测试将验证 Windows IoT Core 设备管理客户端是否已安装，并设置为以服务的形式运行

1.  遵循针对 Windows IoT [设备管理](https://github.com/ms-iot/iot-core-azure-dm-client/blob/master/docs/azure-dm-certification.md)客户端运行 Azure 认证时所用的相同步骤。 
2.  将日志文件连同提交内容一起发送

<a name="Step-3-3-Security"></a>
## <a name="33-security-optional"></a>3.3：安全性（可选）
级别总数：4

 **注意：** Microsoft 正在致力于定义安全要求方面的验证过程，包括审查第三方验证实验室的使用。 
 
#### <a name="331-device-securitylevel1"></a>3.3.1：Device Security.Level1 

**说明：** 

如果设备使用安全协议的自定义实现，而不是使用 Azure IoT 设备 SDK，则设备将认证为“级别 1”。 

**要求详细信息：**

-   最低安全级别 
-   不使用 Azure IoT 设备 SDK 的 IoT Edge 设备 
-   此项要求没有测试步骤。 如果安装了 Edge 运行时并且与 IoT 中心建立了连接，则设备自动符合此级别 
 
#### <a name="332-device-securitylevel2"></a>3.3.2：Device Security.Level2 

**说明：** 

如果设备可以使用 Azure IoT 设备 SDK 实现设备安全协议，则设备将认证为“级别 2”。 

**要求详细信息：**

-   验证 Azure IoT 设备 SDK 的使用情况 
 
#### <a name="333-device-securitylevel-3"></a>3.3.3：Device Security.Level 3 

**说明：**

 如果设备使用硬件安全模块来增强安全性，则设备将认证为“级别 3”。  这种验证是通过安全认证完成的。
 
**要求详细信息：**

此级别需要满足以下“安全性”认证要求： 

-    FIPS 140-2 级别 2 或更高 
-    通用准则 EAL 3+ 
 
#### <a name="334-device-securitylevel-4"></a>3.3.4：Device Security.Level 4 

**说明：**

 如果设备使用硬件安全模块来增强安全性，则设备将认证为“级别 4”。  这种验证是通过安全认证完成的。
 
**要求详细信息：** 

此级别需要满足以下“安全性”认证要求：

-   FIPS 140-2 级别 3 或更高 
-   通用准则 EAL 4+ 
    
<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a>步骤 4：打包和共享
<a name="Step-4-1-Package-build"></a>
## <a name="41-package-build-logs-and-device-in-original-box"></a>4.1：在原始包装中打包生成日志和设备 
打包设备中的以下项目：

1.  “设备管理手动测试”中所述的日志文件。
2.  装有 IoT Azure 运行时，并已寄送到 Microsoft 做进一步验证的设备

<a name="Step-4-2-Share-Package"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a>4.2：与 Microsoft Azure IoT 团队成员共享包

1.  转到[合作伙伴仪表板](https://catalog.azureiotsolutions.com/devices)
2.  单击设备右上角的“上传”图标。

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  此时会打开上传对话框。 单击“上传”按钮浏览文件。

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    可以上传同一设备的多个文件。

4.  上传所有文件后，单击“提交审查”按钮。

    ***注意：*** 提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。

<a name="Step-4-3-Next-Step"></a>
## <a name="43-next-steps"></a>4.3：后续步骤

与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：故障排除

如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。