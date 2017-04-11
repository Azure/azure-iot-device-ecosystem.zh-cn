---
platform: 
device: 
language: csharp
ms.openlocfilehash: 4c82cb2cf62cf9e753353160f16b2f10c68e371d
ms.sourcegitcommit: c6e6e2af724a112c8dc1a00dee046036968ef192
translationtype: HT
---
<a name="run-a-simple-csharp-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C# 示例
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

-   [准备开发环境][setup-devbox-windows]
-   [设置 IoT 中心][lnk-setup-iot-hub]
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备

-   {{记下安装、配置和连接设备时需要遵循的说明。 请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

-   下载 [Azure IoT SDK](https://github.com/Azure/azure-iot-sdks) 和示例程序，并将其保存到本地存储库。
-   启动 Visual Studio 2015 的新实例。
-   打开存储库本地副本中的 `csharp\device` 文件夹内的 **iothub_csharp_client.sln** 解决方案。
-   在 Visual Studio 的“解决方案资源管理器”中，导航到 **samples** 文件夹。
-   在 **DeviceClientAmqpSample** 项目中打开 ***Program.cs*** 文件。
-   在该文件中找到以下代码：

        private const string DeviceConnectionString = "<replace>";
        
-   将 `<replace>` 替换为设备的连接字符串。
-   在“解决方案资源管理器”中右键单击“DeviceClientAmqpSample”项目，单击“调试”，然后单击“启动新实例”生成并运行示例。 当应用程序向 IoT 中心发送设备到云的消息时，控制台会显示消息。
-   使用 **DeviceExplorer** 实用工具来监视 IoT 中心从**设备客户端 AMQP 示例**应用程序接收的消息。
-   参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“监视设备到云的事件”，确定设备是否正在发送数据。
-   参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“发送云到设备的消息”，获取有关向设备发送消息的说明。

[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
