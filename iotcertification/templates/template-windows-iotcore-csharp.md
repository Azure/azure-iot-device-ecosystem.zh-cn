---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: csharp
ms.openlocfilehash: b8a8cf615825c6dd8263a67b29d2bd25deb3013d
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62439608"
---
<a name="run-a-simple-csharp-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="451eb-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 Csharp 示例</span><span class="sxs-lookup"><span data-stu-id="451eb-101">Run a simple Csharp sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="451eb-102">目录</span><span class="sxs-lookup"><span data-stu-id="451eb-102">Table of Contents</span></span>

-   [<span data-ttu-id="451eb-103">介绍</span><span class="sxs-lookup"><span data-stu-id="451eb-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="451eb-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="451eb-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="451eb-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="451eb-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="451eb-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="451eb-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="451eb-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="451eb-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="451eb-108">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="451eb-108">Instructions for using this template</span></span>

-   <span data-ttu-id="451eb-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="451eb-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="451eb-110">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="451eb-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="451eb-111">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="451eb-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="451eb-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="451eb-112">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="451eb-113">介绍</span><span class="sxs-lookup"><span data-stu-id="451eb-113">Introduction</span></span>

<span data-ttu-id="451eb-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="451eb-114">**About this document**</span></span>

<span data-ttu-id="451eb-115">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="451eb-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="451eb-116">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="451eb-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="451eb-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="451eb-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="451eb-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="451eb-118">Registering your IoT device</span></span>
-   <span data-ttu-id="451eb-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="451eb-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="451eb-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="451eb-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="451eb-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="451eb-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="451eb-122">准备好一台装有 Git 客户端并且可以访问 [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="451eb-122">Computer with Git client installed and access to the [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub public repository.</span></span>
-   <span data-ttu-id="451eb-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="451eb-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="451eb-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="451eb-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="451eb-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="451eb-125">{enter your device name here} device.</span></span>

#### <a name="install-visual-studio-2015-and-tools"></a><span data-ttu-id="451eb-126">安装 Visual Studio 2015 和工具</span><span class="sxs-lookup"><span data-stu-id="451eb-126">Install Visual Studio 2015 and Tools</span></span>

-   <span data-ttu-id="451eb-127">若要创建 Windows IoT Core 解决方案，需安装 [Visual Studio 2015](https://www.visualstudio.com/en-us/products/vs-2015-product-editions.aspx)。</span><span class="sxs-lookup"><span data-stu-id="451eb-127">To create Windows IoT Core solutions, you will need to install [Visual Studio 2015](https://www.visualstudio.com/en-us/products/vs-2015-product-editions.aspx).</span></span> <span data-ttu-id="451eb-128">可以安装任何版本的 Visual Studio，包括免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="451eb-128">You can install any edition of Visual Studio, including the free Community edition.</span></span>

    <span data-ttu-id="451eb-129">请务必选择“通用 Windows 应用开发工具”，这是编写 Windows 10 应用时必须使用的组件： </span><span class="sxs-lookup"><span data-stu-id="451eb-129">Make sure to select the **Universal Windows App Development Tools**, the component required for writing apps Windows 10:</span></span>

-   <span data-ttu-id="451eb-130">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="451eb-130">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="451eb-131">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="451eb-131">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="451eb-132">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="451eb-132">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="451eb-133">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="451eb-133">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="451eb-134">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="451eb-134">Step 3: Build and Run the Sample</span></span>

<a name="Step_3_1:_Connect"/>
## <a name="31-connect-the-device"></a><span data-ttu-id="451eb-135">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="451eb-135">3.1 Connect the Device</span></span>

-   <span data-ttu-id="451eb-136">使用以太网电缆将开发板连接到网络。</span><span class="sxs-lookup"><span data-stu-id="451eb-136">Connect the board to your network using an Ethernet cable.</span></span> <span data-ttu-id="451eb-137">由于示例依赖于 Internet 访问，因此必须执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="451eb-137">This step is required, as the sample depends on internet access.</span></span>

-   <span data-ttu-id="451eb-138">使用 micro-USB 电缆将设备插入计算机。</span><span class="sxs-lookup"><span data-stu-id="451eb-138">Plug the device into your computer using a micro-USB cable.</span></span>

<a name="Step_3_2:_Build"/>
## <a name="32--build-the-samples"></a><span data-ttu-id="451eb-139">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="451eb-139">3.2  Build the Samples</span></span>

-   <span data-ttu-id="451eb-140">启动 Visual Studio 2015 的新实例。</span><span class="sxs-lookup"><span data-stu-id="451eb-140">Start a new instance of Visual Studio 2015.</span></span> <span data-ttu-id="451eb-141">打开存储库本地副本中的 **iothub_csharp_client.sln** 解决方案 (/azure-iot-sdk-csharp)。</span><span class="sxs-lookup"><span data-stu-id="451eb-141">Open the **iothub_csharp_client.sln** solution (/azure-iot-sdk-csharp) from your local copy of the repository.</span></span>

-   <span data-ttu-id="451eb-142">在 Visual Studio 的“解决方案资源管理器”中，导航到 **UWPSample(Universal Windows)** 项目。 </span><span class="sxs-lookup"><span data-stu-id="451eb-142">In Visual Studio, from **Solution Explorer**, navigate to the **UWPSample(Universal Windows)** project.</span></span>

-   <span data-ttu-id="451eb-143">在 **ConnectionStrings.cs** 文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="451eb-143">Locate the following code in the **ConnectionStrings.cs** file:</span></span>

        public const string DeviceConnectionString = "<replace>";

-   <span data-ttu-id="451eb-144">将上述占位符替换为在[步骤 1](#Prerequisites) 中获取的设备连接字符串，然后保存更改。</span><span class="sxs-lookup"><span data-stu-id="451eb-144">Replace the above placeholder with device connection string you obtained in [Step 1](#Prerequisites) and save the changes.</span></span>

-   <span data-ttu-id="451eb-145">选择适当的体系结构（x86 或 ARM，具体取决于设备），将调试方法设置为“远程计算机”：</span><span class="sxs-lookup"><span data-stu-id="451eb-145">Choose the right architecture (x86 or ARM, depending on your device) and set the debugging method to "Remote Machine":</span></span>
    
-   <span data-ttu-id="451eb-146">若要在设备上部署二进制文件，请在“解决方案资源管理器”中右键单击 UWPSample 项目，选择“属性”，然后导航到“调试”选项卡：   </span><span class="sxs-lookup"><span data-stu-id="451eb-146">To deploy the binaries on your device, right-click on the UWPSample project in the **Solution Explorer**, select **Properties** and navigate to the **Debug** tab:</span></span>

    <span data-ttu-id="451eb-147">键入设备的名称。</span><span class="sxs-lookup"><span data-stu-id="451eb-147">Type in the name of your device.</span></span> <span data-ttu-id="451eb-148">确保“使用身份验证”框处于未选中状态。</span><span class="sxs-lookup"><span data-stu-id="451eb-148">Make sure the "Use authentication" box is unchecked.</span></span>

-   <span data-ttu-id="451eb-149">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="451eb-149">Build the solution.</span></span>

<a name="Step_3_3:_Run"/>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="451eb-150">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="451eb-150">3.3 Run and Validate the Samples</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="451eb-151">3.3.1：向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="451eb-151">3.3.1 Send Device Events to IoT Hub</span></span>

-   <span data-ttu-id="451eb-152">在 Visual Studio 的“解决方案资源管理器”中右键单击“UWPSample(Universal Windows)”项目，然后单击“调试”  “启动新实例”生成并运行示例。  **&minus;&gt;**</span><span class="sxs-lookup"><span data-stu-id="451eb-152">In Visual Studio, from **Solution Explorer**, right-click the **UWPSample(Universal Windows)** project, click **Debug &minus;&gt; Start new instance** to build and run the sample.</span></span> 

-   <span data-ttu-id="451eb-153">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="451eb-153">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="451eb-154">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="451eb-154">3.3.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="451eb-155">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="451eb-155">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="451eb-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="451eb-156">Next Steps</span></span>

<span data-ttu-id="451eb-157">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="451eb-157">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="451eb-158">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="451eb-158">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="451eb-159">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="451eb-159">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="451eb-160">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="451eb-160">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="451eb-161">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="451eb-161">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="451eb-162">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="451eb-162">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="451eb-163">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="451eb-163">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="451eb-164">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="451eb-164">[Remote monitoring and notifications with Logic Apps]</span></span>   

[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

