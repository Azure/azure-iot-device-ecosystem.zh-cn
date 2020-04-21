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
<a name="connect-enter-your-device-name-here-device-to-your-azure-iot-central-application"></a><span data-ttu-id="0e644-101">将 {在此处输入设备名称} 设备连接到 Azure IoT Central 应用程序</span><span class="sxs-lookup"><span data-stu-id="0e644-101">Connect {enter your device name here} device to your Azure IoT Central Application</span></span>
===

---
# <a name="table-of-contents"></a><span data-ttu-id="0e644-102">目录</span><span class="sxs-lookup"><span data-stu-id="0e644-102">Table of Contents</span></span>

-   [<span data-ttu-id="0e644-103">简介</span><span class="sxs-lookup"><span data-stu-id="0e644-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="0e644-104">先决条件</span><span class="sxs-lookup"><span data-stu-id="0e644-104">Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="0e644-105">创建 Azure IoT Central 应用程序</span><span class="sxs-lookup"><span data-stu-id="0e644-105">Create Azure IoT Central application</span></span>](#Create_AICA)
-   [<span data-ttu-id="0e644-106">设备连接详细信息</span><span class="sxs-lookup"><span data-stu-id="0e644-106">Device Connection Details</span></span>](#DeviceConnectionDetails)
-   [<span data-ttu-id="0e644-107">准备设备</span><span class="sxs-lookup"><span data-stu-id="0e644-107">Prepare the Device</span></span>](#preparethedevice)
-   [<span data-ttu-id="0e644-108">与 IoT Central 集成</span><span class="sxs-lookup"><span data-stu-id="0e644-108">Integration with IoT Central</span></span>](#IntegrationwithIoTCentral)
-   [<span data-ttu-id="0e644-109">其他链接</span><span class="sxs-lookup"><span data-stu-id="0e644-109">Additional Links</span></span>](#AdditionalLinks)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="0e644-110">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="0e644-110">Instructions for using this template</span></span>

-   <span data-ttu-id="0e644-111">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="0e644-111">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="0e644-112">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="0e644-112">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="0e644-113">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="0e644-113">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="0e644-114">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="0e644-114">Remove this section from final document.</span></span>

<a name="Introduction"></a>

# <a name="introduction"></a><span data-ttu-id="0e644-115">介绍</span><span class="sxs-lookup"><span data-stu-id="0e644-115">Introduction</span></span> 

<span data-ttu-id="0e644-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="0e644-116">**About this document**</span></span>

<span data-ttu-id="0e644-117">本文档介绍如何使用“IoT 即插即用”模型将 {在此处输入设备名称} 连接到 Azure IoT Central 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0e644-117">This document describes how to connect {enter your device name here} to Azure IoT Central application using the IoT plug and Play model.</span></span> <span data-ttu-id="0e644-118">“即插即用”使解决方案开发人员可以在不编写任何设备代码的情况下集成设备，从而简化了 IoT。</span><span class="sxs-lookup"><span data-stu-id="0e644-118">Plug and Play simplifies IoT by allowing solution developers to integrate devices without writing any device code.</span></span> <span data-ttu-id="0e644-119">使用“即插即用”，设备制造商将向云开发人员提供其设备的模型，使设备可以快速集成到 IoT Central 或在 Azure IoT 平台上构建的任何解决方案。</span><span class="sxs-lookup"><span data-stu-id="0e644-119">Using Plug and Play, device manufacturers will provide a model of their device to cloud developers to be integrated quickly into IoT Central or any solution built on the Azure IoT platform.</span></span> <span data-ttu-id="0e644-120">“IoT 即插即用”将以定义语言和 SDK 的方式开放给社区。</span><span class="sxs-lookup"><span data-stu-id="0e644-120">IoT Plug and Play will be open to the community by way of a definition language and SDKs.</span></span>

<span data-ttu-id="0e644-121">{请在此处提供设备的简介和功能}</span><span class="sxs-lookup"><span data-stu-id="0e644-121">{Please provide introduction and features of your device here}</span></span>

<a name="Prerequisites"></a>
# <a name="prerequisites"></a><span data-ttu-id="0e644-122">先决条件</span><span class="sxs-lookup"><span data-stu-id="0e644-122">Prerequisites</span></span>

<span data-ttu-id="0e644-123">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="0e644-123">You should have the following items ready before beginning the process:</span></span> 

-   [<span data-ttu-id="0e644-124">Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="0e644-124">Azure Account</span></span>](https://portal.azure.com)
-   [<span data-ttu-id="0e644-125">Azure IoT 中心实例</span><span class="sxs-lookup"><span data-stu-id="0e644-125">Azure IoT Hub Instance</span></span>](https://docs.microsoft.com/en-us/azure/iot-hub/about-iot-hub)
-   [<span data-ttu-id="0e644-126">Azure IoT 中心设备预配服务</span><span class="sxs-lookup"><span data-stu-id="0e644-126">Azure IoT Hub Device Provisioning Service</span></span>](https://docs.microsoft.com/en-us/azure/iot-dps/about-iot-dps)
-   <span data-ttu-id="0e644-127">提供设备支持的网络连接（WiFi、LAN）</span><span class="sxs-lookup"><span data-stu-id="0e644-127">Provide Network connectivity (Wifi, LAN) supported by the device</span></span>
-   <span data-ttu-id="0e644-128">若要启用“即插即用”，必须在设备中预安装设备代码/软件映像</span><span class="sxs-lookup"><span data-stu-id="0e644-128">Its mandatory that the device code/software image is preinstalled in device to enable Plug and Play</span></span>
-   <span data-ttu-id="0e644-129">{请在此处提供开发环境安装指南 URL}</span><span class="sxs-lookup"><span data-stu-id="0e644-129">{Provide URL here to setup guide of development environment}</span></span>

<span data-ttu-id="0e644-130">**注意：** 如果未预安装设备代码，请选择下面的[选项](#preparethedevice)来启用即插即用设备。</span><span class="sxs-lookup"><span data-stu-id="0e644-130">**Note:** If the device code is not preinstalled following are the [options](#preparethedevice) to choose to enable the plug and play device.</span></span>

<a name="preparethedevice"></a>
# <a name="prepare-the-device"></a><span data-ttu-id="0e644-131">准备设备。</span><span class="sxs-lookup"><span data-stu-id="0e644-131">Prepare the Device.</span></span>

<span data-ttu-id="0e644-132">**硬件环境设置**</span><span class="sxs-lookup"><span data-stu-id="0e644-132">**Hardware Environmental setup**</span></span>

-   <span data-ttu-id="0e644-133">请包括设备的设置和连接方法。</span><span class="sxs-lookup"><span data-stu-id="0e644-133">Please include how to setup and connect the device.</span></span> <span data-ttu-id="0e644-134">包括硬件设置所需的任何软件的外部链接</span><span class="sxs-lookup"><span data-stu-id="0e644-134">Include external links for any software required for Hardware setup</span></span>

<span data-ttu-id="0e644-135">**软件环境设置**</span><span class="sxs-lookup"><span data-stu-id="0e644-135">**Software Environmental Setup**</span></span>

-   <span data-ttu-id="0e644-136">请包括设置设备所需满足的先决条件。</span><span class="sxs-lookup"><span data-stu-id="0e644-136">Please include the prerequisite required to setup the device.</span></span> <span data-ttu-id="0e644-137">请尽量使用指向自己页面（包含设备准备步骤）的外部链接。</span><span class="sxs-lookup"><span data-stu-id="0e644-137">Please use external links when possible pointing to your own page with device preparation steps.</span></span>

### <a name="option-1"></a><span data-ttu-id="0e644-138">选项 1</span><span class="sxs-lookup"><span data-stu-id="0e644-138">Option 1</span></span>

-   <span data-ttu-id="0e644-139">如果设备上未预安装设备代码，请提供存储库的 URL。</span><span class="sxs-lookup"><span data-stu-id="0e644-139">If device code not pre-installed on your device, please provide us the URL of your repository.</span></span>

-   <span data-ttu-id="0e644-140">指定有关如何在设备上刷新映像的步骤，并提供下载可刷新映像和必要工具所需的 URL。</span><span class="sxs-lookup"><span data-stu-id="0e644-140">Specify the steps on how to flash the image on device and provide required URL's to download the flash-able image and necessary tools.</span></span> <span data-ttu-id="0e644-141">请添加必要的屏幕截图。 </span><span class="sxs-lookup"><span data-stu-id="0e644-141">**Please add the screenshots where ever necessary.**</span></span>

### <a name="option-2"></a><span data-ttu-id="0e644-142">方法 2</span><span class="sxs-lookup"><span data-stu-id="0e644-142">Option 2</span></span>

-   <span data-ttu-id="0e644-143">对于使用 Microsoft PnP SDK 示例的合作伙伴</span><span class="sxs-lookup"><span data-stu-id="0e644-143">For the partners using the Microsoft PnP SDK samples</span></span>

-   <span data-ttu-id="0e644-144">如果不需要重新编译代码，请在此处提供配置文件，使之能够复制到 C sdk 环境中，以便在设备上启用“即插即用”</span><span class="sxs-lookup"><span data-stu-id="0e644-144">If recompilation of code is not required, please provide config file here, such that it can be copied in the C sdk environment to enable Plug and Play on device</span></span>

-   <span data-ttu-id="0e644-145">请包含有关如何编译代码以及进行编译所需的工具和环境的说明等信息。请添加必要的屏幕截图 </span><span class="sxs-lookup"><span data-stu-id="0e644-145">Please include instruction on how to compile the code, tools and environment required to compile etc. **Please add the screenshots where ever necessary**</span></span>

### <a name="option-3"></a><span data-ttu-id="0e644-146">选项 3</span><span class="sxs-lookup"><span data-stu-id="0e644-146">Option 3</span></span>

-   <span data-ttu-id="0e644-147">如果需要重新编译，请提供可供任何人修改的 GitHub 存储库的链接。</span><span class="sxs-lookup"><span data-stu-id="0e644-147">If recompilation is required, then please provide the link for GitHub repo for anyone to modify.</span></span>

-   <span data-ttu-id="0e644-148">请包含有关如何编译代码以及进行编译所需的工具和环境的说明等信息。请添加必要的屏幕截图 </span><span class="sxs-lookup"><span data-stu-id="0e644-148">Please include instruction on how to compile the code , tools and environment required to compile etc. **Please add the screenshots where ever necessary**</span></span>

<a name="IntegrationwithIoTCentral"></a>
# <a name="integration-with-iot-central"></a><span data-ttu-id="0e644-149">与 IoT Central 集成</span><span class="sxs-lookup"><span data-stu-id="0e644-149">Integration with IoT Central</span></span>

-   <span data-ttu-id="0e644-150">包括有关如何将设备连接到 IoT Central 的步骤</span><span class="sxs-lookup"><span data-stu-id="0e644-150">Include the steps on how to connect the Device to IoT Central</span></span>
-   <span data-ttu-id="0e644-151">包括分步过程，用于介绍设备如何使用 DPS 配置（ID 作用域、SAS 密钥、设备 ID、注册 ID）预配到 IoT Central。</span><span class="sxs-lookup"><span data-stu-id="0e644-151">Include the steps by step process on how the devices use the DPS configuration (ID Scope, SAS Key, Device ID, Registration ID) to provision to IoT Central.</span></span>
-   <span data-ttu-id="0e644-152">包括屏幕截图和注释，用于说明 IoT Central 如何显示/可视化来自 PnP 设备的遥测数据。</span><span class="sxs-lookup"><span data-stu-id="0e644-152">Include screenshots and comments on how IoT Central shows/visualize telemetry coming from your PnP device.</span></span>
-   <span data-ttu-id="0e644-153">将此[入门]( https://aka.ms/AA66he8)文档用作示例</span><span class="sxs-lookup"><span data-stu-id="0e644-153">Use this [Get started]( https://aka.ms/AA66he8) doc as an example</span></span>

<a name="AdditionalLinks"></a>
# <a name="additional-links"></a><span data-ttu-id="0e644-154">其他链接</span><span class="sxs-lookup"><span data-stu-id="0e644-154">Additional Links</span></span>

<span data-ttu-id="0e644-155">若要进一步了解“即插即用”，请参阅下面的链接</span><span class="sxs-lookup"><span data-stu-id="0e644-155">Please refer to the below link for additional information for Plug and Play</span></span> 

-    [<span data-ttu-id="0e644-156">博客</span><span class="sxs-lookup"><span data-stu-id="0e644-156">Blog</span></span>](https://azure.microsoft.com/en-us/blog/iot-plug-and-play-is-now-available-in-preview/)
-    [<span data-ttu-id="0e644-157">常见问题</span><span class="sxs-lookup"><span data-stu-id="0e644-157">FAQ</span></span>](TBD) 
-    [<span data-ttu-id="0e644-158">即插即用 C SDK</span><span class="sxs-lookup"><span data-stu-id="0e644-158">Plug and Play C SDK</span></span>](https://github.com/Azure/azure-iot-sdk-c/tree/public-preview) 
-    [<span data-ttu-id="0e644-159">即插即用 Node SDK</span><span class="sxs-lookup"><span data-stu-id="0e644-159">Plug and Play Node SDK</span></span>](https://github.com/Azure/azure-iot-sdk-node/tree/digitaltwins-preview)
-    [<span data-ttu-id="0e644-160">即插即用定义</span><span class="sxs-lookup"><span data-stu-id="0e644-160">Plug and Play Definitions</span></span>](https://github.com/Azure/IoTPlugandPlay)

