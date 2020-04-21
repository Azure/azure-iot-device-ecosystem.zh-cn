---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: c
ms.openlocfilehash: 862b306edd866511b6c4c9c9bf9c940caaf7ed29
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81480740"
---
<a name="connect-enter-your-device-name-here-device-to-your-azure-iot-central-application"></a>将 {在此处输入设备名称} 设备连接到 Azure IoT Central 应用程序
===

---
# <a name="table-of-contents"></a>目录

-   [简介](#Introduction)
-   [先决条件](#Prerequisites)
-   [创建 Azure IoT Central 应用程序](#Create_AICA)
-   [设备连接详细信息](#DeviceConnectionDetails)
-   [准备设备](#preparethedevice)
-   [与 IoT Central 集成](#IntegrationwithIoTCentral)
-   [其他链接](#AdditionalLinks)

# <a name="instructions-for-using-this-template"></a>有关使用此模板的说明

-   将 {placeholders} 中的文本替换为正确的值。
-   阅读说明后，请删除 {{enclosed}} 行中包含的内容。
-   建议尽可能地使用外部链接。
-   请从最终文档中删除本部分。

<a name="Introduction"></a>

# <a name="introduction"></a>介绍 

**关于本文档**

本文档介绍如何使用“IoT 即插即用”模型将 {在此处输入设备名称} 连接到 Azure IoT Central 应用程序。 “即插即用”使解决方案开发人员可以在不编写任何设备代码的情况下集成设备，从而简化了 IoT。 使用“即插即用”，设备制造商将向云开发人员提供其设备的模型，使设备可以快速集成到 IoT Central 或在 Azure IoT 平台上构建的任何解决方案。 “IoT 即插即用”将以定义语言和 SDK 的方式开放给社区。

{请在此处提供设备的简介和功能}

<a name="Prerequisites"></a>
# <a name="prerequisites"></a>先决条件

在开始过程前，应已准备好以下项目： 

-   [Azure 帐户](https://portal.azure.com)
-   [Azure IoT 中心实例](https://docs.microsoft.com/en-us/azure/iot-hub/about-iot-hub)
-   [Azure IoT 中心设备预配服务](https://docs.microsoft.com/en-us/azure/iot-dps/about-iot-dps)
-   提供设备支持的网络连接（WiFi、LAN）
-   若要启用“即插即用”，必须在设备中预安装设备代码/软件映像
-   {请在此处提供开发环境安装指南 URL}

**注意：** 如果未预安装设备代码，请选择下面的[选项](#preparethedevice)来启用即插即用设备。

<a name="preparethedevice"></a>
# <a name="prepare-the-device"></a>准备设备。

**硬件环境设置**

-   请包括设备的设置和连接方法。 包括硬件设置所需的任何软件的外部链接

**软件环境设置**

-   请包括设置设备所需满足的先决条件。 请尽量使用指向自己页面（包含设备准备步骤）的外部链接。

### <a name="option-1"></a>选项 1

-   如果设备上未预安装设备代码，请提供存储库的 URL。

-   指定有关如何在设备上刷新映像的步骤，并提供下载可刷新映像和必要工具所需的 URL。 请添加必要的屏幕截图。 

### <a name="option-2"></a>方法 2

-   对于使用 Microsoft PnP SDK 示例的合作伙伴

-   如果不需要重新编译代码，请在此处提供配置文件，使之能够复制到 C sdk 环境中，以便在设备上启用“即插即用”

-   请包含有关如何编译代码以及进行编译所需的工具和环境的说明等信息。请添加必要的屏幕截图 

### <a name="option-3"></a>选项 3

-   如果需要重新编译，请提供可供任何人修改的 GitHub 存储库的链接。

-   请包含有关如何编译代码以及进行编译所需的工具和环境的说明等信息。请添加必要的屏幕截图 

<a name="IntegrationwithIoTCentral"></a>
# <a name="integration-with-iot-central"></a>与 IoT Central 集成

-   包括有关如何将设备连接到 IoT Central 的步骤
-   包括分步过程，用于介绍设备如何使用 DPS 配置（ID 作用域、SAS 密钥、设备 ID、注册 ID）预配到 IoT Central。
-   包括屏幕截图和注释，用于说明 IoT Central 如何显示/可视化来自 PnP 设备的遥测数据。
-   将此[入门]( https://aka.ms/AA66he8)文档用作示例

<a name="AdditionalLinks"></a>
# <a name="additional-links"></a>其他链接

若要进一步了解“即插即用”，请参阅下面的链接 

-    [博客](https://azure.microsoft.com/en-us/blog/iot-plug-and-play-is-now-available-in-preview/)
-    [常见问题](TBD) 
-    [即插即用 C SDK](https://github.com/Azure/azure-iot-sdk-c/tree/public-preview) 
-    [即插即用 Node SDK](https://github.com/Azure/azure-iot-sdk-node/tree/digitaltwins-preview)
-    [即插即用定义](https://github.com/Azure/IoTPlugandPlay)

