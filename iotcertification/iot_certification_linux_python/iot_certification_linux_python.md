<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a><span data-ttu-id="05ddc-101">如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="05ddc-101">How to certify IoT devices running Linux with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="05ddc-102">目录</span><span class="sxs-lookup"><span data-stu-id="05ddc-102">Table of Contents</span></span>

-   [<span data-ttu-id="05ddc-103">简介</span><span class="sxs-lookup"><span data-stu-id="05ddc-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="05ddc-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="05ddc-104">Step 1: Configure Azure IoT Hub</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="05ddc-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="05ddc-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="05ddc-106">步骤 3：使用 Python 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="05ddc-106">Step 3: Build and Validate the sample using Python client libraries</span></span>](#Step-3-Build)
    -   [<span data-ttu-id="05ddc-107">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="05ddc-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Step-3-1-Load)
    -   [<span data-ttu-id="05ddc-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="05ddc-108">3.2 Build the samples</span></span>](#Step-3-2-Build)
    -   [<span data-ttu-id="05ddc-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="05ddc-109">3.3 Run and Validate the Samples</span></span>](#Step-3-3-Run)
-   [<span data-ttu-id="05ddc-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="05ddc-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="05ddc-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="05ddc-111">4.1 Package build logs and sample test results</span></span>](#Step-4-1-Package)
    -   [<span data-ttu-id="05ddc-112">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="05ddc-112">4.2 Share package with Engineering Support</span></span>](#Step-4-2-Share)
    -   [<span data-ttu-id="05ddc-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="05ddc-113">4.3 Next steps</span></span>](#Step-4-3-Next)
-   [<span data-ttu-id="05ddc-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="05ddc-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="05ddc-115">简介</span><span class="sxs-lookup"><span data-stu-id="05ddc-115">Introduction</span></span>

<span data-ttu-id="05ddc-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="05ddc-116">**About this document**</span></span>

<span data-ttu-id="05ddc-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="05ddc-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="05ddc-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="05ddc-118">This multi-step process includes:</span></span>
-   <span data-ttu-id="05ddc-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="05ddc-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="05ddc-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="05ddc-120">Registering your IoT device</span></span>
-   <span data-ttu-id="05ddc-121">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="05ddc-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="05ddc-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="05ddc-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="05ddc-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="05ddc-123">**Prepare**</span></span>

<span data-ttu-id="05ddc-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="05ddc-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="05ddc-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="05ddc-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="05ddc-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-python](https://github.com/Azure/azure-iot-sdk-python) GitHub 专用存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="05ddc-126">Computer with GitHub installed and access to the [azure-iot-sdk-python](https://github.com/Azure/azure-iot-sdk-python) GitHub private repository.</span></span>
-   <span data-ttu-id="05ddc-127">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="05ddc-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="05ddc-128">需要认证的硬件。</span><span class="sxs-lookup"><span data-stu-id="05ddc-128">Required hardware to certify.</span></span>

<span data-ttu-id="05ddc-129">\*\**注意：\*\*\*\*如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://iotcert.cloudapp.net/>)请求此身份，然后遵照本文中的说明操作。*</span><span class="sxs-lookup"><span data-stu-id="05ddc-129">***Note:*** *If you haven't contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://iotcert.cloudapp.net/>) first to request it and then follow these instructions.*</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="05ddc-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="05ddc-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="05ddc-131">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="05ddc-131">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span> <span data-ttu-id="05ddc-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="05ddc-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="05ddc-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="05ddc-133">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="05ddc-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="05ddc-134">Step 2: Register Device</span></span>

-   <span data-ttu-id="05ddc-135">遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)所述的说明，了解如何预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="05ddc-135">Follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) on how to provision your device and get its credentials.</span></span>

<a name="Step-3-Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-python-libraries"></a><span data-ttu-id="05ddc-136">步骤 3：使用 Python 库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="05ddc-136">Step 3: Build and Validate the sample using Python libraries</span></span>

<span data-ttu-id="05ddc-137">本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="05ddc-137">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Linux operating system.</span></span> <span data-ttu-id="05ddc-138">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="05ddc-138">You will install necessary prerequisites on your device.</span></span> <span data-ttu-id="05ddc-139">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="05ddc-139">Once done, you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step-3-1-Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="05ddc-140">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="05ddc-140">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="05ddc-141">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="05ddc-141">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="05ddc-142">在设备上的命令行中发出以下命令，安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="05ddc-142">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span> <span data-ttu-id="05ddc-143">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="05ddc-143">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="05ddc-144">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="05ddc-144">**Debian or Ubuntu**</span></span>

        sudo apt-get update

        sudo apt-get install -y curl libcurl4-openssl-dev build-essential cmake git python2.7-dev libboost-python-dev

    <span data-ttu-id="05ddc-145">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="05ddc-145">**Fedora**</span></span>

        sudo dnf check-update -y

        sudo dnf install libcurl-devel openssl-devel gcc-c++ make cmake git python2.7-dev libboost-python-dev

    <span data-ttu-id="05ddc-146">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="05ddc-146">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

    <span data-ttu-id="05ddc-147">***注意：*** 此安装过程需要 cmake 2.8.12 版或更高版本。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-147">***Note:*** *This setup process requires cmake version 2.8.12 or higher.*</span></span> 
    
    <span data-ttu-id="05ddc-148">可使用以下命令来验证环境中当前安装的版本： </span><span class="sxs-lookup"><span data-stu-id="05ddc-148">*You can verify the current version installed in your environment using the  following command:*</span></span>

        cmake --version

    <span data-ttu-id="05ddc-149">*此库还需要 gcc 4.9 或更高版本。* 可使用以下命令来验证环境中当前安装的版本：</span><span class="sxs-lookup"><span data-stu-id="05ddc-149">*This library also requires gcc version 4.9 or higher. You can verify the current version installed in your environment using the following command:*</span></span>
    
        gcc --version 

    <span data-ttu-id="05ddc-150">有关如何升级 Ubuntu 14.04 上的 gcc 版本的信息，请参阅 <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-150">*For information about how to upgrade your version of gcc on Ubuntu 14.04, see <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>.*</span></span>

    <span data-ttu-id="05ddc-151">*此库还需要 Python 版本 2.7.x。可以使用以下命令确认环境中当前安装的版本：*</span><span class="sxs-lookup"><span data-stu-id="05ddc-151">*This library also requires Python version 2.7.x. You can verify the current version installed in your environment using the following command:*</span></span>
    
          python --version

-   <span data-ttu-id="05ddc-152">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="05ddc-152">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-python.git

-   <span data-ttu-id="05ddc-153">验证 ~/azure-iot-sdk-python 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="05ddc-153">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-python.</span></span>

<a name="Step-3-2-Build"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="05ddc-154">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="05ddc-154">3.2 Build the samples</span></span>

-   <span data-ttu-id="05ddc-155">运行以下命令生成 SDK：</span><span class="sxs-lookup"><span data-stu-id="05ddc-155">Run following commands to build the SDK:</span></span>

        cd python/build_all/linux
        sudo ./build.sh | tee LogFile.txt

    <span data-ttu-id="05ddc-156">***注意：*** 应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-156">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>

-   <span data-ttu-id="05ddc-157">成功生成后，`iothub_client.so` Python 扩展模块将复制到 **python/device/samples** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="05ddc-157">After a successful build, the `iothub_client.so` Python extension module is copied to the **python/device/samples** folder.</span></span>


<a name="Step-3-3-Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="05ddc-158">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="05ddc-158">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="05ddc-159">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="05ddc-159">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="05ddc-160">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="05ddc-160">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="05ddc-161">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="05ddc-161">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

-   <span data-ttu-id="05ddc-162">执行以下命令导航到 samples 文件夹：</span><span class="sxs-lookup"><span data-stu-id="05ddc-162">Navigate to samples folder by executing following command:</span></span>

        cd azure-iot-sdk-python/device/samples/

-   <span data-ttu-id="05ddc-163">在设备上运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="05ddc-163">Run the following command on the device:</span></span>

        nano iothub_client_sample.py

-   <span data-ttu-id="05ddc-164">此时会启动基于控制台的文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="05ddc-164">This launches a console-based text editor.</span></span> <span data-ttu-id="05ddc-165">向下滚动到连接信息。</span><span class="sxs-lookup"><span data-stu-id="05ddc-165">Scroll down to the connection information.</span></span>

-   <span data-ttu-id="05ddc-166">找到设备连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="05ddc-166">Find the following place holder for device connection string:</span></span>

        connectionString = "[device connection string]"

-   <span data-ttu-id="05ddc-167">将上述占位符替换为在[步骤 2](#Step-2-Register) 中获取的设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="05ddc-167">Replace the above placeholder with device connection string you got in [Step 2](#Step-2-Register).</span></span>

-   <span data-ttu-id="05ddc-168">按 Ctrl+O 保存更改，当 nano 提示是否保存到同一文件时，按 ENTER 即可。</span><span class="sxs-lookup"><span data-stu-id="05ddc-168">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

-   <span data-ttu-id="05ddc-169">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="05ddc-169">Press Ctrl+X to exit nano.</span></span>

<span data-ttu-id="05ddc-170">**注意：** 请对本部分中执行的所有操作进行屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="05ddc-170">**Note:** Take screenshots of all the operations you will perform in this section.</span></span> <span data-ttu-id="05ddc-171">在[步骤 4](#Step-4-2-Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="05ddc-171">These will be needed in [Step 4](#Step-4-2-Share)</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="05ddc-172">3.3.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="05ddc-172">3.3.1 Send Device Events to IOT Hub:</span></span>

-   <span data-ttu-id="05ddc-173">使用以下命令运行示例应用程序：</span><span class="sxs-lookup"><span data-stu-id="05ddc-173">Run the sample application using the following command:</span></span>

    <span data-ttu-id="05ddc-174">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-174">**For AMQP protocol:**</span></span>

        python iothub_client_sample.py -p amqp

    <span data-ttu-id="05ddc-175">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-175">**For HTTP protocol:**</span></span>

        python iothub_client_sample.py -p http

    <span data-ttu-id="05ddc-176">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-176">**For MQTT protocol:**</span></span>

        python iothub_client_sample.py -p mqtt

-   <span data-ttu-id="05ddc-177">请参阅[管理 IoT 中心](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="05ddc-177">See [Manage IoT Hub](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to learn how to observe the messages IoT Hub receives from the application.</span></span>

-   <span data-ttu-id="05ddc-178">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="05ddc-178">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="05ddc-179">如果没有，则可能表示未正确复制设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="05ddc-179">If not, then you may have incorrectly copied the device connection string.</span></span>

    <span data-ttu-id="05ddc-180">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-180">**If using AMQP protocol:**</span></span>
    
    ![SampleAMQP\_result\_terminal](images/python_amqp_send_message_device.png)

    <span data-ttu-id="05ddc-182">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-182">**If using HTTP protocol:**</span></span>
    
    ![SampleHTTP\_result\_terminal](images/python_http_send_message_device.png)

    <span data-ttu-id="05ddc-184">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-184">**If using MQTT protocol:**</span></span>
    
    ![SampleMQTT\_result\_terminal](images/python_mqtt_send_message_device.png)

-   <span data-ttu-id="05ddc-186">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="05ddc-186">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="05ddc-187">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-187">**If using AMQP protocol:**</span></span>
    
    ![SampleAMQP\_result\_DeviceExplorer](images/python_amqp_send_message_device_explorer.png)

    <span data-ttu-id="05ddc-189">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-189">**If using HTTP protocol:**</span></span>
    
    ![SampleHTTP\_result\_DeviceExplorer](images/python_http_send_message_device_explorer.png)

    <span data-ttu-id="05ddc-191">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-191">**If using MQTT protocol:**</span></span>
    
    ![SampleMQTT\_result\_DeviceExplorer](images/python_mqtt_send_message_device_explorer.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="05ddc-193">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="05ddc-193">3.3.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="05ddc-194">请参阅[管理 IoT 中心](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="05ddc-194">See [Manage IoT Hub](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to learn how to send cloud-to-device messages to the application.</span></span>

-   <span data-ttu-id="05ddc-195">应会在客户端示例的控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="05ddc-195">You should be able to see the command received in the console window for the client sample.</span></span>

    <span data-ttu-id="05ddc-196">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-196">**If using AMQP protocol:**</span></span>
    
    ![MessageSend\_terminal](images/python_amqp_receive_message_device.png)

    <span data-ttu-id="05ddc-198">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-198">**If using HTTP protocol:**</span></span>
    
    ![MessageSend\_terminal](images/python_http_receive_message_device.png)

    <span data-ttu-id="05ddc-200">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="05ddc-200">**If using MQTT protocol:**</span></span>
    
    ![MessageSend\_terminal](images/python_mqtt_receive_message_device.png)

### <a name="333-verify-device-configuration"></a><span data-ttu-id="05ddc-202">3.3.3 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="05ddc-202">3.3.3 Verify Device configuration</span></span>

-   <span data-ttu-id="05ddc-203">在运行 `platform_data.py` 之前，请安装以下模块</span><span class="sxs-lookup"><span data-stu-id="05ddc-203">Please install the below modules before you run the `platform_data.py`</span></span>

    <span data-ttu-id="05ddc-204">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="05ddc-204">**Debian or Ubuntu**</span></span> 

        sudo apt-get install python-requests
        sudo apt-get install python-netifaces

    <span data-ttu-id="05ddc-205">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="05ddc-205">**Fedora**</span></span>

        sudo dnf install python-requests
        sudo dnf install python-netifaces

-   <span data-ttu-id="05ddc-206">通过执行以下命令导航到 tools 文件夹：</span><span class="sxs-lookup"><span data-stu-id="05ddc-206">Navigate to tools folder by executing following command:</span></span>

        cd azure-iot-sdk-python/Tools

-   <span data-ttu-id="05ddc-207">在设备上运行以下命令</span><span class="sxs-lookup"><span data-stu-id="05ddc-207">Run the following command on the device</span></span>
        
        python platform_data.py

    ![deviceinfo\_screenshot](images/python_modified_output.PNG)

-   <span data-ttu-id="05ddc-209">请保存设备配置屏幕截图，然后按[步骤 4](#Step-4-1-Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="05ddc-209">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Step-4-1-Package).</span></span>

<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="05ddc-210">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="05ddc-210">Step 4: Package and Share</span></span>

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="05ddc-211">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="05ddc-211">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="05ddc-212">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="05ddc-212">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="05ddc-213">在生成运行期间记录在日志文件中的生成日志。</span><span class="sxs-lookup"><span data-stu-id="05ddc-213">Build logs that were logged in the log files during build run.</span></span>

2.  <span data-ttu-id="05ddc-214">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-214">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="05ddc-215">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-215">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="05ddc-216">前面“设备配置”  部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="05ddc-216">All the screenshots that are above in "**Device Configuration**" section.</span></span>

5.  <span data-ttu-id="05ddc-217">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="05ddc-217">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="05ddc-218">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-python.md>)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="05ddc-218">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-python.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="05ddc-219">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="05ddc-219">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a><span data-ttu-id="05ddc-220">4.2 与 Microsoft Azure IoT 团队共享包</span><span class="sxs-lookup"><span data-stu-id="05ddc-220">4.2 Share package with Microsoft Azure IoT team</span></span>

1.  <span data-ttu-id="05ddc-221">转到“[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)”。</span><span class="sxs-lookup"><span data-stu-id="05ddc-221">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="05ddc-222">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="05ddc-222">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="05ddc-224">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="05ddc-224">This will open an upload dialog.</span></span> <span data-ttu-id="05ddc-225">单击“上载”按钮浏览文件。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-225">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="05ddc-227">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="05ddc-227">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="05ddc-228">上传所有文件后，单击“提交审查”按钮。 </span><span class="sxs-lookup"><span data-stu-id="05ddc-228">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="05ddc-229">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="05ddc-229">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="05ddc-230">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="05ddc-230">4.3 Next steps</span></span>

<span data-ttu-id="05ddc-231">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="05ddc-231">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="05ddc-232">步骤 5：疑难解答</span><span class="sxs-lookup"><span data-stu-id="05ddc-232">Step 5: Troubleshooting</span></span>

<span data-ttu-id="05ddc-233">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="05ddc-233">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
