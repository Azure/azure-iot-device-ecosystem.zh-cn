---
platform: 
device: 
language: c
ms.openlocfilehash: cd392662f2406a037d660f8d0269ab3544a9732e
ms.sourcegitcommit: 4b98ebc1c3cad79b3f19f21d36add53daa71e0b5
ms.translationtype: HT
ms.contentlocale: zh-CN
---
<a name="run-a-simple-c-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="dc205-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C 示例</span><span class="sxs-lookup"><span data-stu-id="dc205-101">Run a simple C sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="dc205-102">目录</span><span class="sxs-lookup"><span data-stu-id="dc205-102">Table of Contents</span></span>

-   [<span data-ttu-id="dc205-103">介绍</span><span class="sxs-lookup"><span data-stu-id="dc205-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="dc205-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="dc205-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="dc205-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="dc205-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="dc205-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="dc205-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="dc205-107">提示</span><span class="sxs-lookup"><span data-stu-id="dc205-107">Tips</span></span>](#tips)
-   [<span data-ttu-id="dc205-108">后续步骤</span><span class="sxs-lookup"><span data-stu-id="dc205-108">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="dc205-109">此模板的用法说明</span><span class="sxs-lookup"><span data-stu-id="dc205-109">Instructions for using this template</span></span>

-   <span data-ttu-id="dc205-110">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="dc205-110">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="dc205-111">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="dc205-111">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="dc205-112">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="dc205-112">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="dc205-113">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="dc205-113">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="dc205-114">介绍</span><span class="sxs-lookup"><span data-stu-id="dc205-114">Introduction</span></span>

<span data-ttu-id="dc205-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="dc205-115">**About this document**</span></span>

<span data-ttu-id="dc205-116">本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="dc205-116">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="dc205-117">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="dc205-117">This multi-step process includes:</span></span>
-   <span data-ttu-id="dc205-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="dc205-118">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="dc205-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="dc205-119">Registering your IoT device</span></span>
-   <span data-ttu-id="dc205-120">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="dc205-120">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="dc205-121">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="dc205-121">Step 1: Prerequisites</span></span>

<span data-ttu-id="dc205-122">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="dc205-122">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="dc205-123">[准备开发环境][setup-devbox-linux]</span><span class="sxs-lookup"><span data-stu-id="dc205-123">[Prepare your development environment][setup-devbox-linux]</span></span>
-   <span data-ttu-id="dc205-124">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="dc205-124">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="dc205-125">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="dc205-125">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="dc205-126">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="dc205-126">{enter your device name here} device.</span></span>
-   <span data-ttu-id="dc205-127">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="dc205-127">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="dc205-128">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="dc205-128">Step 2: Prepare your Device</span></span>
-   <span data-ttu-id="dc205-129">{{记下安装、配置和连接设备时需要遵循的说明。</span><span class="sxs-lookup"><span data-stu-id="dc205-129">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="dc205-130">请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}</span><span class="sxs-lookup"><span data-stu-id="dc205-130">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="dc205-131">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="dc205-131">Step 3: Build and Run the sample</span></span>

<a name="Load"></a>
## <a name="31-build-sdk-and-sample"></a><span data-ttu-id="dc205-132">3.1 生成 SDK 和示例</span><span class="sxs-lookup"><span data-stu-id="dc205-132">3.1 Build SDK and sample</span></span>

-   <span data-ttu-id="dc205-133">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="dc205-133">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="dc205-134">在开发上的命令行中发出以下命令，安装用于 C 的 Microsoft Azure IoT 设备 SDK 的必备组件包：{{***保留根据 OS 设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="dc205-134">Install the prerequisite packages for the Microsoft Azure IoT Device SDK for C by issuing the following commands from the command line on your board: {{***Keep the command set based on your OS and remove the rest.***}}</span></span>

    <span data-ttu-id="dc205-135">{{**Debian 或 Ubuntu**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-135">{{**Debian or Ubuntu**}}</span></span>

        sudo apt-get update

        sudo apt-get install -y curl libcurl4-openssl-dev uuid-dev uuid g++ make cmake git unzip openjdk-7-jre

    <span data-ttu-id="dc205-136">{{**Fedora**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-136">{{**Fedora**}}</span></span>

        sudo dnf check-update -y

        sudo dnf install libcurl-devel openssl-devel libuuid-devel uuid-devel gcc-c++ make cmake git unzip java-1.7.0-openjdk

    <span data-ttu-id="dc205-137">{{**其他任何 Linux OS**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-137">{{**Any Other Linux OS**}}</span></span>

        Write equivalent commands on the target OS

    <span data-ttu-id="dc205-138">{{***如果需要其他任何软件，请在此处指定用于安装这些软件的命令。***}}</span><span class="sxs-lookup"><span data-stu-id="dc205-138">{{***If any other software is required, please specify here the command(s) for installing same.***}}</span></span>

-   <span data-ttu-id="dc205-139">在开发板上发出以下命令，将用于 C 的 Microsoft Azure IoT 设备 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="dc205-139">Download the Microsoft Azure IoT Device SDK for C to the board by issuing the following command on the board::</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-c.git

-   <span data-ttu-id="dc205-140">使用所选的任何文本编辑器编辑以下文件：{{***根据协议保留文件并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="dc205-140">Edit the following file using any text editor of your choice: {{***Keep the file based on your protocol(s) and remove the rest.***}}</span></span>

    <span data-ttu-id="dc205-141">{{**对于 AMQP 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-141">{{**For AMQP protocol:**}}</span></span>

        azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp.c

    <span data-ttu-id="dc205-142">{{**对于 HTTPS 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-142">{{**For HTTPS protocol:**}}</span></span>

        azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http.c

-   <span data-ttu-id="dc205-143">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="dc205-143">Find the following place holder for IoT connection string:</span></span>

        static const char* connectionString = "[device connection string]";

-   <span data-ttu-id="dc205-144">将上述占位符替换为在[步骤 1](#Prerequisites) 中获取的设备连接字符串，然后保存更改。</span><span class="sxs-lookup"><span data-stu-id="dc205-144">Replace the above placeholder with device connection string you obtained in [Step 1](#Prerequisites) and save the changes.</span></span>

-   <span data-ttu-id="dc205-145">使用以下命令生成 SDK。</span><span class="sxs-lookup"><span data-stu-id="dc205-145">Build the SDK using following command.</span></span>

        sudo ./azure-iot-sdk-c/build_all/linux/build.sh

## <a name="32-send-device-events-to-iot-hub"></a><span data-ttu-id="dc205-146">3.2 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="dc205-146">3.2 Send Device Events to IoT Hub:</span></span>

-   <span data-ttu-id="dc205-147">发出以下命令运行示例：{{***保留根据协议设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="dc205-147">Run the sample by issuing following command: {{***Keep the command set based on your protocol(s) and remove the rest.***}}</span></span>

    <span data-ttu-id="dc205-148">{{**如果使用 AMQP 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-148">{{**If using AMQP protocol:**}}</span></span>

        ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp

    <span data-ttu-id="dc205-149">{{**如果使用 HTTP 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-149">{{**If using HTTP protocol:**}}</span></span>

        ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http

    <span data-ttu-id="dc205-150">{{**如果使用 MQTT 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="dc205-150">{{**If using MQTT protocol:**}}</span></span>

        ~/azure-iot-sdk-c/c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_mqtt/iothub_client_sample_mqtt

-   <span data-ttu-id="dc205-151">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="dc205-151">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

## <a name="33-receive-messages-from-iot-hub"></a><span data-ttu-id="dc205-152">3.3 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="dc205-152">3.3 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="dc205-153">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="dc205-153">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>

<a name="tips"></a>
# <a name="tips"></a><span data-ttu-id="dc205-154">提示</span><span class="sxs-lookup"><span data-stu-id="dc205-154">Tips</span></span>

- <span data-ttu-id="dc205-155">如果只想要生成序列化程序示例，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="dc205-155">If you just want to build the serializer samples, run the following commands:</span></span>

  ```
  cd ./c/serializer/build/linux
  make -f makefile.linux all
  ```

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="dc205-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="dc205-156">Next Steps</span></span>

<span data-ttu-id="dc205-157">现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="dc205-157">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="dc205-158">若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="dc205-158">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="dc205-159">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="dc205-159">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="dc205-160">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="dc205-160">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="dc205-161">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="dc205-161">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="dc205-162">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="dc205-162">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="dc205-163">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="dc205-163">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="dc205-164">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="dc205-164">[Remote monitoring and notifications with Logic Apps]</span></span>   

<span data-ttu-id="dc205-165">[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging</span><span class="sxs-lookup"><span data-stu-id="dc205-165">[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging</span></span>
<span data-ttu-id="dc205-166">[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage</span><span class="sxs-lookup"><span data-stu-id="dc205-166">[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage</span></span>
<span data-ttu-id="dc205-167">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi</span><span class="sxs-lookup"><span data-stu-id="dc205-167">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi</span></span>
<span data-ttu-id="dc205-168">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps</span><span class="sxs-lookup"><span data-stu-id="dc205-168">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps</span></span>
<span data-ttu-id="dc205-169">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning</span><span class="sxs-lookup"><span data-stu-id="dc205-169">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning</span></span>
<span data-ttu-id="dc205-170">[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps</span><span class="sxs-lookup"><span data-stu-id="dc205-170">[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps</span></span>
[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

