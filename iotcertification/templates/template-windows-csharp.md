---
platform: 
device: 
language: csharp
ms.openlocfilehash: 4d15e85b2fa807fbe152a6eff6427c7f7572352a
ms.sourcegitcommit: 4b98ebc1c3cad79b3f19f21d36add53daa71e0b5
ms.translationtype: HT
ms.contentlocale: zh-CN
---
<a name="run-a-simple-csharp-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="b6189-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C# 示例</span><span class="sxs-lookup"><span data-stu-id="b6189-101">Run a simple Csharp sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="b6189-102">目录</span><span class="sxs-lookup"><span data-stu-id="b6189-102">Table of Contents</span></span>

-   [<span data-ttu-id="b6189-103">介绍</span><span class="sxs-lookup"><span data-stu-id="b6189-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="b6189-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="b6189-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="b6189-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="b6189-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="b6189-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="b6189-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="b6189-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b6189-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="b6189-108">此模板的用法说明</span><span class="sxs-lookup"><span data-stu-id="b6189-108">Instructions for using this template</span></span>

-   <span data-ttu-id="b6189-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="b6189-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="b6189-110">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="b6189-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="b6189-111">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="b6189-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="b6189-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="b6189-112">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="b6189-113">介绍</span><span class="sxs-lookup"><span data-stu-id="b6189-113">Introduction</span></span>

<span data-ttu-id="b6189-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="b6189-114">**About this document**</span></span>

<span data-ttu-id="b6189-115">本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="b6189-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="b6189-116">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="b6189-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="b6189-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="b6189-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="b6189-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="b6189-118">Registering your IoT device</span></span>
-   <span data-ttu-id="b6189-119">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="b6189-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="b6189-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="b6189-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="b6189-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="b6189-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="b6189-122">[准备开发环境][setup-devbox-windows]</span><span class="sxs-lookup"><span data-stu-id="b6189-122">[Prepare your development environment][setup-devbox-windows]</span></span>
-   <span data-ttu-id="b6189-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="b6189-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="b6189-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="b6189-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="b6189-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="b6189-125">{enter your device name here} device.</span></span>
-   <span data-ttu-id="b6189-126">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="b6189-126">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="b6189-127">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="b6189-127">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="b6189-128">{{记下安装、配置和连接设备时需要遵循的说明。</span><span class="sxs-lookup"><span data-stu-id="b6189-128">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="b6189-129">请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}</span><span class="sxs-lookup"><span data-stu-id="b6189-129">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="b6189-130">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="b6189-130">Step 3: Build and Run the sample</span></span>

-   <span data-ttu-id="b6189-131">下载 [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp) 和示例程序，并将其保存到本地存储库。</span><span class="sxs-lookup"><span data-stu-id="b6189-131">Download the [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp) and the sample programs and save them to your local repository.</span></span>
-   <span data-ttu-id="b6189-132">启动 Visual Studio 2015 的新实例。</span><span class="sxs-lookup"><span data-stu-id="b6189-132">Start a new instance of Visual Studio 2015.</span></span>
-   <span data-ttu-id="b6189-133">打开存储库本地副本中的 `device` 文件夹内的 **iothub_csharp_client.sln** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="b6189-133">Open the **iothub_csharp_client.sln** solution in the `device` folder in your local copy of the repository.</span></span>
-   <span data-ttu-id="b6189-134">在 Visual Studio 的“解决方案资源管理器”中，导航到 **samples** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6189-134">In Visual Studio, from Solution Explorer, navigate to the **samples** folder.</span></span>
-   <span data-ttu-id="b6189-135">在 **DeviceClientAmqpSample** 项目中打开 ***Program.cs*** 文件。</span><span class="sxs-lookup"><span data-stu-id="b6189-135">In the **DeviceClientAmqpSample** project, open the ***Program.cs*** file.</span></span>
-   <span data-ttu-id="b6189-136">在该文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="b6189-136">Locate the following code in the file:</span></span>

        private const string DeviceConnectionString = "<replace>";
        
-   <span data-ttu-id="b6189-137">将 `<replace>` 替换为设备的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="b6189-137">Replace `<replace>` with the connection string for your device.</span></span>
-   <span data-ttu-id="b6189-138">在“解决方案资源管理器”中右键单击“DeviceClientAmqpSample”项目，单击“调试”，然后单击“启动新实例”生成并运行示例。</span><span class="sxs-lookup"><span data-stu-id="b6189-138">In **Solution Explorer**, right-click the **DeviceClientAmqpSample** project, click **Debug**, and then click **Start new instance** to build and run the sample.</span></span> <span data-ttu-id="b6189-139">当应用程序向 IoT 中心发送设备到云的消息时，控制台会显示消息。</span><span class="sxs-lookup"><span data-stu-id="b6189-139">The console displays messages as the application sends device-to-cloud messages to IoT Hub.</span></span>
-   <span data-ttu-id="b6189-140">使用 **DeviceExplorer** 实用工具来监视 IoT 中心从**设备客户端 AMQP 示例**应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="b6189-140">Use the **DeviceExplorer** utility to observe the messages IoT Hub receives from the **Device Client AMQP Sample** application.</span></span>
-   <span data-ttu-id="b6189-141">参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“监视设备到云的事件”，确定设备是否正在发送数据。</span><span class="sxs-lookup"><span data-stu-id="b6189-141">Refer "Monitor device-to-cloud events" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to see the data your device is sending.</span></span>
-   <span data-ttu-id="b6189-142">参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“发送云到设备的消息”，获取有关向设备发送消息的说明。</span><span class="sxs-lookup"><span data-stu-id="b6189-142">Refer "Send cloud-to-device messages" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) for instructions on sending messages to device.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="b6189-143">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b6189-143">Next Steps</span></span>

<span data-ttu-id="b6189-144">现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="b6189-144">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="b6189-145">若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="b6189-145">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="b6189-146">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="b6189-146">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="b6189-147">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="b6189-147">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="b6189-148">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="b6189-148">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="b6189-149">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="b6189-149">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="b6189-150">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="b6189-150">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="b6189-151">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="b6189-151">[Remote monitoring and notifications with Logic Apps]</span></span>   

<span data-ttu-id="b6189-152">[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging</span><span class="sxs-lookup"><span data-stu-id="b6189-152">[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging</span></span>
<span data-ttu-id="b6189-153">[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage</span><span class="sxs-lookup"><span data-stu-id="b6189-153">[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage</span></span>
<span data-ttu-id="b6189-154">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi</span><span class="sxs-lookup"><span data-stu-id="b6189-154">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi</span></span>
<span data-ttu-id="b6189-155">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps</span><span class="sxs-lookup"><span data-stu-id="b6189-155">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps</span></span>
<span data-ttu-id="b6189-156">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning</span><span class="sxs-lookup"><span data-stu-id="b6189-156">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning</span></span>
<span data-ttu-id="b6189-157">[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps</span><span class="sxs-lookup"><span data-stu-id="b6189-157">[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps</span></span>
[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

