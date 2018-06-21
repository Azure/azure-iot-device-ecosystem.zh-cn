---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: c
ms.openlocfilehash: ca3899acfb442ecf82a50517884a1ccf9d67e481
ms.sourcegitcommit: f08ccd5fd86c6ccb5d66495a76144a2f4e2e11ef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
ms.locfileid: "29770478"
---
<a name="run-a-simple-c-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="f14c9-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C 示例</span><span class="sxs-lookup"><span data-stu-id="f14c9-101">Run a simple C sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="f14c9-102">目录</span><span class="sxs-lookup"><span data-stu-id="f14c9-102">Table of Contents</span></span>

-   [<span data-ttu-id="f14c9-103">介绍</span><span class="sxs-lookup"><span data-stu-id="f14c9-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="f14c9-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="f14c9-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="f14c9-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="f14c9-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="f14c9-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="f14c9-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="f14c9-107">提示</span><span class="sxs-lookup"><span data-stu-id="f14c9-107">Tips</span></span>](#tips)
-   [<span data-ttu-id="f14c9-108">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f14c9-108">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="f14c9-109">此模板的用法说明</span><span class="sxs-lookup"><span data-stu-id="f14c9-109">Instructions for using this template</span></span>

-   <span data-ttu-id="f14c9-110">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="f14c9-110">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="f14c9-111">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="f14c9-111">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="f14c9-112">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="f14c9-112">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="f14c9-113">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="f14c9-113">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="f14c9-114">介绍</span><span class="sxs-lookup"><span data-stu-id="f14c9-114">Introduction</span></span>

<span data-ttu-id="f14c9-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="f14c9-115">**About this document**</span></span>

<span data-ttu-id="f14c9-116">本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="f14c9-116">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="f14c9-117">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="f14c9-117">This multi-step process includes:</span></span>
-   <span data-ttu-id="f14c9-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="f14c9-118">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="f14c9-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="f14c9-119">Registering your IoT device</span></span>
-   <span data-ttu-id="f14c9-120">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="f14c9-120">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="f14c9-121">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="f14c9-121">Step 1: Prerequisites</span></span>

<span data-ttu-id="f14c9-122">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="f14c9-122">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="f14c9-123">[准备开发环境][setup-devbox-linux]</span><span class="sxs-lookup"><span data-stu-id="f14c9-123">[Prepare your development environment][setup-devbox-linux]</span></span>
-   <span data-ttu-id="f14c9-124">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="f14c9-124">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="f14c9-125">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="f14c9-125">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="f14c9-126">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="f14c9-126">{enter your device name here} device.</span></span>
-   <span data-ttu-id="f14c9-127">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="f14c9-127">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="f14c9-128">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="f14c9-128">Step 2: Prepare your Device</span></span>
-   <span data-ttu-id="f14c9-129">{{记下安装、配置和连接设备时需要遵循的说明。</span><span class="sxs-lookup"><span data-stu-id="f14c9-129">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="f14c9-130">请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}</span><span class="sxs-lookup"><span data-stu-id="f14c9-130">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="f14c9-131">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="f14c9-131">Step 3: Build and Run the sample</span></span>

## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="f14c9-132">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="f14c9-132">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="f14c9-133">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="f14c9-133">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="f14c9-134">在设备上的命令行中发出以下命令，安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="f14c9-134">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span> <span data-ttu-id="f14c9-135">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="f14c9-135">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="f14c9-136">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="f14c9-136">**Debian or Ubuntu**</span></span>

        sudo apt-get update

        sudo apt-get install -y curl uuid-dev libcurl4-openssl-dev build-essential cmake git

    <span data-ttu-id="f14c9-137">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="f14c9-137">**Fedora**</span></span>

        sudo dnf check-update -y

        sudo dnf install uuid-devel libcurl-devel openssl-devel gcc-c++ make cmake git

    <span data-ttu-id="f14c9-138">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="f14c9-138">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

    <span data-ttu-id="f14c9-139">***注意：****此安装过程需要 cmake 2.8.12 或更高版本。*</span><span class="sxs-lookup"><span data-stu-id="f14c9-139">***Note:*** *This setup process requires cmake version 2.8.12 or higher.*</span></span> 
    
    <span data-ttu-id="f14c9-140">*可以使用以下命令确认环境中当前安装的版本：*</span><span class="sxs-lookup"><span data-stu-id="f14c9-140">*You can verify the current version installed in your environment using the  following command:*</span></span>

        cmake --version

    <span data-ttu-id="f14c9-141">*此库还需要 gcc 4.9 或更高版本。可以使用以下命令确认环境中当前安装的版本：*</span><span class="sxs-lookup"><span data-stu-id="f14c9-141">*This library also requires gcc version 4.9 or higher. You can verify the current version installed in your environment using the following command:*</span></span>
    
        gcc --version 

    <span data-ttu-id="f14c9-142">有关如何升级 Ubuntu 14.04 上的 gcc 版本的信息，请参阅 <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>。</span><span class="sxs-lookup"><span data-stu-id="f14c9-142">*For information about how to upgrade your version of gcc on Ubuntu 14.04, see <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>.*</span></span>
    
-   <span data-ttu-id="f14c9-143">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="f14c9-143">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-c.git

-   <span data-ttu-id="f14c9-144">验证 ~/azure-iot-sdk-c 目录中现在是否生成了源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="f14c9-144">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-c.</span></span>

<a name="Step-3-2-Build"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="f14c9-145">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="f14c9-145">3.2 Build the samples</span></span>

<span data-ttu-id="f14c9-146">有两个示例：一个用于向 IoT 中心发送消息，另一个用于从 IoT 中心接收消息。</span><span class="sxs-lookup"><span data-stu-id="f14c9-146">There are two samples one for sending messages to IoT Hub and another for receiving messages from IoT Hub.</span></span> <span data-ttu-id="f14c9-147">这两个示例支持不同的协议。</span><span class="sxs-lookup"><span data-stu-id="f14c9-147">Both samples supports different protocols.</span></span> <span data-ttu-id="f14c9-148">在生成示例之前，可以使用所选的协议对示例示例进行修改。</span><span class="sxs-lookup"><span data-stu-id="f14c9-148">You can make modification to the samples with your choice of protocol before building the samples.</span></span> <span data-ttu-id="f14c9-149">默认情况下，将会针对 AMQP 协议生成示例。</span><span class="sxs-lookup"><span data-stu-id="f14c9-149">By default the samples will build for AMQP protocol.</span></span>  <span data-ttu-id="f14c9-150">在生成之前，遵照以下说明编辑示例：</span><span class="sxs-lookup"><span data-stu-id="f14c9-150">Follow the below instructions to edit the samples before building:</span></span> 
    
### <a name="321-send-telemetry-to-iot-hub-sample"></a><span data-ttu-id="f14c9-151">3.2.1：向 IoT 中心示例发送遥测数据：</span><span class="sxs-lookup"><span data-stu-id="f14c9-151">3.2.1 Send Telemetry to IoT Hub Sample:</span></span>

1.  <span data-ttu-id="f14c9-152">在文本编辑器中打开遥测示例文件</span><span class="sxs-lookup"><span data-stu-id="f14c9-152">Open the telemetry sample file in a text editor</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_ll_telemetry_sample/iothub_ll_telemetry_sample.c     

2. <span data-ttu-id="f14c9-153">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="f14c9-153">Find the following placeholder for IoT connection string:</span></span>

        static const char* connectionString = "[device connection string]";

3. <span data-ttu-id="f14c9-154">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="f14c9-154">Replace the above placeholder with device connection string.</span></span>
    
4. <span data-ttu-id="f14c9-155">找到以下占位符以编辑协议：</span><span class="sxs-lookup"><span data-stu-id="f14c9-155">Find the following place holder for editing protocol:</span></span>

          // Select the Protocol to use with the connection
        #ifdef USE_AMQP
            //protocol = AMQP_Protocol_over_WebSocketsTls;
            protocol = AMQP_Protocol;
        #endif
        #ifdef USE_MQTT
            //protocol = MQTT_Protocol;
            //protocol = MQTT_WebSocket_Protocol;
        #endif
        #ifdef USE_HTTP
            //protocol = HTTP_Protocol;
        #endif
    
5. <span data-ttu-id="f14c9-156">取消注释要测试的协议，并注释其他协议。</span><span class="sxs-lookup"><span data-stu-id="f14c9-156">Please uncomment the protocol that you would like to test with and comment other protocols.</span></span> <span data-ttu-id="f14c9-157">若要测试多个协议，请对每个协议重复上述步骤。</span><span class="sxs-lookup"><span data-stu-id="f14c9-157">If testing for multiple protocols, please repeat above step for each protocol.</span></span> 

6. <span data-ttu-id="f14c9-158">按 Ctrl+O 保存更改，当 nano 提示是否保存到同一文件时，按 ENTER 即可。</span><span class="sxs-lookup"><span data-stu-id="f14c9-158">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

7. <span data-ttu-id="f14c9-159">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="f14c9-159">Press Ctrl+X to exit nano.</span></span>

### <a name="321-send-message-from-iot-hub-to-device-sample"></a><span data-ttu-id="f14c9-160">3.2.1：将消息从 IoT 中心发送到设备示例：</span><span class="sxs-lookup"><span data-stu-id="f14c9-160">3.2.1 Send message from IoT Hub to Device Sample:</span></span>

1. <span data-ttu-id="f14c9-161">在文本编辑器中打开遥测示例文件</span><span class="sxs-lookup"><span data-stu-id="f14c9-161">Open the telemetry sample file in a text editor</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_ll_c2d_sample/iothub_ll_c2d_sample.c

2. <span data-ttu-id="f14c9-162">遵循上述步骤 1-7 编辑此示例。</span><span class="sxs-lookup"><span data-stu-id="f14c9-162">Follow same steps 1-7 as above to edit this sample.</span></span>

### <a name="321-build-the-samples"></a><span data-ttu-id="f14c9-163">3.2.1：生成示例：</span><span class="sxs-lookup"><span data-stu-id="f14c9-163">3.2.1 Build the samples:</span></span>

-   <span data-ttu-id="f14c9-164">使用以下命令生成 SDK。</span><span class="sxs-lookup"><span data-stu-id="f14c9-164">Build the SDK using following command.</span></span> <span data-ttu-id="f14c9-165">如果生成期间遇到任何问题。</span><span class="sxs-lookup"><span data-stu-id="f14c9-165">If you are facing any issues during build.</span></span>

        sudo ./azure-iot-sdk-c/build_all/linux/build.sh | tee LogFile.txt
    
    <span data-ttu-id="f14c9-166">***注意：****应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*</span><span class="sxs-lookup"><span data-stu-id="f14c9-166">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>
    
    <span data-ttu-id="f14c9-167">*build.sh 在“~/azure-iot-sdk-c/”下创建名为“cmake”的文件夹。“cmake”中保存了整个软件的所有编译结果。*</span><span class="sxs-lookup"><span data-stu-id="f14c9-167">*build.sh creates a folder called "cmake" under "~/azure-iot-sdk-c/". Inside "cmake" are all the results of the compilation of the complete software.*</span></span>


<a name="Step-3-3-Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="f14c9-168">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="f14c9-168">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="f14c9-169">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="f14c9-169">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="f14c9-170">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="f14c9-170">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="f14c9-171">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="f14c9-171">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="f14c9-172">3.3.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="f14c9-172">3.3.1 Send Device Events to IOT Hub:</span></span>

-   <span data-ttu-id="f14c9-173">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="f14c9-173">Run the sample by issuing following command.</span></span>    

        azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_ll_telemetry_sample/iothub_ll_telemetry_sample


### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="f14c9-174">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="f14c9-174">3.3.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="f14c9-175">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="f14c9-175">Run the sample by issuing following command.</span></span>

        azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_ll_c2d_sample/iothub_ll_c2d_sample
        

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="f14c9-176">后续步骤</span><span class="sxs-lookup"><span data-stu-id="f14c9-176">Next Steps</span></span>

<span data-ttu-id="f14c9-177">现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="f14c9-177">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="f14c9-178">若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="f14c9-178">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="f14c9-179">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="f14c9-179">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="f14c9-180">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="f14c9-180">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="f14c9-181">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="f14c9-181">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="f14c9-182">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="f14c9-182">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="f14c9-183">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="f14c9-183">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="f14c9-184">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="f14c9-184">[Remote monitoring and notifications with Logic Apps]</span></span>   

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
[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
