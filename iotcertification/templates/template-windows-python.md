---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: python
ms.openlocfilehash: dea357a132d8edf8fd62af37b8363c1492c2f190
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62439613"
---
<a name="run-a-simple-python-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="874e0-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 python 示例</span><span class="sxs-lookup"><span data-stu-id="874e0-101">Run a simple python sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="874e0-102">目录</span><span class="sxs-lookup"><span data-stu-id="874e0-102">Table of Contents</span></span>

-   [<span data-ttu-id="874e0-103">介绍</span><span class="sxs-lookup"><span data-stu-id="874e0-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="874e0-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="874e0-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="874e0-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="874e0-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="874e0-106">步骤 3：设置开发环境</span><span class="sxs-lookup"><span data-stu-id="874e0-106">Step 3: Setup your development environment</span></span>](#Environment)
-   [<span data-ttu-id="874e0-107">步骤 4：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="874e0-107">Step 4: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="874e0-108">后续步骤</span><span class="sxs-lookup"><span data-stu-id="874e0-108">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="874e0-109">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="874e0-109">Instructions for using this template</span></span>

-   <span data-ttu-id="874e0-110">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="874e0-110">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="874e0-111">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="874e0-111">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="874e0-112">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="874e0-112">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="874e0-113">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="874e0-113">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="874e0-114">介绍</span><span class="sxs-lookup"><span data-stu-id="874e0-114">Introduction</span></span>

<span data-ttu-id="874e0-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="874e0-115">**About this document**</span></span>

<span data-ttu-id="874e0-116">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="874e0-116">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="874e0-117">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="874e0-117">This multi-step process includes:</span></span>
-   <span data-ttu-id="874e0-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="874e0-118">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="874e0-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="874e0-119">Registering your IoT device</span></span>
-   <span data-ttu-id="874e0-120">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="874e0-120">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="874e0-121">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="874e0-121">Step 1: Prerequisites</span></span>

<span data-ttu-id="874e0-122">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="874e0-122">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="874e0-123">[准备开发环境][setup-devbox-python]</span><span class="sxs-lookup"><span data-stu-id="874e0-123">[Prepare your development environment][setup-devbox-python]</span></span>
-   <span data-ttu-id="874e0-124">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="874e0-124">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="874e0-125">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="874e0-125">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="874e0-126">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="874e0-126">{enter your device name here} device.</span></span>
-   <span data-ttu-id="874e0-127">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="874e0-127">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="874e0-128">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="874e0-128">Step 2: Prepare your Device</span></span>
-   <span data-ttu-id="874e0-129">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="874e0-129">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="874e0-130">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="874e0-130">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="874e0-131">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="874e0-131">Step 3: Build and Run the sample</span></span>

<a name="Load"></a>
## <a name="31-build-sdk-and-sample"></a><span data-ttu-id="874e0-132">3.1 生成 SDK 和示例</span><span class="sxs-lookup"><span data-stu-id="874e0-132">3.1 Build SDK and sample</span></span>

-   <span data-ttu-id="874e0-133">使用以下命令下载最新的 SDK：</span><span class="sxs-lookup"><span data-stu-id="874e0-133">Download latest SDK using following command:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-python.git

- <span data-ttu-id="874e0-134">确保已安装所需的 Python 版本（2.7.x、3.4.x 或 3.5.x）。</span><span class="sxs-lookup"><span data-stu-id="874e0-134">Ensure that the desired Python version is installed (2.7.x, 3.4.x or 3.5.x).</span></span> <span data-ttu-id="874e0-135">在命令行中运行 python --version 或 python3 --version 可检查版本。</span><span class="sxs-lookup"><span data-stu-id="874e0-135">Run python --version or python3 --version at the command line to check the version.</span></span> 

- <span data-ttu-id="874e0-136">打开 Visual Studio 2015 x86 本机工具命令提示，然后导航到存储库本地副本中的 python/build_all/windows 文件夹。</span><span class="sxs-lookup"><span data-stu-id="874e0-136">Open a Visual Studio 2015 x86 Native Tools command prompt and navigate to the folder python/build_all/windows in your local copy of the repository.</span></span>

- <span data-ttu-id="874e0-137">在 python\build_all\windows 目录中运行脚本 build.cmd。</span><span class="sxs-lookup"><span data-stu-id="874e0-137">Run the script build.cmd in the python\build_all\windows directory.</span></span>

- <span data-ttu-id="874e0-138">这样就会将 **iothub_client.pyd** Python 扩展模块复制到 python/device/samples 文件夹。</span><span class="sxs-lookup"><span data-stu-id="874e0-138">As a result, the **iothub_client.pyd** Python extension module is copied to the python/device/samples folder.</span></span>

- <span data-ttu-id="874e0-139">导航到存储库本地副本中的 python/device/samples 文件夹。</span><span class="sxs-lookup"><span data-stu-id="874e0-139">Navigate to the folder python/device/samples in your local copy of the repository.</span></span>

- <span data-ttu-id="874e0-140">在文本编辑器中打开 **iothub_client_sample_amqp.py**、**iothub_client_sample_http.py** 或 **iothub_client_sample_mqtt.py** 文件。</span><span class="sxs-lookup"><span data-stu-id="874e0-140">Open the file **iothub_client_sample_amqp.py**, **iothub_client_sample_http.py** or  **iothub_client_sample_mqtt.py** in a text editor.</span></span>

- <span data-ttu-id="874e0-141">在该文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="874e0-141">Locate the following code in the file:</span></span>

        connectionString = "[device connection string]"

-   <span data-ttu-id="874e0-142">将 [device connection string] 替换为设备的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="874e0-142">Replace [device connection string] with the connection string for your device.</span></span> <span data-ttu-id="874e0-143">保存更改。</span><span class="sxs-lookup"><span data-stu-id="874e0-143">Save the changes.</span></span>

## <a name="32-send-device-events-to-iot-hub"></a><span data-ttu-id="874e0-144">3.2 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="874e0-144">3.2 Send Device Events to IoT Hub:</span></span>

-   <span data-ttu-id="874e0-145">通过 Visual Studio 2015 x86 本地工具命令提示使用以下命令运行示例应用程序，然后导航到存储库本地副本中的 python/build_all/windows 文件夹：{{***保留根据协议设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="874e0-145">Run the sample application using the following command through Visual Studio 2015 x86 Native Tools command prompt and navigate to the folder python/build_all/windows in your local copy of the repository: {{***Keep the command set based on your protocol(s) and remove the rest.***}}</span></span>

    <span data-ttu-id="874e0-146">{{**如果使用 AMQP 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="874e0-146">{{**If using AMQP protocol:**}}</span></span>

        python iothub_client_sample_amqp.py

    <span data-ttu-id="874e0-147">{{**如果使用 HTTPS 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="874e0-147">{{**If using HTTPS protocol:**}}</span></span>

        python iothub_client_sample_http.py

    <span data-ttu-id="874e0-148">{{**如果使用 MQTT 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="874e0-148">{{**If using MQTT protocol:**}}</span></span>

        python iothub_client_sample_mqtt.py

-   <span data-ttu-id="874e0-149">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="874e0-149">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

## <a name="33-receive-messages-from-iot-hub"></a><span data-ttu-id="874e0-150">3.3 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="874e0-150">3.3 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="874e0-151">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="874e0-151">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="874e0-152">后续步骤</span><span class="sxs-lookup"><span data-stu-id="874e0-152">Next Steps</span></span>

<span data-ttu-id="874e0-153">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="874e0-153">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="874e0-154">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="874e0-154">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="874e0-155">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="874e0-155">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="874e0-156">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="874e0-156">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="874e0-157">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="874e0-157">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="874e0-158">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="874e0-158">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="874e0-159">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="874e0-159">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="874e0-160">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="874e0-160">[Remote monitoring and notifications with Logic Apps]</span></span>   

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
[setup-devbox-python]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/python-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
