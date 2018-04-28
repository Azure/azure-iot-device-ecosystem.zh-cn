<a name="how-to-certify-iot-devices-running-openwrt-on-arduino-with-azure-iot-sdk"></a>如何使用 Azure IoT SDK 认证运行 Openwrt on Arduino 的 IoT 设备
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Step-1-Prerequisites)
-   [步骤 2：注册设备](#Step-2-PrepareDevice)
-   [步骤 3：生成并运行示例](#Step-3-Build)
    -   [3.1：设置开发环境](#Step-3-1-setup-dev)
    -   [3.2：生成示例](#build)
    -   [3.3：部署示例](#deploy)
    -   [3.4：确保已安装证书](#certificate)
    -   [3.5：运行示例](#run-the-sample)
-   [步骤 4：打包和共享](#Step-4-Package_Share)
    -   [4.1：打包生成日志和示例测试结果](#Step-4-1-Package)
    -   [4.2：与工程支持人员共享包](#Step-4-2-Share)
    -   [4.3：后续步骤](#Step-4-3-Next)
-   [步骤 5：故障排除](#Step-5-Troubleshooting)
    -   [5.1：E2E 测试用例](#Step-5-1-E2E)

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

以下文档介绍了将 Arduino 系统连接到 Azure IoT 中心的过程。此过程由多个步骤构成，具体包括：
-  配置 Azure IoT 中心
-  注册 IoT 设备
-  在设备上生成和部署 Azure IoT SDK
-  打包和共享日志

**准备**

在执行以下任何步骤之前，请先仔细阅读每个过程的每个步骤，确保对整个过程有全面的了解。

在开始过程前，应已准备好以下项目：

-   一台装有 GitHub 的计算机，并且能够访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 公共存储库。
-   用于访问命令行的 SSH 客户端，例如 [PuTTY](http://www.putty.org/)。
-   需要认证的硬件。

***注意：***如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://catalog.azureiotsuite.com/>)请求此身份，然后遵照本文中的说明操作。


<a name="Step-1-Prerequisites"></a>
# <a name="step-1-prerequisites"></a>步骤 1：先决条件

在开始过程前，应已准备好以下项目：
  - 装有 Git 客户端的计算机，以便可以访问 GitHub 上的 azure-iot-sdks 代码。
  - Arduino Yun 开发板。
  - Ubuntu x86 计算机（用于交叉编译） 
  - [设置 IoT 中心](../setup_iothub.md) 
  - [预配设备并获取其凭据](../manage_iot_hub.md)



<a name="Step-1-Configure"></a>
## <a name="step-11-configure-azure-iot-hub"></a>步骤 1.1：配置 Azure IoT 中心

遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务和配置 Azure IoT 中心。 在注册过程中，将会收到连接字符串。

-   **IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a>步骤 2：注册设备

在本部分，我们将使用 DeviceExplorer 注册设备。 DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：

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

3.  使用以下说明创建设备并将其注册到 IoT 中心。

    a. 单击“管理”选项卡。

    b. 列表中会显示已注册的设备。 如果该设备未显示在列表中，请单击“刷新”按钮。 如果这是第一次执行此操作，则不应检索任何信息。

    c. 单击“创建”按钮创建设备 ID 和密钥。

    d. 成功创建后，设备会列在 DeviceExplorer 中。

    e. 右键单击该设备，并从上下文菜单中选择“复制所选设备的连接字符串”。

    f. 在记事本中保存此信息。 后面的步骤需要用到此信息。

***不是在电脑上运行 Windows？*** - 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。

<a name="Step-3-Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a>步骤 3：使用 C 客户端库生成并验证示例

本部分逐步讲解如何为 Arduino 上的 Openwrt 平台生成、部署和验证 IoT 客户端 SDK。 我们将在设备上安装所需的必备组件。 完成后，将会生成并部署 IoT 客户端 SDK，并使用 Azure IoT SDK 来验证 IoT 认证所需的示例测试。

<a name="Step-3-1-setup-dev"></a>
## <a name="31-setup-the-development-environment"></a>3.1：设置开发环境

-   打开 PuTTY 会话并连接到设备。

-   通过设备上的命令行发出以下命令，安装必备的包。

    在 root/sudo 下安装依赖项。 

``` 
apt-get install curl libcurl4-openssl-dev uuid-dev uuid g++ make cmake git unzip openjdk-7-jre libssl-dev libncurses-dev subversion gawk
```

- 将此存储库 ([azure-iot-sdk](https://github.com/Azure/azure-iot-sdks)) 克隆到所用的计算机。请务必使用以下命令执行递归克隆 (git clone --recursive <repo address>)。

        git clone --recursive https://github.com/Azure/azure-iot-sdk-c.git
- 导航到存储库本地副本中的 **c/build_all/arduino** 文件夹。
- 运行 `./setup.sh` 脚本安装 OpenWRT SDK 和必备组件。 SDK 默认安装在 **~/openwrt/sdk** 中
- （可选）输入“Y”生成 Azure IoT SDK。


    ***注意：***此安装过程需要 cmake 2.8.12 或更高版本。 
    
    可使用以下命令来验证环境中当前安装的版本：

        cmake --version

    此库还需要 gcc 4.9 或更高版本。可使用以下命令来验证环境中当前安装的版本：
    
        gcc --version    
    
-   检查 ~/azure-iot-sdk-c 目录下现在是否包含源代码的副本。

<a name="build"/>
## <a name="32-build-the-sample"></a>3.2：生成示例

- 在文本编辑器（例如 nano）中打开文件 **azure-iot-sdk-c/serializer/samples/simplesample_http/simplesample_http.c**
- 在该文件中找到以下代码：
```
static const char* connectionString = "[device connection string]";
```
- 将“[device connection string]”替换为[前面](#Step-1-Configure)记下的设备连接字符串。 保存更改。
- 运行 **azure-iot-sdk-c/build_all/arduino** 目录中的 `./build.sh` 脚本。   

<a name="deploy"/>
## <a name="33-deploy-the-sample"></a>3.3：部署示例

- 打开 shell 并导航到安装的 OpenWRT SDK 文件夹。 该文件夹默认为 **~/openwrt/sdk**。
- 传输示例可执行文件。

OpenWRT Yun 映像：

```
scp ~/openwrt/sdk/build_dir/target-mips_r2_uClibc-0.9.33.2/azure-iot-sdks-1/serializer/samples/simplesample_http/simplesample_http root@arduino.local:/tmp
```

***注意：此处的 uClibc 版本可能与你安装的版本不同，因此可能需要相应地调整路径。***
<a name="certificate"/>
## <a name="34-make-sure-the-certificates-are-installed"></a>3.4：确保已安装证书

在 Arduino 设备上，安装如下所示的 ca-certificates 包：

```
wget https://downloads.openwrt.org/snapshots/trunk/ar71xx/generic/packages/base/ca-certificates_20160104_all.ipk --no-check-certificate
opkg install ca-certificates_20160104_all.ipk
```
执行此步骤时可能会收到错误消息（返回代码 127），但证书将会安装。

***注意：发布更新的证书版本后，上述证书名称可能会发生变化。如果在下载证书文件时收到 404 错误，请仔细检查[此处](https://downloads.openwrt.org/snapshots/trunk/ar71xx/generic/packages/base)所述基本路径下的 CA 证书名称，并相应地更新证书路径。***

<a name="run-the-sample"/>
## <a name="35-run-the-sample"></a>3.5：运行示例
在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。 我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。 此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。

**注意：**请对本部分中执行的所有操作截图。 在[步骤 4](#Step-4-2-Share) 中需要使用这些屏幕截图。

- 运行示例 **/tmp/simplesample_http**
- 请参阅[管理 IoT 中心][lnk-manage-iothub]，了解用于监视设备向 IoT 中心发送的消息以及向设备发送命令的工具的信息。

***注意：若要从 iothub-explorer 或 DeviceExplorer 向设备发送命令，该命令应类似于 {"Name":"TurnFanOff","Parameters":{}}***

<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a>步骤 4：打包和共享

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a>4.1：打包生成日志和示例测试结果

打包设备中的以下项目：

1.  在生成运行期间记录在日志文件中的生成日志和 E2E 测试结果。

2.  在执行[步骤 3](#run-the-sample) 期间抓取的所有屏幕截图

4.  请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。 请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>)提供的模板创建设备特定的说明。
    
    有关说明的大致形式的指导，请参阅[此](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a>4.2：与 Microsoft Azure IoT 团队成员共享包

1.  转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。
2.  单击设备右上角的“上传”图标。

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  此时会打开上传对话框。 单击“上传”按钮浏览文件。

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    可以上传同一设备的多个文件。

4.  上传所有文件后，单击“提交审查”按钮。

    ***注意：***提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。
 

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a>4.3：后续步骤

与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：故障排除

如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。

[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[setup-iothub]: ../setup_iothub.md
[lnk-manage-iothub]: ../manage_iot_hub.md