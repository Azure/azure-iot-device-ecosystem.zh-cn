<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a><span data-ttu-id="bacfe-101">如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="bacfe-101">How to certify IoT devices running Linux with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="bacfe-102">目录</span><span class="sxs-lookup"><span data-stu-id="bacfe-102">Table of Contents</span></span>

-   [<span data-ttu-id="bacfe-103">介绍</span><span class="sxs-lookup"><span data-stu-id="bacfe-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="bacfe-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bacfe-104">Step 1: Configure Azure IoT Hub</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="bacfe-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="bacfe-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="bacfe-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="bacfe-106">Step 3: Build and Validate the sample using C client libraries</span></span>](#Step-3-Build)
    -   [<span data-ttu-id="bacfe-107">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="bacfe-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Step-3-1-Load)
    -   [<span data-ttu-id="bacfe-108">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="bacfe-108">3.2 Build the samples</span></span>](#Step-3-2-Build)
    -   [<span data-ttu-id="bacfe-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="bacfe-109">3.3 Run and Validate the Samples</span></span>](#Step-3-3-Run)
-   [<span data-ttu-id="bacfe-110">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="bacfe-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="bacfe-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="bacfe-111">4.1 Package build logs and sample test results</span></span>](#Step-4-1-Package)
    -   [<span data-ttu-id="bacfe-112">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="bacfe-112">4.2 Share package with Engineering Support</span></span>](#Step-4-2-Share)
    -   [<span data-ttu-id="bacfe-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="bacfe-113">4.3 Next steps</span></span>](#Step-4-3-Next)
-   [<span data-ttu-id="bacfe-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="bacfe-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="bacfe-115">介绍</span><span class="sxs-lookup"><span data-stu-id="bacfe-115">Introduction</span></span>

<span data-ttu-id="bacfe-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="bacfe-116">**About this document**</span></span>

<span data-ttu-id="bacfe-117">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="bacfe-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="bacfe-118">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="bacfe-118">This multi-step process includes:</span></span>

-   <span data-ttu-id="bacfe-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bacfe-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="bacfe-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="bacfe-120">Registering your IoT device</span></span>
-   <span data-ttu-id="bacfe-121">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="bacfe-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="bacfe-122">打包和共享日志</span><span class="sxs-lookup"><span data-stu-id="bacfe-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="bacfe-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="bacfe-123">**Prepare**</span></span>

<span data-ttu-id="bacfe-124">在执行以下任何步骤之前，请先仔细阅读每个过程的每个步骤，确保对整个过程有全面的了解。</span><span class="sxs-lookup"><span data-stu-id="bacfe-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="bacfe-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="bacfe-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="bacfe-126">一台装有 GitHub 的计算机，并且能够访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 公共存储库。</span><span class="sxs-lookup"><span data-stu-id="bacfe-126">Computer with GitHub installed and access to the [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub public repository.</span></span>
-   <span data-ttu-id="bacfe-127">用于访问命令行的 SSH 客户端，例如 [PuTTY](http://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="bacfe-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="bacfe-128">需要认证的硬件。</span><span class="sxs-lookup"><span data-stu-id="bacfe-128">Required hardware to certify.</span></span>

<span data-ttu-id="bacfe-129">***注意：***如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://catalog.azureiotsuite.com/>)请求此身份，然后遵照本文中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="bacfe-129">***Note:*** *If you haven't contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://catalog.azureiotsuite.com/>) first to request it and then follow these instructions.*</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="bacfe-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bacfe-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="bacfe-131">遵照[此处](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub)所述的说明[注册](https://account.windowsazure.com/signup?offer=ms-azr-0044p) Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="bacfe-131">[Sign up](https://account.windowsazure.com/signup?offer=ms-azr-0044p) to the Azure IoT Hub service and follow the instructions mentioned [here](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub).</span></span> <span data-ttu-id="bacfe-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bacfe-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="bacfe-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="bacfe-133">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="bacfe-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="bacfe-134">Step 2: Register Device</span></span>

<span data-ttu-id="bacfe-135">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="bacfe-135">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="bacfe-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="bacfe-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="bacfe-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="bacfe-137">Device management</span></span>
    -   <span data-ttu-id="bacfe-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="bacfe-138">Create new devices</span></span>
    -   <span data-ttu-id="bacfe-139">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="bacfe-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="bacfe-140">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="bacfe-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="bacfe-141">提供删除设备的功能</span><span class="sxs-lookup"><span data-stu-id="bacfe-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="bacfe-142">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="bacfe-142">Monitoring events from your device</span></span>
-   <span data-ttu-id="bacfe-143">将消息发送到设备</span><span class="sxs-lookup"><span data-stu-id="bacfe-143">Sending messages to your device</span></span>

<span data-ttu-id="bacfe-144">若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step-1-Configure) 中所述的以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="bacfe-144">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step-1-Configure):</span></span>

-   <span data-ttu-id="bacfe-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="bacfe-145">IoT Hub Connection String</span></span>


<span data-ttu-id="bacfe-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="bacfe-146">**Steps:**</span></span>
1.  <span data-ttu-id="bacfe-147">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="bacfe-147">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="bacfe-148">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="bacfe-148">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="bacfe-149">使用以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="bacfe-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="bacfe-150">a.</span><span class="sxs-lookup"><span data-stu-id="bacfe-150">a.</span></span> <span data-ttu-id="bacfe-151">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="bacfe-151">Click the **Management** tab.</span></span>

    <span data-ttu-id="bacfe-152">b.</span><span class="sxs-lookup"><span data-stu-id="bacfe-152">b.</span></span> <span data-ttu-id="bacfe-153">列表中会显示已注册的设备。</span><span class="sxs-lookup"><span data-stu-id="bacfe-153">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="bacfe-154">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="bacfe-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="bacfe-155">如果这是第一次执行此操作，则不应检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="bacfe-155">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="bacfe-156">c.</span><span class="sxs-lookup"><span data-stu-id="bacfe-156">c.</span></span> <span data-ttu-id="bacfe-157">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="bacfe-157">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="bacfe-158">d.</span><span class="sxs-lookup"><span data-stu-id="bacfe-158">d.</span></span> <span data-ttu-id="bacfe-159">成功创建后，设备会列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="bacfe-159">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="bacfe-160">e.</span><span class="sxs-lookup"><span data-stu-id="bacfe-160">e.</span></span> <span data-ttu-id="bacfe-161">右键单击该设备，并从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="bacfe-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="bacfe-162">f.</span><span class="sxs-lookup"><span data-stu-id="bacfe-162">f.</span></span> <span data-ttu-id="bacfe-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="bacfe-163">Save this information in Notepad.</span></span> <span data-ttu-id="bacfe-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="bacfe-164">You will need this information in later steps.</span></span>

<span data-ttu-id="bacfe-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="bacfe-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="bacfe-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="bacfe-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step-3-Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="bacfe-167">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="bacfe-167">Step 3: Build and Validate the sample using C client libraries</span></span>

<span data-ttu-id="bacfe-168">本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="bacfe-168">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Linux operating system.</span></span> <span data-ttu-id="bacfe-169">我们将在设备上安装所需的必备组件。</span><span class="sxs-lookup"><span data-stu-id="bacfe-169">You will install necessary prerequisites on your device.</span></span> <span data-ttu-id="bacfe-170">完成后，将会生成并部署 IoT 客户端 SDK，并使用 Azure IoT SDK 来验证 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="bacfe-170">Once done, you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step-3-1-Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="bacfe-171">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="bacfe-171">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="bacfe-172">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="bacfe-172">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="bacfe-173">通过设备上的命令行发出以下命令，安装必备的包。</span><span class="sxs-lookup"><span data-stu-id="bacfe-173">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span> <span data-ttu-id="bacfe-174">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="bacfe-174">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="bacfe-175">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="bacfe-175">**Debian or Ubuntu**</span></span>

        sudo apt-get update

        sudo apt-get install -y curl uuid-dev libcurl4-openssl-dev build-essential cmake git

    <span data-ttu-id="bacfe-176">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="bacfe-176">**Fedora**</span></span>

        sudo dnf check-update -y

        sudo dnf install uuid-devel libcurl-devel openssl-devel gcc-c++ make cmake git

    <span data-ttu-id="bacfe-177">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="bacfe-177">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

    <span data-ttu-id="bacfe-178">***注意：***此安装过程需要 cmake 2.8.12 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="bacfe-178">***Note:*** *This setup process requires cmake version 2.8.12 or higher.*</span></span> 
    
    <span data-ttu-id="bacfe-179">可使用以下命令来验证环境中当前安装的版本：</span><span class="sxs-lookup"><span data-stu-id="bacfe-179">*You can verify the current version installed in your environment using the  following command:*</span></span>

        cmake --version

    <span data-ttu-id="bacfe-180">此库还需要 gcc 4.9 或更高版本。可使用以下命令来验证环境中当前安装的版本：</span><span class="sxs-lookup"><span data-stu-id="bacfe-180">*This library also requires gcc version 4.9 or higher. You can verify the current version installed in your environment using the following command:*</span></span>
    
        gcc --version 

    <span data-ttu-id="bacfe-181">有关如何升级 Ubuntu 14.04 上的 gcc 版本的信息，请参阅 <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>。</span><span class="sxs-lookup"><span data-stu-id="bacfe-181">*For information about how to upgrade your version of gcc on Ubuntu 14.04, see <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>.*</span></span>
    
-   <span data-ttu-id="bacfe-182">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="bacfe-182">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-c.git

-   <span data-ttu-id="bacfe-183">检查 ~/azure-iot-sdk-c 目录下现在是否包含源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="bacfe-183">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-c.</span></span>

<a name="Step-3-2-Build"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="bacfe-184">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="bacfe-184">3.2 Build the samples</span></span>

<span data-ttu-id="bacfe-185">有两个示例：一个用于向 IoT 中心发送消息，另一个用于从 IoT 中心接收消息。</span><span class="sxs-lookup"><span data-stu-id="bacfe-185">There are two samples one for sending messages to IoT Hub and another for receiving messages from IoT Hub.</span></span> <span data-ttu-id="bacfe-186">这两个示例支持不同的协议。</span><span class="sxs-lookup"><span data-stu-id="bacfe-186">Both samples supports different protocols.</span></span> <span data-ttu-id="bacfe-187">在生成示例之前，可以使用所选的协议对示例示例进行修改。</span><span class="sxs-lookup"><span data-stu-id="bacfe-187">You can make modification to the samples with your choice of protocol before building the samples.</span></span> <span data-ttu-id="bacfe-188">默认情况下，将会针对 AMQP 协议生成示例。</span><span class="sxs-lookup"><span data-stu-id="bacfe-188">By default the samples will build for AMQP protocol.</span></span>  <span data-ttu-id="bacfe-189">在生成之前，遵照以下说明编辑示例：</span><span class="sxs-lookup"><span data-stu-id="bacfe-189">Follow the below instructions to edit the samples before building:</span></span> 
    
### <a name="321-send-telemetry-to-iot-hub-sample"></a><span data-ttu-id="bacfe-190">3.2.1：向 IoT 中心示例发送遥测数据：</span><span class="sxs-lookup"><span data-stu-id="bacfe-190">3.2.1 Send Telemetry to IoT Hub Sample:</span></span>

1.  <span data-ttu-id="bacfe-191">在文本编辑器中打开遥测示例文件</span><span class="sxs-lookup"><span data-stu-id="bacfe-191">Open the telemetry sample file in a text editor</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_ll_telemetry_sample/iothub_ll_telemetry_sample.c     

2. <span data-ttu-id="bacfe-192">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="bacfe-192">Find the following placeholder for IoT connection string:</span></span>

        static const char* connectionString = "[device connection string]";

3. <span data-ttu-id="bacfe-193">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bacfe-193">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="bacfe-194">可根据[步骤 2](#Step-2-Register) 中所述，从 DeviceExplorer 获取已复制到记事本中的此字符串。</span><span class="sxs-lookup"><span data-stu-id="bacfe-194">You can get this from DeviceExplorer as explained in [Step 2](#Step-2-Register), that you copied into Notepad.</span></span>
    
4. <span data-ttu-id="bacfe-195">找到以下占位符以编辑协议：</span><span class="sxs-lookup"><span data-stu-id="bacfe-195">Find the following place holder for editing protocol:</span></span>

        // The protocol you wish to use should be uncommented
        //
        #define SAMPLE_HTTP
        //#define SAMPLE_MQTT
        //#define SAMPLE_MQTT_OVER_WEBSOCKETS
        //#define SAMPLE_AMQP
        //#define SAMPLE_AMQP_OVER_WEBSOCKETS
    
5. <span data-ttu-id="bacfe-196">取消注释要测试的协议，并注释其他协议。</span><span class="sxs-lookup"><span data-stu-id="bacfe-196">Please uncomment the protocol that you would like to test with and comment other protocols.</span></span> <span data-ttu-id="bacfe-197">若要测试多个协议，请对每个协议重复上述步骤。</span><span class="sxs-lookup"><span data-stu-id="bacfe-197">If testing for multiple protocols, please repeat above step for each protocol.</span></span> 

6. <span data-ttu-id="bacfe-198">按 Ctrl+O 保存更改，当 nano 提示是否保存为同一文件时，请按 ENTER。</span><span class="sxs-lookup"><span data-stu-id="bacfe-198">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

7. <span data-ttu-id="bacfe-199">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="bacfe-199">Press Ctrl+X to exit nano.</span></span>

### <a name="321-send-message-from-iot-hub-to-device-sample"></a><span data-ttu-id="bacfe-200">3.2.1：将消息从 IoT 中心发送到设备示例：</span><span class="sxs-lookup"><span data-stu-id="bacfe-200">3.2.1 Send message from IoT Hub to Device Sample:</span></span>

1.  <span data-ttu-id="bacfe-201">在文本编辑器中打开遥测示例文件</span><span class="sxs-lookup"><span data-stu-id="bacfe-201">Open the telemetry sample file in a text editor</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_ll_c2d_sample/iothub_ll_c2d_sample.c
        
2.  <span data-ttu-id="bacfe-202">遵循上述步骤 1-7 编辑此示例。</span><span class="sxs-lookup"><span data-stu-id="bacfe-202">Follow same steps 1-7 as above to edit this sample.</span></span>

### <a name="321-build-the-samples"></a><span data-ttu-id="bacfe-203">3.2.1：生成示例：</span><span class="sxs-lookup"><span data-stu-id="bacfe-203">3.2.1 Build the samples:</span></span>

1.  <span data-ttu-id="bacfe-204">使用以下命令生成 SDK。</span><span class="sxs-lookup"><span data-stu-id="bacfe-204">Build the SDK using following command.</span></span> <span data-ttu-id="bacfe-205">如果在生成期间遇到任何问题，请遵循故障排除[步骤 5](#Step-5-Troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="bacfe-205">If you are facing any issues during build, follow troubleshooting [Step 5](#Step-5-Troubleshooting).</span></span>

        sudo ./azure-iot-sdk-c/build_all/linux/build.sh | tee LogFile.txt
    
    <span data-ttu-id="bacfe-206">***注意：***应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。</span><span class="sxs-lookup"><span data-stu-id="bacfe-206">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>
    
    <span data-ttu-id="bacfe-207">build.sh 在“~/azure-iot-sdk-c/”下创建名为“cmake”的文件夹。“cmake”中包含整个软件的所有编译结果。</span><span class="sxs-lookup"><span data-stu-id="bacfe-207">*build.sh creates a folder called "cmake" under "~/azure-iot-sdk-c/". Inside "cmake" are all the results of the compilation of the complete software.*</span></span>


<a name="Step-3-3-Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="bacfe-208">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="bacfe-208">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="bacfe-209">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="bacfe-209">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="bacfe-210">我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="bacfe-210">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="bacfe-211">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="bacfe-211">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="bacfe-212">**注意：**请对本部分中执行的所有操作截图。</span><span class="sxs-lookup"><span data-stu-id="bacfe-212">**Note:** Take screenshots of all the operations you will perform in this section.</span></span> <span data-ttu-id="bacfe-213">在[步骤 4](#Step-4-2-Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bacfe-213">These will be needed in [Step 4](#Step-4-2-Share)</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="bacfe-214">3.3.1：向 IOT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="bacfe-214">3.3.1 Send Device Events to IOT Hub:</span></span>

1.  <span data-ttu-id="bacfe-215">如[步骤 2](#Step-2-Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="bacfe-215">Launch the DeviceExplorer as explained in [Step 2](#Step-2-Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="bacfe-217">DeviceExplorer 现在正在监视从所选设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="bacfe-217">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="bacfe-218">发出以下命令运行示例。</span><span class="sxs-lookup"><span data-stu-id="bacfe-218">Run the sample by issuing following command.</span></span>    

        azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_ll_telemetry_sample/iothub_ll_telemetry_sample

4.  <span data-ttu-id="bacfe-219">检查确认消息中是否显示了“OK”。</span><span class="sxs-lookup"><span data-stu-id="bacfe-219">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="bacfe-220">如果没有，则可能是错误地复制了设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="bacfe-220">If not, then you may have incorrectly copied the device hub connection information.</span></span>

    ![SampleAMQP\_result\_terminal](images/3_3_1_02.png)    

5.  <span data-ttu-id="bacfe-222">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="bacfe-222">DeviceExplorer should show that IoTHub has successfully received data sent by sample test.</span></span>

    ![Sample\_result\_DeviceExplorer](images/3_3_1_04.png)    

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="bacfe-224">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="bacfe-224">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="bacfe-225">发出以下命令运行示例。</span><span class="sxs-lookup"><span data-stu-id="bacfe-225">Run the sample by issuing following command.</span></span>

        azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_ll_c2d_sample/iothub_ll_c2d_sample
        
2. <span data-ttu-id="bacfe-226">若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="bacfe-226">To verify that you can send messages from the IoT Hub to your device,  go to the **Message To Device** tab in DeviceExplorer.</span></span>

3.  <span data-ttu-id="bacfe-227">使用“设备 ID”下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="bacfe-227">Select the device you created using Device ID drop down.</span></span>

4.  <span data-ttu-id="bacfe-228">在“消息”字段中添加一些文本，并单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="bacfe-228">Add some text to the Message field, then click Send.</span></span>

    ![MessageSend\_DeviceExplorer](images/3_3_1_06.png)

5.  <span data-ttu-id="bacfe-230">应会看到客户端示例控制台窗口中收到的命令。</span><span class="sxs-lookup"><span data-stu-id="bacfe-230">You should be able to see the command received in the console window for the client sample.</span></span>

    ![MessageSend\_terminal](images/3_3_1_07.png)
    
<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="bacfe-232">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="bacfe-232">Step 4: Package and Share</span></span>

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="bacfe-233">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="bacfe-233">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="bacfe-234">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="bacfe-234">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="bacfe-235">在生成运行期间记录在日志文件中的生成日志。</span><span class="sxs-lookup"><span data-stu-id="bacfe-235">Build logs that were logged in the log files during build run.</span></span>

2.  <span data-ttu-id="bacfe-236">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bacfe-236">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="bacfe-237">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bacfe-237">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="bacfe-238">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="bacfe-238">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="bacfe-239">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="bacfe-239">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="bacfe-240">有关说明的大致形式的指导，请参阅[此](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="bacfe-240">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a><span data-ttu-id="bacfe-241">4.2：与 Microsoft Azure IoT 团队成员共享包</span><span class="sxs-lookup"><span data-stu-id="bacfe-241">4.2 Share package with Microsoft Azure IoT team</span></span>

1.  <span data-ttu-id="bacfe-242">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="bacfe-242">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="bacfe-243">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="bacfe-243">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="bacfe-245">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="bacfe-245">This will open an upload dialog.</span></span> <span data-ttu-id="bacfe-246">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="bacfe-246">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="bacfe-248">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="bacfe-248">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="bacfe-249">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="bacfe-249">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="bacfe-250">***注意：***提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。</span><span class="sxs-lookup"><span data-stu-id="bacfe-250">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="bacfe-251">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="bacfe-251">4.3 Next steps</span></span>

<span data-ttu-id="bacfe-252">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="bacfe-252">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="bacfe-253">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="bacfe-253">Step 5: Troubleshooting</span></span>

<span data-ttu-id="bacfe-254">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="bacfe-254">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>