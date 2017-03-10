---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: javascript
translationtype: Human Translation
ms.sourcegitcommit: 342b2e268ae6ff4885f2d7b015f1c5dd4c3ae0ad
ms.openlocfilehash: 50014f5213d5ba251007c369aa2a86e7438d48cf
ms.lasthandoff: 01/19/2017

---

<a name="run-a-simple-javascript-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JavaScript 示例
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：生成并运行示例](#Build)

# <a name="instructions-for-using-this-template"></a>此模板的用法说明

-   将 {placeholders} 中的文本替换为正确的值。
-   阅读说明后，请删除 {{enclosed}} 行中包含的内容。
-   建议尽可能地使用外部链接。
-   请从最终文档中删除本部分。

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。 此过程由多个步骤组成，其中包括：
-   配置 Azure IoT 中心
-   注册 IoT 设备
-   在设备上生成并部署 Azure IoT SDK

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a>步骤 1：先决条件

在开始过程前，应已准备好以下项目：


-   [准备开发环境][setup-devbox-linux]
-   [设置 IoT 中心][lnk-setup-iot-hub]
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   装有 Git 客户端的计算机
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备

-   在 **C:\OpenSSL** 位置安装 OpenSSL 并执行以下操作：
    -   将 `C:\OpenSSL\` 添加到 **PATH** 环境变量
    -   在 OpenSSL 目录中搜索“openssl.cnf”文件的位置。
    -   创建新环境变量 **OPENSSL_CONF** 并将其值设置为 `openssl.cnf` 文件的绝对路径。
    
-   {{记下安装、配置和连接设备时需要遵循的说明。 请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a>3.1 在设备上加载 Azure IoT 代码和必备组件

-   创建环境变量 `IOTHUB_CONNECTION_STRING`，并将其值设置为在[步骤 1](#Prerequisites) 中获取的 **IoT 中心连接字符串**。

-   打开 Node.js 命令提示符。
        
-   检查是否已正确设置所有环境变量。

        echo %PATH%
        echo %OPENSSL_CONF%
        echo %IOTHUB_CONNECTION_STRING%
    
-   下载该 SDK 

        git clone --recursive https://github.com/Azure/azure-iot-sdks.git


<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a>3.2 生成示例

-   若要验证源代码，请在设备上的 Node.js 命令提示符下运行以下命令。

        cd azure-iot-sdks\node
        build\dev-setup.cmd
        build\build.cmd > LogFile.txt

    ***注意：****应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*

-   安装 npm 包以运行示例。

        cd \azure-iot-sdks\node\device\samples

    **对于 AMQP 协议：**
    
        npm install azure-iot-device-amqp
    
    **对于 HTTP 协议：**
    
        npm install azure-iot-device-http
    
    **对于 MQTT 协议：**

        npm install azure-iot-device-mqtt   

-   更新示例以设置协议。

        cd azure-iot-sdks\node\device\samples
        notepad simple_sample_device.js

-   这会启动文本编辑器。 向下滚动到协议信息，找到以下代码：

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    使用的默认协议为 AMQP。 脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。 
    请根据想要使用的协议取消注释相应的代码行。

-   向下滚动到连接信息，找到 IoT 连接字符串的以下占位符：

        var connectionString = "[IoT Device Connection String]";

-   将上述占位符替换为设备连接字符串。 可根据[步骤 1](#Prerequisites) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。

-   保存更改并关闭记事本。

-   退出 **azure-iot-sdks\node\device\samples** 目录之前，在 Node.js 命令提示符下运行以下命令

        npm link azure-iot-device

<a name="Run"></a>

## <a name="33-run-and-validate-the-samples"></a>3.3 运行并验证示例

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1 向 IoT 中心发送设备事件

-   发出以下命令运行示例，验证是否已成功发送和接收数据。

        node azure-iot-sdks\node\device\samples\simple_sample_device.js

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。

### <a name="332-receive-messages-from-iot-hub"></a>3.3.2 从 IoT 中心接收消息

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。

[setup-devbox-linux]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/node-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

