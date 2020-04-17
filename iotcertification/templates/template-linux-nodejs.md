---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: javascript
ms.openlocfilehash: e23fb7e36e4d59bb9a1c4623ea03c009efc295b6
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62456406"
---
<a name="run-a-simple-javascript-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="c0e27-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JavaScript 示例</span><span class="sxs-lookup"><span data-stu-id="c0e27-101">Run a simple JavaScript sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="c0e27-102">目录</span><span class="sxs-lookup"><span data-stu-id="c0e27-102">Table of Contents</span></span>

-   [<span data-ttu-id="c0e27-103">介绍</span><span class="sxs-lookup"><span data-stu-id="c0e27-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="c0e27-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="c0e27-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="c0e27-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="c0e27-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="c0e27-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="c0e27-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="c0e27-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c0e27-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="c0e27-108">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="c0e27-108">Instructions for using this template</span></span>

-   <span data-ttu-id="c0e27-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="c0e27-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="c0e27-110">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="c0e27-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="c0e27-111">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="c0e27-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="c0e27-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="c0e27-112">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="c0e27-113">介绍</span><span class="sxs-lookup"><span data-stu-id="c0e27-113">Introduction</span></span>

<span data-ttu-id="c0e27-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="c0e27-114">**About this document**</span></span>

<span data-ttu-id="c0e27-115">本文档介绍如何使用 Azure IoT SDK 连接运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="c0e27-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="c0e27-116">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="c0e27-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="c0e27-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c0e27-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="c0e27-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="c0e27-118">Registering your IoT device</span></span>
-   <span data-ttu-id="c0e27-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="c0e27-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="c0e27-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="c0e27-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="c0e27-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="c0e27-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="c0e27-122">[准备开发环境][setup-devbox-linux]</span><span class="sxs-lookup"><span data-stu-id="c0e27-122">[Prepare your development environment][setup-devbox-linux]</span></span>
-   <span data-ttu-id="c0e27-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="c0e27-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="c0e27-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="c0e27-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="c0e27-125">装有 Git 客户端的计算机</span><span class="sxs-lookup"><span data-stu-id="c0e27-125">Computer with Git client installed</span></span> 
-   <span data-ttu-id="c0e27-126">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="c0e27-126">{enter your device name here} device.</span></span>
-   <span data-ttu-id="c0e27-127">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-127">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="c0e27-128">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="c0e27-128">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="c0e27-129">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="c0e27-129">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="c0e27-130">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-130">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a><span data-ttu-id="c0e27-131">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="c0e27-131">Step 3: Build and Run the Sample</span></span>

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="c0e27-132">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="c0e27-132">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="c0e27-133">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="c0e27-133">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="c0e27-134">在后续步骤中根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="c0e27-134">Choose your commands in next steps based on the OS running on your device.</span></span>

-   <span data-ttu-id="c0e27-135">运行以下命令检查是否已安装 NodeJS</span><span class="sxs-lookup"><span data-stu-id="c0e27-135">Run following command to check if NodeJS is already installed</span></span>

        node --version

    <span data-ttu-id="c0e27-136">如果版本为 **0.12.x 或更高**，可跳过有关安装必备组件包的后续步骤。</span><span class="sxs-lookup"><span data-stu-id="c0e27-136">If version is **0.12.x or greater**, then skip next step of installing prerequisite packages.</span></span> <span data-ttu-id="c0e27-137">否则，请在设备上的命令行中发出以下命令来卸载该版本。{{***保留根据 OS 设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-137">Else uninstall it by issuing following command from command line on the device.{{***Keep the command set based on your OS and remove the rest.***}}</span></span>

    <span data-ttu-id="c0e27-138">{{**Debian 或 Ubuntu**}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-138">{{**Debian or Ubuntu**}}</span></span>

        sudo apt-get remove nodejs

    <span data-ttu-id="c0e27-139">{{**Fedora**}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-139">{{**Fedora**}}</span></span>

        sudo dnf remove nodejs

    <span data-ttu-id="c0e27-140">{{**其他任何 Linux OS**}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-140">{{**Any Other Linux OS**}}</span></span>

        Use equivalent commands on the target OS

-   <span data-ttu-id="c0e27-141">通过设备上的命令行发出以下命令，安装必备的包。</span><span class="sxs-lookup"><span data-stu-id="c0e27-141">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span> <span data-ttu-id="c0e27-142">根据设备上运行的 OS 选择命令。{{***保留根据 OS 设置的命令并删除剩余内容。***}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-142">Choose your commands based on the OS running on your device.{{***Keep the command set based on your OS and remove the rest.***}}</span></span>

    <span data-ttu-id="c0e27-143">{{**Debian 或 Ubuntu**}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-143">{{**Debian or Ubuntu**}}</span></span>

        curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -

        sudo apt-get install -y nodejs

    <span data-ttu-id="c0e27-144">{{**Fedora**}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-144">{{**Fedora**}}</span></span>

        wget http://nodejs.org/dist/v4.2.1/node-v4.2.1-linux-x64.tar.gz

        tar xvf node-v4.2.1-linux-x64.tar.gz

        sudo mv node-v4.2.1-linux-x64 /opt

        echo "export PATH=\$PATH:/opt/node-v4.2.1-linux-x64/bin" >> ~/.bashrc

        source ~/.bashrc

    <span data-ttu-id="c0e27-145">{{**其他任何 Linux OS**}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-145">{{**Any Other Linux OS**}}</span></span>

        Use equivalent commands on the target OS

     <span data-ttu-id="c0e27-146">{{***如果需要其他任何软件，请在此处指定用于安装这些软件的命令。***}}</span><span class="sxs-lookup"><span data-stu-id="c0e27-146">{{***If any other software is required, please specify here the command(s) for installing same.***}}</span></span>
     
    <span data-ttu-id="c0e27-147">**注意：** 若要测试 Node JS 是否成功安装，请尝试运行以下命令获取其版本信息：</span><span class="sxs-lookup"><span data-stu-id="c0e27-147">**Note:** To test successful installation of Node JS, try to fetch its version information by running following command:</span></span>

        node --version

-   <span data-ttu-id="c0e27-148">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="c0e27-148">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-node.git

-   <span data-ttu-id="c0e27-149">验证 ~/azure-iot-sdk-node 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="c0e27-149">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-node.</span></span>

<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="c0e27-150">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="c0e27-150">3.2 Build the samples</span></span>

-   <span data-ttu-id="c0e27-151">若要验证源代码，请在设备上运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="c0e27-151">To validate the source code run the following commands on the device.</span></span>

        export IOTHUB_CONNECTION_STRING='<iothub_connection_string>'

    <span data-ttu-id="c0e27-152">将 `<iothub_connection_string>` 占位符替换为在[步骤 1](#Prerequisites) 中获取的 IoT 中心连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c0e27-152">Replace the `<iothub_connection_string>` placeholder with IoTHub Connection String you got in [Step 1](#Prerequisites).</span></span>    

-   <span data-ttu-id="c0e27-153">运行以下命令</span><span class="sxs-lookup"><span data-stu-id="c0e27-153">Run the following commands</span></span> 

        cd ~/azure-iot-sdk-node
        build/dev-setup.sh
        build/build.sh | tee LogFile.txt

    <span data-ttu-id="c0e27-154">\*\**注意：\*\*\*\*应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*</span><span class="sxs-lookup"><span data-stu-id="c0e27-154">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>

-   <span data-ttu-id="c0e27-155">安装 npm 包以运行示例。</span><span class="sxs-lookup"><span data-stu-id="c0e27-155">Install npm package to run sample.</span></span>

        cd ~/azure-iot-sdk-node/device/samples

    <span data-ttu-id="c0e27-156">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c0e27-156">**For AMQP Protocol:**</span></span>
    
        npm install azure-iot-device-amqp
    
    <span data-ttu-id="c0e27-157">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c0e27-157">**For HTTP Protocol:**</span></span>
    
        npm install azure-iot-device-http
    
    <span data-ttu-id="c0e27-158">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c0e27-158">**For MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt   

-   <span data-ttu-id="c0e27-159">若要更新示例，请在设备上运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="c0e27-159">To update sample, run the following command on device.</span></span>

        cd ~/azure-iot-sdk-node/device/samples
        nano simple_sample_device.js

-   <span data-ttu-id="c0e27-160">此时会启动基于控制台的文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="c0e27-160">This launches a console-based text editor.</span></span> <span data-ttu-id="c0e27-161">向下滚动到协议信息。</span><span class="sxs-lookup"><span data-stu-id="c0e27-161">Scroll down to the protocol information.</span></span>
    
-   <span data-ttu-id="c0e27-162">找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="c0e27-162">Find the below code:</span></span>

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    <span data-ttu-id="c0e27-163">使用的默认协议为 AMQP。</span><span class="sxs-lookup"><span data-stu-id="c0e27-163">The default protocol used is AMQP.</span></span> <span data-ttu-id="c0e27-164">脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。</span><span class="sxs-lookup"><span data-stu-id="c0e27-164">Code for other protocols(HTTP/MQTT) are mentioned just below the above line in the script.</span></span>
    <span data-ttu-id="c0e27-165">请根据想要使用的协议取消注释相应的代码行。</span><span class="sxs-lookup"><span data-stu-id="c0e27-165">Uncomment the line as per the protocol you want to use.</span></span>


-   <span data-ttu-id="c0e27-166">向下滚动到连接信息。</span><span class="sxs-lookup"><span data-stu-id="c0e27-166">Scroll down to the connection information.</span></span>
    <span data-ttu-id="c0e27-167">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="c0e27-167">Find the following place holder for IoT connection string:</span></span>

        var connectionString = "[IoT Device Connection String]";

-   <span data-ttu-id="c0e27-168">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c0e27-168">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="c0e27-169">可根据[步骤 1](#Prerequisites) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c0e27-169">You can get this from DeviceExplorer as explained in [Step 1](#Prerequisites), that you copied into Notepad.</span></span>

-   <span data-ttu-id="c0e27-170">按 Ctrl+O 保存更改，当 nano 提示是否保存为同一文件时，请按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="c0e27-170">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

-   <span data-ttu-id="c0e27-171">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="c0e27-171">Press Ctrl+X to exit nano.</span></span>

-   <span data-ttu-id="c0e27-172">在退出 **~/azure-iot-sdk-node/device/samples** 目录之前运行以下命令</span><span class="sxs-lookup"><span data-stu-id="c0e27-172">Run the following command before leaving the **~/azure-iot-sdk-node/device/samples** directory</span></span>

        npm link azure-iot-device

<a name="Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="c0e27-173">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="c0e27-173">3.3 Run and Validate the Samples</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="c0e27-174">3.3.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="c0e27-174">3.3.1 Send Device Events to IOT Hub</span></span>

-   <span data-ttu-id="c0e27-175">发出以下命令运行示例，验证是否已成功发送和接收数据。</span><span class="sxs-lookup"><span data-stu-id="c0e27-175">Run the sample by issuing following command and verify that data has been successfully sent and received.</span></span>

        node ~/azure-iot-sdk-node/device/samples/simple_sample_device.js

-   <span data-ttu-id="c0e27-176">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="c0e27-176">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="c0e27-177">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="c0e27-177">3.3.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="c0e27-178">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0e27-178">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>


<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="c0e27-179">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c0e27-179">Next Steps</span></span>

<span data-ttu-id="c0e27-180">现在，你已学会了如何运行一个可以收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0e27-180">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="c0e27-181">若要了解如何使用各种服务在 Azure 中存储、分析和可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="c0e27-181">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="c0e27-182">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="c0e27-182">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="c0e27-183">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="c0e27-183">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="c0e27-184">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="c0e27-184">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="c0e27-185">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="c0e27-185">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="c0e27-186">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="c0e27-186">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="c0e27-187">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="c0e27-187">[Remote monitoring and notifications with Logic Apps]</span></span>   

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

