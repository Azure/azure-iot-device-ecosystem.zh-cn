---
platform: 
device: 
language: java
ms.openlocfilehash: 8cdb9d7dc6b61d00729ee6d29af258875df246ed
ms.sourcegitcommit: 4b98ebc1c3cad79b3f19f21d36add53daa71e0b5
ms.translationtype: HT
ms.contentlocale: zh-CN
---
<a name="run-a-simple-java-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="af002-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JAVA 示例</span><span class="sxs-lookup"><span data-stu-id="af002-101">Run a simple JAVA sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="af002-102">目录</span><span class="sxs-lookup"><span data-stu-id="af002-102">Table of Contents</span></span>

-   [<span data-ttu-id="af002-103">介绍</span><span class="sxs-lookup"><span data-stu-id="af002-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="af002-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="af002-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="af002-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="af002-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="af002-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="af002-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="af002-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="af002-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="af002-108">此模板的用法说明</span><span class="sxs-lookup"><span data-stu-id="af002-108">Instructions for using this template</span></span>

-   <span data-ttu-id="af002-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="af002-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="af002-110">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="af002-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="af002-111">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="af002-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="af002-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="af002-112">Remove this section from final document.</span></span>

<a name="Introduction"/>
# <a name="introduction"></a><span data-ttu-id="af002-113">介绍</span><span class="sxs-lookup"><span data-stu-id="af002-113">Introduction</span></span>

<span data-ttu-id="af002-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="af002-114">**About this document**</span></span>

<span data-ttu-id="af002-115">本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="af002-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="af002-116">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="af002-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="af002-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="af002-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="af002-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="af002-118">Registering your IoT device</span></span>
-   <span data-ttu-id="af002-119">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="af002-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="af002-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="af002-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="af002-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="af002-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="af002-122">[准备开发环境][setup-devbox-windows]</span><span class="sxs-lookup"><span data-stu-id="af002-122">[Prepare your development environment][setup-devbox-windows]</span></span>
-   <span data-ttu-id="af002-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="af002-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="af002-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="af002-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="af002-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="af002-125">{enter your device name here} device.</span></span>
-   <span data-ttu-id="af002-126">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="af002-126">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="af002-127">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="af002-127">Step 2: Prepare your Device</span></span>
-   <span data-ttu-id="af002-128">{{记下安装、配置和连接设备时需要遵循的说明。</span><span class="sxs-lookup"><span data-stu-id="af002-128">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="af002-129">请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}</span><span class="sxs-lookup"><span data-stu-id="af002-129">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-sdk-and-run-the-sample"></a><span data-ttu-id="af002-130">步骤 3：生成 SDK 并运行示例</span><span class="sxs-lookup"><span data-stu-id="af002-130">Step 3: Build SDK and Run the sample</span></span>

<a name="Step_3_1"/>
## <a name="31-install-azure-iot-device-sdk-and-prerequisites-on-device"></a><span data-ttu-id="af002-131">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="af002-131">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>

-   <span data-ttu-id="af002-132">运行 SDK 需要 Java SE 1.8。</span><span class="sxs-lookup"><span data-stu-id="af002-132">To run the SDK you will need Java SE 1.8.</span></span>

-   <span data-ttu-id="af002-133">在设备上使用命令行安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="af002-133">Install the prerequisite packages using command line on the device.</span></span>

<a name="Step_3_1_1"/>
### <a name="311--install-java-jdk-18-and-set-up-environment-variables"></a><span data-ttu-id="af002-134">3.1.1 安装 Java JDK 1.8 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="af002-134">3.1.1  Install Java JDK 1.8 and set up environment variables</span></span>
        
1.  <span data-ttu-id="af002-135">有关下载和安装说明，请访问：<http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></span><span class="sxs-lookup"><span data-stu-id="af002-135">For downloads and installation instructions go here: <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></span></span>
       
2.  <span data-ttu-id="af002-136">请确保 `PATH` 环境变量包含 jdk1.8.x\bin 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="af002-136">Please make sure that the `PATH` environment variable includes the full path to the jdk1.8.x\bin directory.</span></span> <span data-ttu-id="af002-137">（示例：c:\Program Files\Java\jdk1.8.0_65）</span><span class="sxs-lookup"><span data-stu-id="af002-137">(Example: c:\Program Files\Java\jdk1.8.0_65)</span></span>
        
3.  <span data-ttu-id="af002-138">请确保 `JAVA_HOME` 环境变量包含 jdk1.8.x 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="af002-138">Please make sure that the `JAVA_HOME` environment variable includes the full path to the jdk1.8.x directory.</span></span> <span data-ttu-id="af002-139">（示例：JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65）</span><span class="sxs-lookup"><span data-stu-id="af002-139">(Example: JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65)</span></span>

4.  <span data-ttu-id="af002-140">可以通过重新启动控制台并运行 `java -version`，来测试是否已正确设置 PATH 变量。</span><span class="sxs-lookup"><span data-stu-id="af002-140">You can test whether your PATH variable is set correctly by restarting your console and running `java -version`.</span></span>

<a name="Step_3_1_2"/>
### <a name="312--install-maven-and-set-up-environment-variables"></a><span data-ttu-id="af002-141">3.1.2 安装 Maven 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="af002-141">3.1.2  Install Maven and set up environment variables</span></span>
<span data-ttu-id="af002-142">建议使用 Maven 3 安装用于 Java 的 Azure IoT 设备 SDK。</span><span class="sxs-lookup"><span data-stu-id="af002-142">Using Maven 3 is the recommended way to install Azure IoT device SDK for Java.</span></span>

1.  <span data-ttu-id="af002-143">有关 Maven 3 的下载和安装说明，请访问：<https://maven.apache.org/download.cgi></span><span class="sxs-lookup"><span data-stu-id="af002-143">For downloads and installation instructions for maven 3 go here: <https://maven.apache.org/download.cgi></span></span>

2.  <span data-ttu-id="af002-144">请确保 PATH 环境变量包含 apache-maven-3.x.x\bin 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="af002-144">Please make sure that the PATH environment variable includes the full path to the apache-maven-3.x.x\bin directory.</span></span> <span data-ttu-id="af002-145">（示例：F:\Setups\apache-maven-3.3.3\bin）。</span><span class="sxs-lookup"><span data-stu-id="af002-145">(Example: F:\Setups\apache-maven-3.3.3\bin).</span></span> <span data-ttu-id="af002-146">Apache maven 3.x.x 目录是 Maven 3 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="af002-146">The apache-maven-3.x.x directory is where Maven 3 is installed.</span></span>

2.  <span data-ttu-id="af002-147">可以通过重新启动控制台并运行 `mvn --version.`，来验证是否已正确设置用于运行 Maven 3 的环境变量</span><span class="sxs-lookup"><span data-stu-id="af002-147">You can verify that the environment variables necessary to run Maven 3 have been set correctly by restarting your console and running `mvn --version.`</span></span>
  
<a name="Step_3_1_3"/>
### <a name="313--install-git"></a><span data-ttu-id="af002-148">3.1.3 安装 GIT</span><span class="sxs-lookup"><span data-stu-id="af002-148">3.1.3  Install GIT</span></span>

-   <span data-ttu-id="af002-149">有关下载和安装说明，请访问：<http://git-scm.com/book/en/v2/Getting-Started-Installing-Git></span><span class="sxs-lookup"><span data-stu-id="af002-149">For downloads and installation instructions go here: <http://git-scm.com/book/en/v2/Getting-Started-Installing-Git></span></span>


<a name="Step_3_1_4"/>
### <a name="314-build-the-azure-iot-device-sdk-for-java"></a><span data-ttu-id="af002-150">3.1.4 生成适用于 Java 的 Azure IoT 设备 SDK</span><span class="sxs-lookup"><span data-stu-id="af002-150">3.1.4 Build the Azure IoT Device SDK for Java</span></span>

1.  <span data-ttu-id="af002-151">发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="af002-151">Download the SDK to the board by issuing the following command:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-java.git

2.  <span data-ttu-id="af002-152">验证 **azure-iot-sdk-java** 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="af002-152">Verify that you now have a copy of the source code under the directory **azure-iot-sdk-java**.</span></span>

3.  <span data-ttu-id="af002-153">在设备上按顺序运行以下命令，生成 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="af002-153">Run the following commands on device in sequence to build Azure IoT SDK.</span></span>

        cd azure-iot-sdk-java/device
        mvn install

4.  <span data-ttu-id="af002-154">上述命令将生成包含所有依赖项的已编译 JAR 文件。</span><span class="sxs-lookup"><span data-stu-id="af002-154">Above command will generate the compiled JAR files with all dependencies.</span></span> <span data-ttu-id="af002-155">可在以下位置找到此捆绑包：</span><span class="sxs-lookup"><span data-stu-id="af002-155">This bundle can be found at:</span></span>

        azure-iot-sdk-java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"/>
## <a name="32-run-and-validate-the-samples"></a><span data-ttu-id="af002-156">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="af002-156">3.2 Run and Validate the Samples</span></span>

<a name="Step_3_2_1"/>
### <a name="321-send-device-events-to-iot-hub"></a><span data-ttu-id="af002-157">3.2.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="af002-157">3.2.1 Send Device Events to IoT Hub:</span></span>

-   <span data-ttu-id="af002-158">导航到包含发送事件示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="af002-158">Navigate to the folder containing the executable JAR file for send event sample.</span></span>

        cd /azure-iot-sdk-java/device/samples/send-event/target

-   <span data-ttu-id="af002-159">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="af002-159">Run the sample by issuing following command.</span></span>
<span data-ttu-id="af002-160">{{保留根据协议设置的命令并删除剩余内容。}}</span><span class="sxs-lookup"><span data-stu-id="af002-160">{{Keep the command set based on your protocol(s) and remove the rest.}}</span></span>

    <span data-ttu-id="af002-161">{{**如果使用 AMQPS 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="af002-161">{{**If using AMQPS protocol:**}}</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps"
    
    <span data-ttu-id="af002-162">{{**如果使用 HTTPS 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="af002-162">{{**If using HTTPS protocol:**}}</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "https"

    <span data-ttu-id="af002-163">{{**如果使用 MQTT 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="af002-163">{{**If using MQTT protocol:**}}</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "mqtt"
        
    <span data-ttu-id="af002-164">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="af002-164">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="af002-165">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="af002-165">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="af002-166">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="af002-166">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="af002-167">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="af002-167">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

-   <span data-ttu-id="af002-168">在 Windows 上，请参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“监视设备到云的事件”，确定设备是否正在发送数据。</span><span class="sxs-lookup"><span data-stu-id="af002-168">On Windows, refer "Monitor device-to-cloud events" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to see the data your device is sending.</span></span>

<a name="Step_3_2_2"/>
### <a name="322-receive-messages-from-iot-hub"></a><span data-ttu-id="af002-169">3.2.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="af002-169">3.2.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="af002-170">导航到包含接收消息示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="af002-170">Navigate to the folder containing the executable JAR file for the receive message sample.</span></span>

        cd /azure-iot-sdk-java/device/samples/handle-messages/target
     
-   <span data-ttu-id="af002-171">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="af002-171">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="af002-172">{{**如果使用 AMQPS 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="af002-172">{{**If using AMQPS protocol:**}}</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps"
    
    <span data-ttu-id="af002-173">{{**如果使用 HTTPS 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="af002-173">{{**If using HTTPS protocol:**}}</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "https"
        
     <span data-ttu-id="af002-174">{{**如果使用 MQTT 协议：**}}</span><span class="sxs-lookup"><span data-stu-id="af002-174">{{**If using MQTT protocol:**}}</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "mqtt"

    <span data-ttu-id="af002-175">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="af002-175">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="af002-176">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="af002-176">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="af002-177">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="af002-177">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="af002-178">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="af002-178">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

-   <span data-ttu-id="af002-179">在 Windows 上，请参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“发送云到设备的消息”，获取有关向设备发送消息的说明。</span><span class="sxs-lookup"><span data-stu-id="af002-179">On Windows, refer "Send cloud-to-device messages" in [DeviceExplorer Usage document](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) for instructions on sending messages to device.</span></span>

<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="af002-180">后续步骤</span><span class="sxs-lookup"><span data-stu-id="af002-180">Next Steps</span></span>

<span data-ttu-id="af002-181">现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="af002-181">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="af002-182">若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="af002-182">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="af002-183">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="af002-183">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="af002-184">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="af002-184">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="af002-185">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="af002-185">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="af002-186">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="af002-186">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="af002-187">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="af002-187">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="af002-188">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="af002-188">[Remote monitoring and notifications with Logic Apps]</span></span>   

<span data-ttu-id="af002-189">[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging</span><span class="sxs-lookup"><span data-stu-id="af002-189">[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging</span></span>
<span data-ttu-id="af002-190">[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage</span><span class="sxs-lookup"><span data-stu-id="af002-190">[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage</span></span>
<span data-ttu-id="af002-191">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi</span><span class="sxs-lookup"><span data-stu-id="af002-191">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi</span></span>
<span data-ttu-id="af002-192">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps</span><span class="sxs-lookup"><span data-stu-id="af002-192">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps</span></span>
<span data-ttu-id="af002-193">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning</span><span class="sxs-lookup"><span data-stu-id="af002-193">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning</span></span>
<span data-ttu-id="af002-194">[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps</span><span class="sxs-lookup"><span data-stu-id="af002-194">[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps</span></span>
[setup-devbox-windows]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/java-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

