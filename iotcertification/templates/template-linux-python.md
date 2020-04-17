---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: python
ms.openlocfilehash: f12f4bfa4f76e9da3908d242ec05b745813d2cf4
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62456404"
---
<a name="run-a-simple-python-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="fa479-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 PYTHON 示例</span><span class="sxs-lookup"><span data-stu-id="fa479-101">Run a simple PYTHON sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="fa479-102">目录</span><span class="sxs-lookup"><span data-stu-id="fa479-102">Table of Contents</span></span>

-   [<span data-ttu-id="fa479-103">介绍</span><span class="sxs-lookup"><span data-stu-id="fa479-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="fa479-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="fa479-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="fa479-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="fa479-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="fa479-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="fa479-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="fa479-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="fa479-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="fa479-108">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="fa479-108">Instructions for using this template</span></span>

-   <span data-ttu-id="fa479-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="fa479-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="fa479-110">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="fa479-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="fa479-111">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="fa479-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="fa479-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="fa479-112">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="fa479-113">介绍</span><span class="sxs-lookup"><span data-stu-id="fa479-113">Introduction</span></span>

<span data-ttu-id="fa479-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="fa479-114">**About this document**</span></span>

<span data-ttu-id="fa479-115">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="fa479-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="fa479-116">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="fa479-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="fa479-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="fa479-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="fa479-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="fa479-118">Registering your IoT device</span></span>
-   <span data-ttu-id="fa479-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="fa479-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="fa479-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="fa479-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="fa479-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="fa479-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="fa479-122">[准备开发环境][setup-devbox-python]</span><span class="sxs-lookup"><span data-stu-id="fa479-122">[Prepare your development environment][setup-devbox-python]</span></span>
-   <span data-ttu-id="fa479-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="fa479-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="fa479-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="fa479-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="fa479-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="fa479-125">{enter your device name here} device.</span></span>
-   <span data-ttu-id="fa479-126">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="fa479-126">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="fa479-127">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="fa479-127">Step 2: Prepare your Device</span></span>
-   <span data-ttu-id="fa479-128">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="fa479-128">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="fa479-129">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="fa479-129">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="fa479-130">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="fa479-130">Step 3: Build and Run the sample</span></span>

<a name="Load"></a>
## <a name="31-build-sdk-and-sample"></a><span data-ttu-id="fa479-131">3.1 生成 SDK 和示例</span><span class="sxs-lookup"><span data-stu-id="fa479-131">3.1 Build SDK and sample</span></span>

-   <span data-ttu-id="fa479-132">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="fa479-132">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="fa479-133">在开发上的命令行中发出以下命令，安装用于 Python 的 Microsoft Azure IoT 设备 SDK 的必备组件包：{{***保留根据 OS 设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="fa479-133">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for Python by issuing the following commands from the command line on your board: {{***Keep the command set based on your OS and remove the rest.***}}</span></span>

     <span data-ttu-id="fa479-134">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="fa479-134">**Debian or Ubuntu**</span></span>

        sudo apt-get update

        sudo apt-get install -y curl libcurl4-openssl-dev build-essential cmake git python2.7-dev libboost-python-dev

    <span data-ttu-id="fa479-135">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="fa479-135">**Fedora**</span></span>

        sudo dnf check-update -y

        sudo dnf install libcurl-devel openssl-devel gcc-c++ make cmake git python2.7-dev libboost-python-dev

    <span data-ttu-id="fa479-136">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="fa479-136">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

    <span data-ttu-id="fa479-137">{{***如果需要其他任何软件，请在此处指定用于安装这些软件的命令。***}}</span><span class="sxs-lookup"><span data-stu-id="fa479-137">{{***If any other software is required, please specify here the command(s) for installing same.***}}</span></span>

-   <span data-ttu-id="fa479-138">在开发板上发出以下命令，将 Microsoft Azure IoT 设备 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="fa479-138">Download the Microsoft Azure IoT Device SDK to the board by issuing the following command on the board::</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-python.git

-   <span data-ttu-id="fa479-139">运行以下命令生成 SDK：</span><span class="sxs-lookup"><span data-stu-id="fa479-139">Run following commands to build the SDK:</span></span>

        cd python/build_all/linux
        sudo ./build.sh    

-   <span data-ttu-id="fa479-140">成功生成后，`iothub_client.so` Python 扩展模块将复制到 **python/device/samples** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="fa479-140">After a successful build, the `iothub_client.so` Python extension module is copied to the **python/device/samples** folder.</span></span>

- <span data-ttu-id="fa479-141">执行以下命令导航到 samples 文件夹：</span><span class="sxs-lookup"><span data-stu-id="fa479-141">Navigate to samples folder by executing following command:</span></span>

        cd azure-iot-sdk-python/device/samples/

-   <span data-ttu-id="fa479-142">使用所选的任何文本编辑器编辑以下文件：{{***根据协议保留文件并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="fa479-142">Edit the following file using any text editor of your choice: {{***Keep the file based on your protocol(s) and remove the rest.***}}</span></span>

    <span data-ttu-id="fa479-143">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fa479-143">**For AMQP protocol:**</span></span>

        nano iothub_client_sample_amqp.py

    <span data-ttu-id="fa479-144">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fa479-144">**For HTTP protocol:**</span></span>

        nano iothub_client_sample_http.py

    <span data-ttu-id="fa479-145">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="fa479-145">**For MQTT protocol:**</span></span>

        nano iothub_client_sample_mqtt.py

-   <span data-ttu-id="fa479-146">找到设备连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="fa479-146">Find the following place holder for device connection string:</span></span>

        connectionString = "[device connection string]"

-   <span data-ttu-id="fa479-147">将上述占位符替换为在[步骤 1](#Prerequisites) 中获取的设备连接字符串，然后保存更改。</span><span class="sxs-lookup"><span data-stu-id="fa479-147">Replace the above placeholder with device connection string you obtained in [Step 1](#Prerequisites) and save the changes.</span></span>

## <a name="32-send-device-events-to-iot-hub"></a><span data-ttu-id="fa479-148">3.2 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="fa479-148">3.2 Send Device Events to IoT Hub:</span></span>

-   <span data-ttu-id="fa479-149">使用以下命令运行示例应用程序：{{***保留根据协议设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="fa479-149">Run the sample application using the following command: {{***Keep the command set based on your protocol(s) and remove the rest.***}}</span></span>

    <span data-ttu-id="fa479-150">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fa479-150">**For AMQP protocol:**</span></span>

        python iothub_client_sample_amqp.py

    <span data-ttu-id="fa479-151">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fa479-151">**For HTTP protocol:**</span></span>

        python iothub_client_sample_http.py

    <span data-ttu-id="fa479-152">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="fa479-152">**For MQTT protocol:**</span></span>

        python iothub_client_sample_mqtt.py

-   <span data-ttu-id="fa479-153">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="fa479-153">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

## <a name="33-receive-messages-from-iot-hub"></a><span data-ttu-id="fa479-154">3.3 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="fa479-154">3.3 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="fa479-155">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="fa479-155">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="fa479-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="fa479-156">Next Steps</span></span>

<span data-ttu-id="fa479-157">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="fa479-157">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="fa479-158">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="fa479-158">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="fa479-159">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="fa479-159">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="fa479-160">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="fa479-160">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="fa479-161">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="fa479-161">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="fa479-162">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="fa479-162">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="fa479-163">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="fa479-163">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="fa479-164">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="fa479-164">[Remote monitoring and notifications with Logic Apps]</span></span>   

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

