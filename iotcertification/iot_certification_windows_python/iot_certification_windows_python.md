<a name="how-to-certify-iot-devices-running-windows-10-with-azure-iot-sdk"></a><span data-ttu-id="5bea4-101">如何使用 Azure IoT SDK 认证运行 Windows 10 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="5bea4-101">How to certify IoT devices running Windows 10 with Azure IoT SDK</span></span> 
===
---


# <a name="table-of-contents"></a><span data-ttu-id="5bea4-102">目录</span><span class="sxs-lookup"><span data-stu-id="5bea4-102">Table of Contents</span></span>

-   [<span data-ttu-id="5bea4-103">介绍</span><span class="sxs-lookup"><span data-stu-id="5bea4-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="5bea4-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="5bea4-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1_Sign_Up)
-   <span data-ttu-id="5bea4-105">[步骤 2：注册设备](#Step_2</span><span class="sxs-lookup"><span data-stu-id="5bea4-105">[Step 2: Register Device](#Step_2</span></span>
-   <span data-ttu-id="5bea4-106">Register)</span><span class="sxs-lookup"><span data-stu-id="5bea4-106">Register)</span></span>
-   [<span data-ttu-id="5bea4-107">步骤 3：使用 Python 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="5bea4-107">Step 3: Build and Validate the Sample using Python Client Libraries</span></span>](#Step_3_Build_and_Validate)
    -   [<span data-ttu-id="5bea4-108">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="5bea4-108">3.1 Connect the Device</span></span>](#Step_3_1_Connect)
    -   [<span data-ttu-id="5bea4-109">3.2 设置开发环境</span><span class="sxs-lookup"><span data-stu-id="5bea4-109">3.2 Setup your development environment</span></span>](#Step_3_2_Setup)
    -   [<span data-ttu-id="5bea4-110">3.3 使用 Nuget 包在 Windows 上生成 Python iothub_client 模块（建议）</span><span class="sxs-lookup"><span data-stu-id="5bea4-110">3.3 Build the Python iothub_client module on Windows using Nuget packages (recommended)</span></span>](#Step_3_3_Build)
    -   [<span data-ttu-id="5bea4-111">3.4 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="5bea4-111">3.4 Run and Validate the Samples</span></span>](#Step_3_4_Run)
-   [<span data-ttu-id="5bea4-112">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="5bea4-112">Step 4: Package and Share</span></span>](#Step_4_Package_Share)
    -   [<span data-ttu-id="5bea4-113">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="5bea4-113">4.1 Package build logs and sample test results</span></span>](#Step_4_1_Package)
    -   [<span data-ttu-id="5bea4-114">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="5bea4-114">4.2 Share package with Engineering Support</span></span>](#Step_4_2_Share)
    -   [<span data-ttu-id="5bea4-115">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="5bea4-115">4.3 Next steps</span></span>](#Step_4_3_Next)
-   [<span data-ttu-id="5bea4-116">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="5bea4-116">Step 5: Troubleshooting</span></span>](#Step_5_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="5bea4-117">介绍</span><span class="sxs-lookup"><span data-stu-id="5bea4-117">Introduction</span></span>

<span data-ttu-id="5bea4-118">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="5bea4-118">**About this document**</span></span>

<span data-ttu-id="5bea4-119">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="5bea4-119">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="5bea4-120">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="5bea4-120">This multi-step process includes:</span></span>
-   <span data-ttu-id="5bea4-121">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="5bea4-121">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="5bea4-122">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="5bea4-122">Registering your IoT device</span></span>
-   <span data-ttu-id="5bea4-123">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="5bea4-123">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="5bea4-124">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="5bea4-124">Packaging and sharing the logs</span></span>  

<span data-ttu-id="5bea4-125">**准备**</span><span class="sxs-lookup"><span data-stu-id="5bea4-125">**Prepare**</span></span>

<span data-ttu-id="5bea4-126">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="5bea4-126">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="5bea4-127">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="5bea4-127">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="5bea4-128">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-python](https://github.com/Azure/azure-iot-sdk-python) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="5bea4-128">Computer with GitHub installed and access to the [azure-iot-sdk-python](https://github.com/Azure/azure-iot-sdk-python) GitHub public repository.</span></span>
-   <span data-ttu-id="5bea4-129">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="5bea4-129">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="5bea4-130">可以安装任何版本的 Visual Studio，包括免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="5bea4-130">You can install any edition of Visual Studio, including the free Community edition.</span></span>

<a name="Step_1_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="5bea4-131">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="5bea4-131">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="5bea4-132">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="5bea4-132">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="5bea4-133">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5bea4-133">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="5bea4-134">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="5bea4-134">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2_Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="5bea4-135">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="5bea4-135">Step 2: Register Device</span></span>

- [<span data-ttu-id="5bea4-136">预配设备并获取其凭据</span><span class="sxs-lookup"><span data-stu-id="5bea4-136">Provision your device and get its credentials</span></span>](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)

<a name="Step_3_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-python-client-libraries"></a><span data-ttu-id="5bea4-137">步骤 3：使用 Python 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="5bea4-137">Step 3: Build and Validate the Sample using Python Client Libraries</span></span> 

<span data-ttu-id="5bea4-138">本部分逐步讲解如何在运行 Windows 10 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="5bea4-138">This section walks you through building, deploying and validating the IoT Client SDK on your device running Windows 10 operating system.</span></span> <span data-ttu-id="5bea4-139">我们将在设备上安装所需的必备组件。</span><span class="sxs-lookup"><span data-stu-id="5bea4-139">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="5bea4-140">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="5bea4-140">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1_Connect"></a>
## <a name="31-connect-the-device"></a><span data-ttu-id="5bea4-141">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="5bea4-141">3.1 Connect the Device</span></span>

1.  <span data-ttu-id="5bea4-142">使用以太网电缆将开发板连接到网络。</span><span class="sxs-lookup"><span data-stu-id="5bea4-142">Connect the board to your network using an Ethernet cable.</span></span> <span data-ttu-id="5bea4-143">由于示例依赖于 Internet 访问，因此必须执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="5bea4-143">This step is required, as the sample depends on internet access.</span></span>

2.  <span data-ttu-id="5bea4-144">使用 micro-USB 电缆将设备插入计算机。</span><span class="sxs-lookup"><span data-stu-id="5bea4-144">Plug the device into your computer using a micro-USB cable.</span></span>

<a name="Step_3_2_Setup"></a>
## <a name="32--setup-your-development-environment"></a><span data-ttu-id="5bea4-145">3.2 设置开发环境</span><span class="sxs-lookup"><span data-stu-id="5bea4-145">3.2  Setup your development environment</span></span>

<span data-ttu-id="5bea4-146">完成以下步骤以设置开发环境：</span><span class="sxs-lookup"><span data-stu-id="5bea4-146">Complete the following steps to set up your development environment:</span></span>

1. <span data-ttu-id="5bea4-147">使用以下命令下载最新的 SDK：</span><span class="sxs-lookup"><span data-stu-id="5bea4-147">Download latest SDK using following command:</span></span>
  
  ```
  git clone --recursive https://github.com/Azure/azure-iot-sdk-python.git
  ```

2. <span data-ttu-id="5bea4-148">安装最新的 x86 或 x64 Python 2.7 客户端。</span><span class="sxs-lookup"><span data-stu-id="5bea4-148">Install the latest x86 or x64 Python 2.7 client.</span></span> <span data-ttu-id="5bea4-149">生成过程需要在路径中包含有效的 Python.exe。</span><span class="sxs-lookup"><span data-stu-id="5bea4-149">The build needs a valid Python.exe in the path.</span></span> <span data-ttu-id="5bea4-150">生成脚本会根据正在使用的 Python 版本（例如 Python 2.7.11 x86 32 位）选择编译器。</span><span class="sxs-lookup"><span data-stu-id="5bea4-150">Based on the active Python version (e.g. Python 2.7.11 x86 32bit) the build script choses the compiler.</span></span>

> <span data-ttu-id="5bea4-151">可以通过 [python-2.7](https://www.python.org/downloads/) 安装最新的 x86 或 x64 Python 2.7 客户端。</span><span class="sxs-lookup"><span data-stu-id="5bea4-151">You can install the latest x86 or x64 Python 2.7 client from [python-2.7](https://www.python.org/downloads/).</span></span>

<a name="Step_3_2_Build"></a>
## <a name="33--build-the-python-iothubclient-module-on-windows-using-nuget-packages-recommended"></a><span data-ttu-id="5bea4-152">3.3 使用 Nuget 包在 Windows 上生成 Python iothub_client 模块（建议）</span><span class="sxs-lookup"><span data-stu-id="5bea4-152">3.3  Build the Python iothub_client module on Windows using Nuget packages (recommended)</span></span>

<span data-ttu-id="5bea4-153">以下说明介绍如何在 Windows 中生成库：</span><span class="sxs-lookup"><span data-stu-id="5bea4-153">The following instructions outline how you can build the libraries in Windows:</span></span>

1. <span data-ttu-id="5bea4-154">打开 Visual Studio 2015 x86 本机工具命令提示，然后导航到存储库本地副本中的 python/build_all/windows 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5bea4-154">Open a Visual Studio 2015 x86 Native Tools command prompt and navigate to the folder python/build_all/windows in your local copy of the repository.</span></span>

    ![Navigation\_terminal](images/build_path_1.png)        
    
2. <span data-ttu-id="5bea4-156">在 python\build_all\windows 目录中运行脚本 build.cmd。</span><span class="sxs-lookup"><span data-stu-id="5bea4-156">Run the script build.cmd in the python\build_all\windows directory.</span></span>

3. <span data-ttu-id="5bea4-157">这样就会将 **iothub_client.pyd** Python 扩展模块复制到 python/device/samples 文件夹</span><span class="sxs-lookup"><span data-stu-id="5bea4-157">As a result, the **iothub_client.pyd** Python extension module is copied to the python/device/samples folder</span></span>

    ![Navigation\_terminal](images/build_path_2.png)    

<a name="Step_3_3_Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="5bea4-159">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="5bea4-159">3.3 Run and Validate the Samples</span></span>
    
<span data-ttu-id="5bea4-160">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="5bea4-160">In this section you will run the Azure IoT client SDK samples to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="5bea4-161">我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="5bea4-161">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="5bea4-162">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="5bea4-162">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="5bea4-163">\*\**注意：\*\*\*\*请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2_Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="5bea4-163">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2_Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="5bea4-164">3.3.1：向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="5bea4-164">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="5bea4-165">如[步骤 2](#Step_2_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="5bea4-165">Launch the DeviceExplorer as explained in [Step 2](#Step_2_Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="5bea4-167">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="5bea4-167">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>
     
3. <span data-ttu-id="5bea4-168">导航到存储库本地副本中的 python/device/samples 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5bea4-168">Navigate to the folder python/device/samples in your local copy of the repository.</span></span> 

4. <span data-ttu-id="5bea4-169">在文本编辑器中打开 **iothub_client_sample.py** 或 **iothub_client_sample_class.py** 文件。</span><span class="sxs-lookup"><span data-stu-id="5bea4-169">Open the file **iothub_client_sample.py** or  **iothub_client_sample_class.py** in a text editor.</span></span>

5. <span data-ttu-id="5bea4-170">在该文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="5bea4-170">Locate the following code in the file:</span></span>

        connectionString = "[device connection string]"

6. <span data-ttu-id="5bea4-171">将 [device connection string] 替换为设备的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5bea4-171">Replace [device connection string] with the connection string for your device.</span></span> <span data-ttu-id="5bea4-172">保存更改。</span><span class="sxs-lookup"><span data-stu-id="5bea4-172">Save the changes.</span></span>

7.  <span data-ttu-id="5bea4-173">通过 Visual Studio 2015 x86 本地工具命令提示使用以下命令运行示例应用程序，然后导航到存储库本地副本中的 python/build_all/windows 文件夹：</span><span class="sxs-lookup"><span data-stu-id="5bea4-173">Run the sample application using the following command through Visual Studio 2015 x86 Native Tools command prompt and navigate to the folder python/build_all/windows in your local copy of the repository:</span></span>
    
    <span data-ttu-id="5bea4-174">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-174">**If HTTP protocol:**</span></span>

        python iothub_client_sample.py -p http

    <span data-ttu-id="5bea4-175">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-175">**If MQTT protocol:**</span></span>

        python iothub_client_sample.py -p mqtt

    <span data-ttu-id="5bea4-176">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-176">**If AMQP protocol:**</span></span>

        python iothub_client_sample.py -p amqp

8. <span data-ttu-id="5bea4-177">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="5bea4-177">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="5bea4-178">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="5bea4-178">If not, then you may have incorrectly copied the device hub connection information.</span></span>
  
  <span data-ttu-id="5bea4-179">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-179">**If HTTP protocol:**</span></span> 
  
  ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_http.png)
  
  <span data-ttu-id="5bea4-181">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-181">**If MQTT protocol:**</span></span>
  
  ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_mqtt.png)
  
  <span data-ttu-id="5bea4-183">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-183">**If AMQP protocol:**</span></span>
  
  ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_amqp.png)
  
9. <span data-ttu-id="5bea4-185">应会看到 DeviceExplorer 的数据选项卡中收到的事件。</span><span class="sxs-lookup"><span data-stu-id="5bea4-185">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

    <span data-ttu-id="5bea4-186">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-186">**If HTTP protocol:**</span></span>   

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_http.png)

    <span data-ttu-id="5bea4-188">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-188">**If MQTT protocol:**</span></span>

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_mqtt.png)

    <span data-ttu-id="5bea4-190">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-190">**If AMQP protocol:**</span></span>
    
     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_amqp.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="5bea4-192">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="5bea4-192">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="5bea4-193">若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="5bea4-193">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="5bea4-194">使用“设备 ID”下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="5bea4-194">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="5bea4-195">在“消息”字段中添加一些文本，并单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="5bea4-195">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_message_receive_from_device_http.png)

4. <span data-ttu-id="5bea4-197">应会看到设备控制台窗口中收到的消息。</span><span class="sxs-lookup"><span data-stu-id="5bea4-197">You should be able to see the message received in the device console window.</span></span>
    
    <span data-ttu-id="5bea4-198">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-198">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

    <span data-ttu-id="5bea4-200">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-200">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_mqtt.png)

    <span data-ttu-id="5bea4-202">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="5bea4-202">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_amqp.png)
    
<a name="Step_4_Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="5bea4-204">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="5bea4-204">Step 4: Package and Share</span></span>

<a name="Step_4_1_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="5bea4-205">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="5bea4-205">4.1 Package build logs and sample test results</span></span>
  
<span data-ttu-id="5bea4-206">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="5bea4-206">Package the following artifacts from your device:</span></span>

1. <span data-ttu-id="5bea4-207">第 3.2 部分所述的生成日志。</span><span class="sxs-lookup"><span data-stu-id="5bea4-207">Build logs from section 3.2.</span></span>

2. <span data-ttu-id="5bea4-208">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="5bea4-208">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3. <span data-ttu-id="5bea4-209">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="5bea4-209">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>

4. <span data-ttu-id="5bea4-210">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="5bea4-210">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span>

> <span data-ttu-id="5bea4-211">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-python.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="5bea4-211">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-python.md>) to create your device-specific instructions.</span></span>
    
> <span data-ttu-id="5bea4-212">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="5bea4-212">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a><span data-ttu-id="5bea4-213">4.2 与 Azure IoT 认证团队共享包</span><span class="sxs-lookup"><span data-stu-id="5bea4-213">4.2 Share package with the Azure IoT Certification Team</span></span>

1.  <span data-ttu-id="5bea4-214">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="5bea4-214">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="5bea4-215">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="5bea4-215">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="5bea4-217">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="5bea4-217">This will open an upload dialog.</span></span> <span data-ttu-id="5bea4-218">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="5bea4-218">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="5bea4-220">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="5bea4-220">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="5bea4-221">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="5bea4-221">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="5bea4-222">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="5bea4-222">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3_Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="5bea4-223">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="5bea4-223">4.3 Next steps</span></span>

<span data-ttu-id="5bea4-224">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="5bea4-224">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="5bea4-225">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="5bea4-225">Step 5: Troubleshooting</span></span>

<span data-ttu-id="5bea4-226">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="5bea4-226">Please contact engineering support on <iotcert@microsoft.com> for help with  troubleshooting.</span></span>

