---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: javascript
ms.openlocfilehash: 96df8ca2bad7d4bef51c5180c4926c9aefa6fc0b
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62439603"
---
<a name="run-a-simple-javascript-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="c4130-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JavaScript 示例</span><span class="sxs-lookup"><span data-stu-id="c4130-101">Run a simple JavaScript sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="c4130-102">目录</span><span class="sxs-lookup"><span data-stu-id="c4130-102">Table of Contents</span></span>

-   [<span data-ttu-id="c4130-103">介绍</span><span class="sxs-lookup"><span data-stu-id="c4130-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="c4130-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="c4130-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="c4130-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="c4130-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="c4130-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="c4130-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="c4130-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c4130-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="c4130-108">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="c4130-108">Instructions for using this template</span></span>

-   <span data-ttu-id="c4130-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="c4130-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="c4130-110">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="c4130-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="c4130-111">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="c4130-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="c4130-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="c4130-112">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="c4130-113">介绍</span><span class="sxs-lookup"><span data-stu-id="c4130-113">Introduction</span></span>

<span data-ttu-id="c4130-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="c4130-114">**About this document**</span></span>

<span data-ttu-id="c4130-115">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="c4130-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="c4130-116">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="c4130-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="c4130-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c4130-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="c4130-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="c4130-118">Registering your IoT device</span></span>
-   <span data-ttu-id="c4130-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="c4130-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="c4130-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="c4130-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="c4130-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="c4130-121">You should have the following items ready before beginning the process:</span></span>


-   <span data-ttu-id="c4130-122">[准备开发环境][setup-devbox-linux]</span><span class="sxs-lookup"><span data-stu-id="c4130-122">[Prepare your development environment][setup-devbox-linux]</span></span>
-   <span data-ttu-id="c4130-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="c4130-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="c4130-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="c4130-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="c4130-125">装有 Git 客户端的计算机</span><span class="sxs-lookup"><span data-stu-id="c4130-125">Computer with Git client installed</span></span>
-   <span data-ttu-id="c4130-126">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="c4130-126">{enter your device name here} device.</span></span>
-   <span data-ttu-id="c4130-127">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="c4130-127">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="c4130-128">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="c4130-128">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="c4130-129">在 **C:\OpenSSL** 位置安装 OpenSSL 并执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c4130-129">Install OpenSSL at **C:\OpenSSL** location and perform following actions:</span></span>
    -   <span data-ttu-id="c4130-130">将 `C:\OpenSSL\` 添加到 **PATH** 环境变量</span><span class="sxs-lookup"><span data-stu-id="c4130-130">Add `C:\OpenSSL\` to the **PATH** environment variable</span></span>
    -   <span data-ttu-id="c4130-131">在 OpenSSL 目录中搜索“openssl.cnf”文件的位置。</span><span class="sxs-lookup"><span data-stu-id="c4130-131">Search for the location of file 'openssl.cnf' inside the OpenSSL directory.</span></span>
    -   <span data-ttu-id="c4130-132">创建新环境变量 **OPENSSL_CONF** 并将其值设置为 `openssl.cnf` 文件的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="c4130-132">Create a new environment variable **OPENSSL_CONF** and set its value as absolute path of the file `openssl.cnf`.</span></span>
    
-   <span data-ttu-id="c4130-133">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="c4130-133">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="c4130-134">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="c4130-134">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="c4130-135">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="c4130-135">Step 3: Build and Run the Sample</span></span>

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="c4130-136">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="c4130-136">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="c4130-137">创建环境变量 `IOTHUB_CONNECTION_STRING`，并将其值设置为在[步骤 1](#Prerequisites) 中获取的 **IoT 中心连接字符串**。</span><span class="sxs-lookup"><span data-stu-id="c4130-137">Create environment variable `IOTHUB_CONNECTION_STRING` and set its value as your **IoTHub connection string** which you got in [Step 1](#Prerequisites).</span></span>

-   <span data-ttu-id="c4130-138">打开 Node.js 命令提示符。</span><span class="sxs-lookup"><span data-stu-id="c4130-138">Open a Node.js command prompt.</span></span>
        
-   <span data-ttu-id="c4130-139">检查是否已正确设置所有环境变量。</span><span class="sxs-lookup"><span data-stu-id="c4130-139">Check all environment variables are properly set.</span></span>

        echo %PATH%
        echo %OPENSSL_CONF%
        echo %IOTHUB_CONNECTION_STRING%
    
-   <span data-ttu-id="c4130-140">下载该 SDK</span><span class="sxs-lookup"><span data-stu-id="c4130-140">Download the SDK</span></span> 

        git clone --recursive https://github.com/Azure/azure-iot-sdk-node.git


<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="c4130-141">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="c4130-141">3.2 Build the samples</span></span>

-   <span data-ttu-id="c4130-142">若要验证源代码，请在设备上的 Node.js 命令提示符下运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="c4130-142">To validate the source code run the following commands on Node.js command prompt on Device.</span></span>

        cd azure-iot-sdk-node
        build\dev-setup.cmd
        build\build.cmd > LogFile.txt

    <span data-ttu-id="c4130-143">\*\**注意：\*\*\*\*应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*</span><span class="sxs-lookup"><span data-stu-id="c4130-143">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>

-   <span data-ttu-id="c4130-144">安装 npm 包以运行示例。</span><span class="sxs-lookup"><span data-stu-id="c4130-144">Install npm package to run sample.</span></span>

        cd \azure-iot-sdk-node\device\samples

    <span data-ttu-id="c4130-145">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c4130-145">**For AMQP Protocol:**</span></span>
    
        npm install azure-iot-device-amqp
    
    <span data-ttu-id="c4130-146">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c4130-146">**For HTTP Protocol:**</span></span>
    
        npm install azure-iot-device-http
    
    <span data-ttu-id="c4130-147">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c4130-147">**For MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt   

-   <span data-ttu-id="c4130-148">更新示例以设置协议。</span><span class="sxs-lookup"><span data-stu-id="c4130-148">Update the sample to set the protocol.</span></span>

        cd azure-iot-sdk-node\device\samples
        notepad simple_sample_device.js

-   <span data-ttu-id="c4130-149">这会启动文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="c4130-149">This launches a text editor.</span></span> <span data-ttu-id="c4130-150">向下滚动到协议信息，找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4130-150">Scroll down to the protocol information and find the below code:</span></span>

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    <span data-ttu-id="c4130-151">使用的默认协议为 AMQP。</span><span class="sxs-lookup"><span data-stu-id="c4130-151">The default protocol used is AMQP.</span></span> <span data-ttu-id="c4130-152">脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。</span><span class="sxs-lookup"><span data-stu-id="c4130-152">Code for other protocols(HTTP/MQTT) are mentioned just below the above line in the script.</span></span> 
    <span data-ttu-id="c4130-153">请根据想要使用的协议取消注释相应的代码行。</span><span class="sxs-lookup"><span data-stu-id="c4130-153">Uncomment the line as per the protocol you want to use.</span></span>

-   <span data-ttu-id="c4130-154">向下滚动到连接信息，找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="c4130-154">Scroll down to the connection information and find following placeholder for IoT connection string:</span></span>

        var connectionString = "[IoT Device Connection String]";

-   <span data-ttu-id="c4130-155">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c4130-155">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="c4130-156">可根据[步骤 1](#Prerequisites) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c4130-156">You can get this from DeviceExplorer as explained in [Step 1](#Prerequisites), that you copied into Notepad.</span></span>

-   <span data-ttu-id="c4130-157">保存更改并关闭记事本。</span><span class="sxs-lookup"><span data-stu-id="c4130-157">Save your changes and close the notepad.</span></span>

-   <span data-ttu-id="c4130-158">退出 **azure-iot-sdk-node\device\samples** 目录之前，在 Node.js 命令提示符下运行以下命令</span><span class="sxs-lookup"><span data-stu-id="c4130-158">Run the following command on Node.js command prompt before leaving the **azure-iot-sdk-node\device\samples** directory</span></span>

        npm link azure-iot-device

<a name="Run"></a>

## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="c4130-159">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="c4130-159">3.3 Run and Validate the Samples</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="c4130-160">3.3.1：向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="c4130-160">3.3.1 Send Device Events to IoT Hub</span></span>

-   <span data-ttu-id="c4130-161">发出以下命令运行示例，验证是否已成功发送和接收数据。</span><span class="sxs-lookup"><span data-stu-id="c4130-161">Run the sample by issuing following command and verify that data has been successfully sent and received.</span></span>

        node azure-iot-sdk-node\device\samples\simple_sample_device.js

-   <span data-ttu-id="c4130-162">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="c4130-162">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="c4130-163">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="c4130-163">3.3.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="c4130-164">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4130-164">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="c4130-165">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c4130-165">Next Steps</span></span>

<span data-ttu-id="c4130-166">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4130-166">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="c4130-167">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="c4130-167">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="c4130-168">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="c4130-168">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="c4130-169">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="c4130-169">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="c4130-170">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="c4130-170">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="c4130-171">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="c4130-171">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="c4130-172">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="c4130-172">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="c4130-173">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="c4130-173">[Remote monitoring and notifications with Logic Apps]</span></span>   

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
[setup-devbox-linux]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/node-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

