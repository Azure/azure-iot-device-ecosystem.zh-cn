---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: c
ms.openlocfilehash: 0fe4529fc57ff96cb0a4bb513c9a08df3e2b8609
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62439589"
---
<a name="run-a-simple-c-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="71e79-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C 示例</span><span class="sxs-lookup"><span data-stu-id="71e79-101">Run a simple C sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="71e79-102">目录</span><span class="sxs-lookup"><span data-stu-id="71e79-102">Table of Contents</span></span>

-   [<span data-ttu-id="71e79-103">介绍</span><span class="sxs-lookup"><span data-stu-id="71e79-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="71e79-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="71e79-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="71e79-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="71e79-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="71e79-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="71e79-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="71e79-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="71e79-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="71e79-108">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="71e79-108">Instructions for using this template</span></span>

-   <span data-ttu-id="71e79-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="71e79-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="71e79-110">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="71e79-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="71e79-111">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="71e79-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="71e79-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="71e79-112">Remove this section from final document.</span></span>

<a name="Introduction"/>
# <a name="introduction"></a><span data-ttu-id="71e79-113">介绍</span><span class="sxs-lookup"><span data-stu-id="71e79-113">Introduction</span></span>

<span data-ttu-id="71e79-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="71e79-114">**About this document**</span></span>

<span data-ttu-id="71e79-115">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="71e79-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="71e79-116">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="71e79-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="71e79-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="71e79-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="71e79-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="71e79-118">Registering your IoT device</span></span>
-   <span data-ttu-id="71e79-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="71e79-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="71e79-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="71e79-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="71e79-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="71e79-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="71e79-122">[准备开发环境][setup-devbox-windows]</span><span class="sxs-lookup"><span data-stu-id="71e79-122">[Prepare your development environment][setup-devbox-windows]</span></span>
-   <span data-ttu-id="71e79-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="71e79-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="71e79-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="71e79-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="71e79-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="71e79-125">{enter your device name here} device.</span></span>
-   <span data-ttu-id="71e79-126">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="71e79-126">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="71e79-127">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="71e79-127">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="71e79-128">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="71e79-128">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="71e79-129">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="71e79-129">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-sdk-and-run-the-sample"></a><span data-ttu-id="71e79-130">步骤 3：生成 SDK 并运行示例</span><span class="sxs-lookup"><span data-stu-id="71e79-130">Step 3: Build SDK and Run the sample</span></span>

-   <span data-ttu-id="71e79-131">启动 Visual Studio 2015 的新实例。</span><span class="sxs-lookup"><span data-stu-id="71e79-131">Start a new instance of Visual Studio 2015.</span></span> <span data-ttu-id="71e79-132">打开主目录中 **cmake** 文件夹内的 **azure_iot_sdks.sln** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="71e79-132">Open the **azure_iot_sdks.sln** solution in the **cmake** folder in your home directory.</span></span>

-   <span data-ttu-id="71e79-133">在 Visual Studio 的“解决方案资源管理器”中，导航到“simplesample_amqp”项目并打开“simplesample_amqp.c”文件。   </span><span class="sxs-lookup"><span data-stu-id="71e79-133">In Visual Studio, in **Solution Explorer**, navigate to **simplesample_amqp** project, open the **simplesample_amqp.c** file.</span></span>

-   <span data-ttu-id="71e79-134">在该文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="71e79-134">Locate the following code in the file:</span></span>

        static const char* connectionString = "[device connection string]";

-   <span data-ttu-id="71e79-135">将上述占位符替换为在[步骤 1](#Prerequisites) 中获取的设备连接字符串，然后保存更改。</span><span class="sxs-lookup"><span data-stu-id="71e79-135">Replace the above placeholder with device connection string you obtained in [Step 1](#Prerequisites) and save the changes.</span></span>

-   <span data-ttu-id="71e79-136">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="71e79-136">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

-   <span data-ttu-id="71e79-137">在“解决方案资源管理器”中右键单击“simplesample_amqp”项目，单击“调试”，然后单击“启动新实例”生成并运行示例。    </span><span class="sxs-lookup"><span data-stu-id="71e79-137">In **Solution Explorer**, right-click the **simplesample_amqp** project, click **Debug**, and then click **Start new instance** to build and run the sample.</span></span> <span data-ttu-id="71e79-138">当应用程序向 IoT 中心发送设备到云的消息时，控制台会显示消息。</span><span class="sxs-lookup"><span data-stu-id="71e79-138">The console displays messages as the application sends device-to-cloud messages to IoT Hub.</span></span>

-   <span data-ttu-id="71e79-139">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="71e79-139">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="71e79-140">后续步骤</span><span class="sxs-lookup"><span data-stu-id="71e79-140">Next Steps</span></span>

<span data-ttu-id="71e79-141">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="71e79-141">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="71e79-142">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="71e79-142">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="71e79-143">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="71e79-143">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="71e79-144">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="71e79-144">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="71e79-145">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="71e79-145">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="71e79-146">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="71e79-146">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="71e79-147">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="71e79-147">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="71e79-148">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="71e79-148">[Remote monitoring and notifications with Logic Apps]</span></span>   

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
[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

