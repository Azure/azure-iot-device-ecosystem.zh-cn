---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: csharp
ms.openlocfilehash: e045a56e6a77226fa0f03353874acdf3d5e7f11e
ms.sourcegitcommit: dab4a191b1927a60143b2b0449b533d716b309e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
ms.locfileid: "31437972"
---
<a name="run-a-simple-csharp-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="2d922-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 Csharp 示例</span><span class="sxs-lookup"><span data-stu-id="2d922-101">Run a simple Csharp sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="2d922-102">目录</span><span class="sxs-lookup"><span data-stu-id="2d922-102">Table of Contents</span></span>

-   [<span data-ttu-id="2d922-103">介绍</span><span class="sxs-lookup"><span data-stu-id="2d922-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="2d922-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="2d922-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="2d922-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="2d922-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="2d922-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="2d922-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="2d922-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2d922-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="2d922-108">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="2d922-108">Instructions for using this template</span></span>

-   <span data-ttu-id="2d922-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="2d922-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="2d922-110">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="2d922-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="2d922-111">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="2d922-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="2d922-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="2d922-112">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="2d922-113">介绍</span><span class="sxs-lookup"><span data-stu-id="2d922-113">Introduction</span></span>

<span data-ttu-id="2d922-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="2d922-114">**About this document**</span></span>

<span data-ttu-id="2d922-115">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="2d922-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="2d922-116">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="2d922-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="2d922-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2d922-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="2d922-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="2d922-118">Registering your IoT device</span></span>
-   <span data-ttu-id="2d922-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="2d922-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="2d922-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="2d922-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="2d922-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="2d922-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="2d922-122">[准备开发环境][setup-devbox-windows]</span><span class="sxs-lookup"><span data-stu-id="2d922-122">[Prepare your development environment][setup-devbox-windows]</span></span>
-   <span data-ttu-id="2d922-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="2d922-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="2d922-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="2d922-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="2d922-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="2d922-125">{enter your device name here} device.</span></span>
-   <span data-ttu-id="2d922-126">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="2d922-126">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="2d922-127">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="2d922-127">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="2d922-128">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="2d922-128">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="2d922-129">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="2d922-129">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="2d922-130">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="2d922-130">Step 3: Build and Run the sample</span></span>

-   <span data-ttu-id="2d922-131">下载 [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp) 和示例程序，并将其保存到本地存储库。</span><span class="sxs-lookup"><span data-stu-id="2d922-131">Download the [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp) and the sample programs and save them to your local repository.</span></span>
-   <span data-ttu-id="2d922-132">打开设备控制台（命令提示符或 PowerShell 窗口），并切换到本地 SDK 的 **azure-iot-sdk-csharp** 目录。</span><span class="sxs-lookup"><span data-stu-id="2d922-132">Open a device console (command prompt or a powershell window) and change to your local SDK **azure-iot-sdk-csharp** directory.</span></span>

-  <span data-ttu-id="2d922-133">在设备上以环境变量的形式添加 IoT 中心设备连接字符串：</span><span class="sxs-lookup"><span data-stu-id="2d922-133">Add the Iot Hub device connection string on your device as an environment variable:</span></span>

        setx IOTHUB_DEVICE_CONN_STRING <yourDeviceConnectionString>

-  <span data-ttu-id="2d922-134">运行以下命令生成 SDK：</span><span class="sxs-lookup"><span data-stu-id="2d922-134">Run the following command to build the SDK:</span></span>

        build.cmd -config Release
        
- <span data-ttu-id="2d922-135">在设备控制台中，使用以下命令运行示例：</span><span class="sxs-lookup"><span data-stu-id="2d922-135">From the device console, run the sample using following command:</span></span>

    <span data-ttu-id="2d922-136">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2d922-136">**If HTTP protocol:**</span></span>

        cd iothub\device\samples\DeviceClientHttpSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientHttpSample.dll

    <span data-ttu-id="2d922-137">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2d922-137">**If MQTT protocol:**</span></span>

        cd iothub\device\samples\DeviceClientMqttSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientMqttSample.dll
        
    <span data-ttu-id="2d922-138">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2d922-138">**If AMQP protocol:**</span></span>

        cd iothub\device\samples\DeviceClientAmqpSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientAmqpSample.dll

-   <span data-ttu-id="2d922-139">使用 **DeviceExplorer** 实用工具观察 IoT 中心从**设备客户端示例**应用程序收到的消息。</span><span class="sxs-lookup"><span data-stu-id="2d922-139">Use the **DeviceExplorer** utility to observe the messages IoT Hub receives from the **Device Client Sample** application.</span></span>
-   <span data-ttu-id="2d922-140">参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“监视设备到云的事件”，查看设备正在发送的数据。</span><span class="sxs-lookup"><span data-stu-id="2d922-140">Refer "Monitor device-to-cloud events" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to see the data your device is sending.</span></span>
-   <span data-ttu-id="2d922-141">参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“发送云到设备的消息”，获取有关向设备发送消息的说明。</span><span class="sxs-lookup"><span data-stu-id="2d922-141">Refer "Send cloud-to-device messages" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) for instructions on sending messages to device.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="2d922-142">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2d922-142">Next Steps</span></span>

<span data-ttu-id="2d922-143">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="2d922-143">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="2d922-144">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="2d922-144">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="2d922-145">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="2d922-145">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="2d922-146">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="2d922-146">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="2d922-147">[使用 Power BI 可视化 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="2d922-147">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="2d922-148">[使用 Azure Web 应用可视化 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="2d922-148">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="2d922-149">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="2d922-149">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="2d922-150">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="2d922-150">[Remote monitoring and notifications with Logic Apps]</span></span>   

[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[使用 Power BI 可视化 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[使用 Azure Web 应用可视化 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
