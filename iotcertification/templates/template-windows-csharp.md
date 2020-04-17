---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: csharp
ms.openlocfilehash: e045a56e6a77226fa0f03353874acdf3d5e7f11e
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62439615"
---
<a name="run-a-simple-csharp-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 Csharp 示例
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

-   [准备开发环境][setup-devbox-windows]
-   [设置 IoT 中心][lnk-setup-iot-hub]
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备

-   {{写下安装、配置和连接设备所要遵照的说明。 请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

-   下载 [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp) 和示例程序，并将其保存到本地存储库。
-   打开设备控制台（命令提示符或 PowerShell 窗口），并切换到本地 SDK 的 **azure-iot-sdk-csharp** 目录。

-  在设备上以环境变量的形式添加 IoT 中心设备连接字符串：

        setx IOTHUB_DEVICE_CONN_STRING <yourDeviceConnectionString>

-  运行以下命令生成 SDK：

        build.cmd -config Release
        
- 在设备控制台中，使用以下命令运行示例：

    **如果使用 HTTP 协议：**

        cd iothub\device\samples\DeviceClientHttpSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientHttpSample.dll

    **如果使用 MQTT 协议：**

        cd iothub\device\samples\DeviceClientMqttSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientMqttSample.dll
        
    **如果使用 AMQP 协议：**

        cd iothub\device\samples\DeviceClientAmqpSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientAmqpSample.dll

-   使用 **DeviceExplorer** 实用工具观察 IoT 中心从**设备客户端示例**应用程序收到的消息。
-   参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“监视设备到云的事件”，查看设备正在发送的数据。
-   参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“发送云到设备的消息”，获取有关向设备发送消息的说明。

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
[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
