<a name="how-to-certify-iot-devices-running-android-with-azure-iot-sdk"></a><span data-ttu-id="a31ef-101">如何使用 Azure IoT SDK 认证运行 Android 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="a31ef-101">How to certify IoT devices running Android with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="a31ef-102">目录</span><span class="sxs-lookup"><span data-stu-id="a31ef-102">Table of Contents</span></span>

-   [<span data-ttu-id="a31ef-103">简介</span><span class="sxs-lookup"><span data-stu-id="a31ef-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="a31ef-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="a31ef-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1)
-   [<span data-ttu-id="a31ef-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="a31ef-105">Step 2: Register Device</span></span>](#Step_2)
-   [<span data-ttu-id="a31ef-106">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="a31ef-106">Step 3: Build and Validate the sample using Java client libraries</span></span>](#Step_3)
    -   [<span data-ttu-id="a31ef-107">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="a31ef-107">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>](#Step_3_1)
    -   [<span data-ttu-id="a31ef-108">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="a31ef-108">3.2 Run and Validate the Samples</span></span>](#Step_3_2)
-   [<span data-ttu-id="a31ef-109">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="a31ef-109">Step 4: Package and Share</span></span>](#Step_4)
    -   [<span data-ttu-id="a31ef-110">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="a31ef-110">4.1 Package build logs and sample test results</span></span>](#Step_4_1)
    -   [<span data-ttu-id="a31ef-111">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="a31ef-111">4.2 Share with the Azure IoT Certification team</span></span>](#Step_4_2)
    -   [<span data-ttu-id="a31ef-112">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="a31ef-112">4.3 Next steps</span></span>](#Step_4_3)
-   [<span data-ttu-id="a31ef-113">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="a31ef-113">Step 5: Troubleshooting</span></span>](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="a31ef-114">简介</span><span class="sxs-lookup"><span data-stu-id="a31ef-114">Introduction</span></span>

<span data-ttu-id="a31ef-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="a31ef-115">**About this document**</span></span>

<span data-ttu-id="a31ef-116">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT Java SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="a31ef-116">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT Java SDK.</span></span> <span data-ttu-id="a31ef-117">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="a31ef-117">This multi-step process includes:</span></span> 
-   <span data-ttu-id="a31ef-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="a31ef-118">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="a31ef-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="a31ef-119">Registering your IoT device</span></span>
-   <span data-ttu-id="a31ef-120">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="a31ef-120">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="a31ef-121">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="a31ef-121">Packaging and sharing the logs</span></span>

<span data-ttu-id="a31ef-122">**准备**</span><span class="sxs-lookup"><span data-stu-id="a31ef-122">**Prepare**</span></span>

<span data-ttu-id="a31ef-123">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="a31ef-123">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="a31ef-124">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="a31ef-124">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="a31ef-125">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="a31ef-125">Computer with GitHub installed and access to the [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub public repository.</span></span>
-   <span data-ttu-id="a31ef-126">需要认证的硬件。</span><span class="sxs-lookup"><span data-stu-id="a31ef-126">Required hardware to certify.</span></span>

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="a31ef-127">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="a31ef-127">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="a31ef-128">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="a31ef-128">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="a31ef-129">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="a31ef-129">As part of the sign up process, you will receive the connection string.</span></span> 

-   <span data-ttu-id="a31ef-130">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="a31ef-130">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="a31ef-131">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="a31ef-131">Step 2: Register Device</span></span>

-   <span data-ttu-id="a31ef-132">遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)所述的说明，了解如何预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="a31ef-132">Follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) on how to provision your device and get its credentials.</span></span>

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-java-client-libraries"></a><span data-ttu-id="a31ef-133">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="a31ef-133">Step 3: Build and Validate the sample using Java client libraries</span></span>

<span data-ttu-id="a31ef-134">本部分逐步讲解如何在运行 Android OS 4.0.3 或更高版本的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="a31ef-134">This section walks you through building, deploying and validating the IoT Client SDK on your device running an Android OS version 4.0.3 or greater.</span></span> <span data-ttu-id="a31ef-135">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="a31ef-135">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="a31ef-136">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="a31ef-136">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1"></a>
## <a name="31-prepare-your-development-environment"></a><span data-ttu-id="a31ef-137">3.1 准备开发环境</span><span class="sxs-lookup"><span data-stu-id="a31ef-137">3.1 Prepare your development environment</span></span>

-   <span data-ttu-id="a31ef-138">从[此处](<http://www.oracle.com/technetwork/java/javase/downloads/index.html>)下载并安装最新的 JDK。</span><span class="sxs-lookup"><span data-stu-id="a31ef-138">Download and install latest JDK from [here](<http://www.oracle.com/technetwork/java/javase/downloads/index.html>).</span></span>

-   <span data-ttu-id="a31ef-139">将 [Android Studio](<https://developer.android.com/studio/index.html> 下载到 Windows 计算机上，然后遵照安装说明操作。</span><span class="sxs-lookup"><span data-stu-id="a31ef-139">Download [Android Studio](<https://developer.android.com/studio/index.html> on your Windows machine and follow the installation instructions.</span></span>

- <span data-ttu-id="a31ef-140">使用 USB 电缆将设备插入开发计算机。</span><span class="sxs-lookup"><span data-stu-id="a31ef-140">Plug in your device to your development machine with a USB cable.</span></span> <span data-ttu-id="a31ef-141">如果在 Windows 上开发，可能需要安装设备适用的 USB 驱动程序。</span><span class="sxs-lookup"><span data-stu-id="a31ef-141">If you're developing on Windows, you might need to install the appropriate USB driver for your device.</span></span> <span data-ttu-id="a31ef-142">有关安装驱动程序的帮助，请参阅 [OEM USB 驱动程序](<https://developer.android.com/studio/run/oem-usb.html>)文档。</span><span class="sxs-lookup"><span data-stu-id="a31ef-142">For help installing drivers, see the [OEM USB Drivers](<https://developer.android.com/studio/run/oem-usb.html>) document.</span></span>
- <span data-ttu-id="a31ef-143">在设备上启用 USB 调试。</span><span class="sxs-lookup"><span data-stu-id="a31ef-143">Enable USB debugging on your device.</span></span> <span data-ttu-id="a31ef-144">在 Android 4.0 和更高版本上，请转到“设置”>“开发人员选项”。</span><span class="sxs-lookup"><span data-stu-id="a31ef-144">On Android 4.0 and newer, go to Settings > Developer options.</span></span>

    <span data-ttu-id="a31ef-145">***注意***：在 Android 4.2 及更高版本上，“开发人员选项”默认为隐藏。*若要使其可见，请转到“设置”>“关于手机”，然后点击“软件版本号”七次。返回上一屏幕即可找到“开发人员选项”。*</span><span class="sxs-lookup"><span data-stu-id="a31ef-145">***Note***: *On Android 4.2 and newer, Developer options is hidden by default. To make it available, go to Settings > About phone and tap Build number seven times. Return to the previous screen to find Developer options.*</span></span>

<a name="Step_3_2"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="a31ef-146">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="a31ef-146">3.2 Build the Samples</span></span>

1.  <span data-ttu-id="a31ef-147">启动 Android Studio 的新实例并从该位置打开 Android 项目：</span><span class="sxs-lookup"><span data-stu-id="a31ef-147">Start a new instance of Android Studio and open Android project from here:</span></span>

        azure-iot-sdk-java/device/iot-device-samples/android-sample/        

2.  <span data-ttu-id="a31ef-148">转到“MainActivity.java”，将 **[device connection string]** 占位符替换为在[步骤 2](#Step_2) 中创建的设备连接字符串，然后保存该文件。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-148">Go to **MainActivity.java**, replace the **[device connection string]** placeholder with connection string of the device you have created in [Step 2](#Step_2) and save the file.</span></span>

3. <span data-ttu-id="a31ef-149">转到“生成”菜单并选择“生成项目”，以生成项目。  </span><span class="sxs-lookup"><span data-stu-id="a31ef-149">Build your project by going to **Build** menu **> Make Project**.</span></span>


<a name="Step_3_3"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="a31ef-150">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="a31ef-150">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="a31ef-151">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="a31ef-151">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="a31ef-152">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="a31ef-152">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="a31ef-153">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="a31ef-153">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="a31ef-154">\*\**注意：\*\*\*\*请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="a31ef-154">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2).*</span></span>

<a name="Step_3_2_1"></a>
### <a name="321-run-the-sample"></a><span data-ttu-id="a31ef-155">3.2.1 运行示例：</span><span class="sxs-lookup"><span data-stu-id="a31ef-155">3.2.1 Run the Sample:</span></span>

#### <a name="run-on-the-device"></a><span data-ttu-id="a31ef-156">在设备上运行</span><span class="sxs-lookup"><span data-stu-id="a31ef-156">Run on the Device</span></span>

- <span data-ttu-id="a31ef-157">选择一个项目文件，然后单击工具栏上的“运行”。</span><span class="sxs-lookup"><span data-stu-id="a31ef-157">Select one of your project's files and click Run  from the toolbar.</span></span>
- <span data-ttu-id="a31ef-158">在显示的“选择设备”窗口中，选中“选择正在运行的设备”单选按钮，选择你的设备，然后单击“确定”。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-158">In the Choose Device window that appears, select the **Choose a running device** radio button, select your device, and click OK .</span></span> 
- <span data-ttu-id="a31ef-159">Android Studio 将在连接的设备上安装并启动应用。</span><span class="sxs-lookup"><span data-stu-id="a31ef-159">Android Studio will install the app on your connected device and starts it.</span></span>

#### <a name="run-on-the-emulator"></a><span data-ttu-id="a31ef-160">在模拟器上运行</span><span class="sxs-lookup"><span data-stu-id="a31ef-160">Run on the Emulator</span></span>

1.  <span data-ttu-id="a31ef-161">通过“工具”菜单 >“Android”>“AVD Manager”启动“AVD Manager”。   </span><span class="sxs-lookup"><span data-stu-id="a31ef-161">Launch the **AVD Manager** from **Tools** menu **> Android > AVD Manager**.</span></span>
2.  <span data-ttu-id="a31ef-162">在模拟器中启动虚拟设备。</span><span class="sxs-lookup"><span data-stu-id="a31ef-162">Launch a virtual device in emulator.</span></span> <span data-ttu-id="a31ef-163">如果列表中未显示任何设备，请创建一个设备。</span><span class="sxs-lookup"><span data-stu-id="a31ef-163">If no device is shown in the list, create one.</span></span>
3.  <span data-ttu-id="a31ef-164">加载并运行设备后，请通过“运行”菜单 >“运行 ‘模块名称’”或者单击 **Shift + F10** **运行**应用。  </span><span class="sxs-lookup"><span data-stu-id="a31ef-164">Once device is loaded and running, **Run** your app from **Run** menu **> Run 'module_name'** or by clicking **Shift + F10**.</span></span>
4.  <span data-ttu-id="a31ef-165">在“选择部署目标”弹出窗口中选择虚拟设备。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-165">Select your virtual device from the **Select Deployment Target** pop-up window.</span></span>
5.  <span data-ttu-id="a31ef-166">随后将在模拟器中加载应用。</span><span class="sxs-lookup"><span data-stu-id="a31ef-166">Your app will load in the emulator.</span></span>

<a name="Step_3_2_2"></a>
### <a name="322-send-device-events-to-iot-hub"></a><span data-ttu-id="a31ef-167">3.2.2 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="a31ef-167">3.2.2 Send Device Events to IoT Hub:</span></span>

1.  <span data-ttu-id="a31ef-168">如[步骤 2](#Step_2) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。  从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-168">Launch the DeviceExplorer as explained in [Step 2](#Step_2) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/de_monitordevice.png)

2.  <span data-ttu-id="a31ef-170">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="a31ef-170">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="a31ef-171">在设备（或模拟器）上运行应用后，应用会立即开始向 IoT 中心发送消息。</span><span class="sxs-lookup"><span data-stu-id="a31ef-171">As soon as you run the app on your device (or emulator), it will start sending messages to IoTHub.</span></span>

4.  <span data-ttu-id="a31ef-172">查看“Android Monitor”窗口。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-172">Check the **Android Monitor** window.</span></span> <span data-ttu-id="a31ef-173">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="a31ef-173">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="a31ef-174">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="a31ef-174">If not, then you may have incorrectly copied the device hub connection information.</span></span>

    <span data-ttu-id="a31ef-175">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="a31ef-175">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="a31ef-176">![Terminal\_HTTP\_send\_event](images/androidmonitor_logcat_sendmessages_http.png)</span><span class="sxs-lookup"><span data-stu-id="a31ef-176">![Terminal\_HTTP\_send\_event](images/androidmonitor_logcat_sendmessages_http.png)</span></span>

    <span data-ttu-id="a31ef-177">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="a31ef-177">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="a31ef-178">![Terminal\_MQTT\_send\_event](images/androidmonitor_logcat_sendmessages_mqtt.png)</span><span class="sxs-lookup"><span data-stu-id="a31ef-178">![Terminal\_MQTT\_send\_event](images/androidmonitor_logcat_sendmessages_mqtt.png)</span></span>

6.  <span data-ttu-id="a31ef-179">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="a31ef-179">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="a31ef-180">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="a31ef-180">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="a31ef-181">![DeviceExplorer\_HTTP\_message\_received](images/de_sendmessages_http.png)</span><span class="sxs-lookup"><span data-stu-id="a31ef-181">![DeviceExplorer\_HTTP\_message\_received](images/de_sendmessages_http.png)</span></span>

    <span data-ttu-id="a31ef-182">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="a31ef-182">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="a31ef-183">![DeviceExplorer\_MQTT\_message\_received](images/de_sendmessages_mqtt.png)</span><span class="sxs-lookup"><span data-stu-id="a31ef-183">![DeviceExplorer\_MQTT\_message\_received](images/de_sendmessages_mqtt.png)</span></span>

<a name="Step_3_2_3"></a>
### <a name="323-receive-messages-from-iot-hub"></a><span data-ttu-id="a31ef-184">3.2.3 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="a31ef-184">3.2.3 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="a31ef-185">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-185">To verify that you can send messages from the IoT Hub to your device, go to the **Messages To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="a31ef-186">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="a31ef-186">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="a31ef-187">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="a31ef-187">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_message\_send](images/de_receivemessage.png)

4.  <span data-ttu-id="a31ef-189">在设备或模拟器上加载的示例应用 UI 中单击“接收消息”按钮。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-189">Click the **Receive Messages** button from the sample App UI loaded on your device or in the emulator.</span></span>

5.  <span data-ttu-id="a31ef-190">查看“Android Monitor”窗口。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-190">Check the **Android Monitor** window.</span></span> <span data-ttu-id="a31ef-191">应会看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="a31ef-191">You should be able to see the command received.</span></span>

    <span data-ttu-id="a31ef-192">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="a31ef-192">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="a31ef-193">![Terminal\_HTTP\_message\_received](images/androidmonitor_logcat_receivemessage_http.png)</span><span class="sxs-lookup"><span data-stu-id="a31ef-193">![Terminal\_HTTP\_message\_received](images/androidmonitor_logcat_receivemessage_http.png)</span></span>

    <span data-ttu-id="a31ef-194">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="a31ef-194">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="a31ef-195">![Terminal\_MQTT\_message\_received](images/androidmonitor_logcat_receivemessage_mqtt.png)</span><span class="sxs-lookup"><span data-stu-id="a31ef-195">![Terminal\_MQTT\_message\_received](images/androidmonitor_logcat_receivemessage_mqtt.png)</span></span>

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="a31ef-196">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="a31ef-196">Step 4: Package and Share</span></span>

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="a31ef-197">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="a31ef-197">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="a31ef-198">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="a31ef-198">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="a31ef-199">执行步骤 3.1.4 和 3.1.5 过程中在日志文件记录的生成日志和测试结果。</span><span class="sxs-lookup"><span data-stu-id="a31ef-199">Build logs and test results that were logged in the log files during steps 3.1.4 and 3.1.5.</span></span>

2.  <span data-ttu-id="a31ef-200">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="a31ef-200">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="a31ef-201">前面“**从 IoT 中心接收消息**”部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="a31ef-201">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="a31ef-202">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="a31ef-202">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> 
    
    <span data-ttu-id="a31ef-203">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="a31ef-203">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a><span data-ttu-id="a31ef-204">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="a31ef-204">4.2 Share with the Azure IoT Certification team</span></span>

1.  <span data-ttu-id="a31ef-205">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="a31ef-205">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="a31ef-206">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="a31ef-206">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="a31ef-208">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="a31ef-208">This will open an upload dialog.</span></span> <span data-ttu-id="a31ef-209">单击“上载”按钮浏览文件。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-209">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="a31ef-211">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="a31ef-211">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="a31ef-212">上传所有文件后，单击“提交审查”按钮。 </span><span class="sxs-lookup"><span data-stu-id="a31ef-212">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="a31ef-213">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="a31ef-213">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a><span data-ttu-id="a31ef-214">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="a31ef-214">4.3 Next steps</span></span>

<span data-ttu-id="a31ef-215">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="a31ef-215">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="a31ef-216">步骤 5：疑难解答</span><span class="sxs-lookup"><span data-stu-id="a31ef-216">Step 5: Troubleshooting</span></span>

<span data-ttu-id="a31ef-217">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="a31ef-217">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
