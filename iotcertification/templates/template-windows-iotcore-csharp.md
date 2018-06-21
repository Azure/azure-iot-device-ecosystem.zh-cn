---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: csharp
ms.openlocfilehash: b8a8cf615825c6dd8263a67b29d2bd25deb3013d
ms.sourcegitcommit: 4b98ebc1c3cad79b3f19f21d36add53daa71e0b5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.locfileid: "19786095"
---
<a name="run-a-simple-csharp-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C# 示例
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：生成并运行示例](#Build)
-   [后续步骤](#NextSteps)

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

-   准备好一台装有 Git 客户端并且可以访问 [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub 公共存储库的计算机。
-   [设置 IoT 中心][lnk-setup-iot-hub]
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   {在此处输入设备名称} 设备。

#### <a name="install-visual-studio-2015-and-tools"></a>安装 Visual Studio 2015 和工具

-   若要创建 Windows IoT Core 解决方案，需安装 [Visual Studio 2015](https://www.visualstudio.com/en-us/products/vs-2015-product-editions.aspx)。 可以安装任意版本的 Visual Studio，包括免费的 Community 版。

    请务必选择“通用 Windows 应用开发工具”，这是编写 Windows 10 应用时必须使用的组件：

-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备

-   {{记下安装、配置和连接设备时需要遵循的说明。 请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

<a name="Step_3_1:_Connect"/>
## <a name="31-connect-the-device"></a>3.1 连接设备

-   使用以太网电缆将开发板连接到网络。 由于示例依赖于 Internet 访问，因此必须执行此步骤。

-   使用 micro-USB 电缆将设备插入计算机。

<a name="Step_3_2:_Build"/>
## <a name="32--build-the-samples"></a>3.2 生成示例

-   启动 Visual Studio 2015 的新实例。 打开存储库本地副本中的 **iothub_csharp_client.sln** 解决方案 (/azure-iot-sdk-csharp)。

-   在 Visual Studio 的“解决方案资源管理器”中，导航到 **UWPSample(Universal Windows)** 项目。

-   在 **ConnectionStrings.cs** 文件中找到以下代码：

        public const string DeviceConnectionString = "<replace>";

-   将上述占位符替换为在[步骤 1](#Prerequisites) 中获取的设备连接字符串，然后保存更改。

-   选择适当的体系结构（x86 或 ARM，具体取决于设备），将调试方法设置为“远程计算机”：
    
-   若要在设备上部署二进制文件，请在“解决方案资源管理器”中右键单击 UWPSample 项目，选择“属性”，然后导航到“调试”选项卡：

    键入设备的名称。 确保“使用身份验证”框处于未选中状态。

-   生成解决方案。

<a name="Step_3_3:_Run"/>
## <a name="33-run-and-validate-the-samples"></a>3.3 运行并验证示例

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1 向 IoT 中心发送设备事件

-   在 Visual Studio 的“解决方案资源管理器”中右键单击“UWPSample(Universal Windows)”项目，然后单击“调试”&minus;&gt;“启动新实例”生成并运行示例。 

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。

### <a name="332-receive-messages-from-iot-hub"></a>3.3.2 从 IoT 中心接收消息

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。

<a name="NextSteps"></a>
# <a name="next-steps"></a>后续步骤

现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。 若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：

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
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

