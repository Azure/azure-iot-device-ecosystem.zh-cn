---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: javascript
ms.openlocfilehash: 96df8ca2bad7d4bef51c5180c4926c9aefa6fc0b
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62439603"
---
<a name="run-a-simple-javascript-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JavaScript 示例
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：生成并运行示例](#Build)
-   [后续步骤](#NextSteps)

# <a name="instructions-for-using-this-template"></a>有关使用此模板的说明

-   将 {placeholders} 中的文本替换为正确的值。
-   遵照 {{enclosed}} 行之间的说明后，删除这些行。
-   建议尽量使用外部链接。
-   请从最终文档中删除本部分。

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。 此过程由多个步骤构成，具体包括：
-   配置 Azure IoT 中心
-   注册 IoT 设备
-   在设备上生成和部署 Azure IoT SDK

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
    
-   {{写下安装、配置和连接设备所要遵照的说明。 请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a>3.1：在设备上加载 Azure IoT 代码和必备组件

-   创建环境变量 `IOTHUB_CONNECTION_STRING`，并将其值设置为在[步骤 1](#Prerequisites) 中获取的 **IoT 中心连接字符串**。

-   打开 Node.js 命令提示符。
        
-   检查是否已正确设置所有环境变量。

        echo %PATH%
        echo %OPENSSL_CONF%
        echo %IOTHUB_CONNECTION_STRING%
    
-   下载该 SDK 

        git clone --recursive https://github.com/Azure/azure-iot-sdk-node.git


<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a>3.2：生成示例

-   若要验证源代码，请在设备上的 Node.js 命令提示符下运行以下命令。

        cd azure-iot-sdk-node
        build\dev-setup.cmd
        build\build.cmd > LogFile.txt

    ***注意：****应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*

-   安装 npm 包以运行示例。

        cd \azure-iot-sdk-node\device\samples

    **对于 AMQP 协议：**
    
        npm install azure-iot-device-amqp
    
    **对于 HTTP 协议：**
    
        npm install azure-iot-device-http
    
    **对于 MQTT 协议：**

        npm install azure-iot-device-mqtt   

-   更新示例以设置协议。

        cd azure-iot-sdk-node\device\samples
        notepad simple_sample_device.js

-   这会启动文本编辑器。 向下滚动到协议信息，找到以下代码：

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    使用的默认协议为 AMQP。 脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。 
    请根据想要使用的协议取消注释相应的代码行。

-   向下滚动到连接信息，找到 IoT 连接字符串的以下占位符：

        var connectionString = "[IoT Device Connection String]";

-   将上述占位符替换为设备连接字符串。 可根据[步骤 1](#Prerequisites) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。

-   保存更改并关闭记事本。

-   退出 **azure-iot-sdk-node\device\samples** 目录之前，在 Node.js 命令提示符下运行以下命令

        npm link azure-iot-device

<a name="Run"></a>

## <a name="33-run-and-validate-the-samples"></a>3.3：运行并验证示例

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1：向 IoT 中心发送设备事件

-   发出以下命令运行示例，验证是否已成功发送和接收数据。

        node azure-iot-sdk-node\device\samples\simple_sample_device.js

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。

### <a name="332-receive-messages-from-iot-hub"></a>3.3.2：从 IoT 中心接收消息

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。

<a name="NextSteps"></a>
# <a name="next-steps"></a>后续步骤

现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。 若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：

-   [使用 iothub-explorer 管理云设备消息传送]
-   [将 IoT 中心消息保存到 Azure 数据存储]
-   [使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]
-   [使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]
-   [在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]
-   [使用逻辑应用执行远程监视和发送通知]   

[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[setup-devbox-linux]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/node-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

