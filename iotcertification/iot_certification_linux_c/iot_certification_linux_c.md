<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a><span data-ttu-id="78e58-101">如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="78e58-101">How to certify IoT devices running Linux with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="78e58-102">目录</span><span class="sxs-lookup"><span data-stu-id="78e58-102">Table of Contents</span></span>

-   [<span data-ttu-id="78e58-103">介绍</span><span class="sxs-lookup"><span data-stu-id="78e58-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="78e58-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="78e58-104">Step 1: Configure Azure IoT Hub</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="78e58-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="78e58-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="78e58-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="78e58-106">Step 3: Build and Validate the sample using C client libraries</span></span>](#Step-3-Build)
    -   [<span data-ttu-id="78e58-107">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="78e58-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Step-3-1-Load)
    -   [<span data-ttu-id="78e58-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="78e58-108">3.2 Build the samples</span></span>](#Step-3-2-Build)
    -   [<span data-ttu-id="78e58-109">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="78e58-109">3.3 Run and Validate the Samples</span></span>](#Step-3-3-Run)
-   [<span data-ttu-id="78e58-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="78e58-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="78e58-111">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="78e58-111">4.1 Package build logs and sample test results</span></span>](#Step-4-1-Package)
    -   [<span data-ttu-id="78e58-112">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="78e58-112">4.2 Share package with Engineering Support</span></span>](#Step-4-2-Share)
    -   [<span data-ttu-id="78e58-113">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="78e58-113">4.3 Next steps</span></span>](#Step-4-3-Next)
-   [<span data-ttu-id="78e58-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="78e58-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="78e58-115">介绍</span><span class="sxs-lookup"><span data-stu-id="78e58-115">Introduction</span></span>

<span data-ttu-id="78e58-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="78e58-116">**About this document**</span></span>

<span data-ttu-id="78e58-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="78e58-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="78e58-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="78e58-118">This multi-step process includes:</span></span>

-   <span data-ttu-id="78e58-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="78e58-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="78e58-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="78e58-120">Registering your IoT device</span></span>
-   <span data-ttu-id="78e58-121">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="78e58-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="78e58-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="78e58-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="78e58-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="78e58-123">**Prepare**</span></span>

<span data-ttu-id="78e58-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="78e58-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="78e58-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="78e58-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="78e58-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="78e58-126">Computer with GitHub installed and access to the [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub public repository.</span></span>
-   <span data-ttu-id="78e58-127">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="78e58-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="78e58-128">用于认证的所需硬件。</span><span class="sxs-lookup"><span data-stu-id="78e58-128">Required hardware to certify.</span></span>

<span data-ttu-id="78e58-129">***注意：****如果你尚未咨询 Microsoft 如何成为 Azure 认证的 IoT 合作伙伴，请先提交此[表单](<https://catalog.azureiotsuite.com/>)来提出请求，然后遵照本文中的说明。*</span><span class="sxs-lookup"><span data-stu-id="78e58-129">***Note:*** *If you haven't contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://catalog.azureiotsuite.com/>) first to request it and then follow these instructions.*</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="78e58-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="78e58-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="78e58-131">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="78e58-131">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span> <span data-ttu-id="78e58-132">在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="78e58-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="78e58-133">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="78e58-133">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="78e58-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="78e58-134">Step 2: Register Device</span></span>

<span data-ttu-id="78e58-135">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="78e58-135">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="78e58-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="78e58-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="78e58-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="78e58-137">Device management</span></span>
    -   <span data-ttu-id="78e58-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="78e58-138">Create new devices</span></span>
    -   <span data-ttu-id="78e58-139">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="78e58-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="78e58-140">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="78e58-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="78e58-141">可删除设备</span><span class="sxs-lookup"><span data-stu-id="78e58-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="78e58-142">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="78e58-142">Monitoring events from your device</span></span>
-   <span data-ttu-id="78e58-143">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="78e58-143">Sending messages to your device</span></span>

<span data-ttu-id="78e58-144">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step-1-Configure) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="78e58-144">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step-1-Configure):</span></span>

-   <span data-ttu-id="78e58-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="78e58-145">IoT Hub Connection String</span></span>


<span data-ttu-id="78e58-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="78e58-146">**Steps:**</span></span>
1.  <span data-ttu-id="78e58-147">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="78e58-147">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="78e58-148">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="78e58-148">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="78e58-149">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="78e58-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="78e58-150">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="78e58-150">a.</span></span> <span data-ttu-id="78e58-151">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="78e58-151">Click the **Management** tab.</span></span>

    <span data-ttu-id="78e58-152">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="78e58-152">b.</span></span> <span data-ttu-id="78e58-153">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="78e58-153">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="78e58-154">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="78e58-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="78e58-155">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="78e58-155">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="78e58-156">c.</span><span class="sxs-lookup"><span data-stu-id="78e58-156">c.</span></span> <span data-ttu-id="78e58-157">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="78e58-157">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="78e58-158">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="78e58-158">d.</span></span> <span data-ttu-id="78e58-159">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="78e58-159">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="78e58-160">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="78e58-160">e.</span></span> <span data-ttu-id="78e58-161">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="78e58-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="78e58-162">f.</span><span class="sxs-lookup"><span data-stu-id="78e58-162">f.</span></span> <span data-ttu-id="78e58-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="78e58-163">Save this information in Notepad.</span></span> <span data-ttu-id="78e58-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="78e58-164">You will need this information in later steps.</span></span>

<span data-ttu-id="78e58-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="78e58-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="78e58-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="78e58-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step-3-Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="78e58-167">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="78e58-167">Step 3: Build and Validate the sample using C client libraries</span></span>

<span data-ttu-id="78e58-168">本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="78e58-168">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Linux operating system.</span></span> <span data-ttu-id="78e58-169">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="78e58-169">You will install necessary prerequisites on your device.</span></span> <span data-ttu-id="78e58-170">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="78e58-170">Once done, you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step-3-1-Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="78e58-171">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="78e58-171">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="78e58-172">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="78e58-172">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="78e58-173">在设备上的命令行中发出以下命令，安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="78e58-173">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span> <span data-ttu-id="78e58-174">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="78e58-174">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="78e58-175">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="78e58-175">**Debian or Ubuntu**</span></span>

        sudo apt-get update

        sudo apt-get install -y curl uuid-dev libcurl4-openssl-dev build-essential cmake git

    <span data-ttu-id="78e58-176">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="78e58-176">**Fedora**</span></span>

        sudo dnf check-update -y

        sudo dnf install uuid-devel libcurl-devel openssl-devel gcc-c++ make cmake git

    <span data-ttu-id="78e58-177">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="78e58-177">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

    <span data-ttu-id="78e58-178">***注意：****此安装过程需要 cmake 2.8.12 或更高版本。*</span><span class="sxs-lookup"><span data-stu-id="78e58-178">***Note:*** *This setup process requires cmake version 2.8.12 or higher.*</span></span> 
    
    <span data-ttu-id="78e58-179">*可以使用以下命令确认环境中当前安装的版本：*</span><span class="sxs-lookup"><span data-stu-id="78e58-179">*You can verify the current version installed in your environment using the  following command:*</span></span>

        cmake --version

    <span data-ttu-id="78e58-180">*此库还需要 gcc 4.9 或更高版本。可以使用以下命令确认环境中当前安装的版本：*</span><span class="sxs-lookup"><span data-stu-id="78e58-180">*This library also requires gcc version 4.9 or higher. You can verify the current version installed in your environment using the following command:*</span></span>
    
        gcc --version 

    <span data-ttu-id="78e58-181">*有关如何在 Ubuntu 14.04 上升级 gcc 版本的信息，请参阅 <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>。*</span><span class="sxs-lookup"><span data-stu-id="78e58-181">*For information about how to upgrade your version of gcc on Ubuntu 14.04, see <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>.*</span></span>
    
-   <span data-ttu-id="78e58-182">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="78e58-182">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-c.git

-   <span data-ttu-id="78e58-183">验证 ~/azure-iot-sdk-c 目录中现在是否生成了源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="78e58-183">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-c.</span></span>

<a name="Step-3-2-Build"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="78e58-184">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="78e58-184">3.2 Build the samples</span></span>

-   <span data-ttu-id="78e58-185">有两个不同的示例，一个支持 AMQP 协议，另一个支持 HTTP 协议。</span><span class="sxs-lookup"><span data-stu-id="78e58-185">There are two different samples available, one supporting AMQP protocol and other supporting HTTP protocol.</span></span> <span data-ttu-id="78e58-186">可以使用其中的任一协议在设备上验证示例。</span><span class="sxs-lookup"><span data-stu-id="78e58-186">You can use either of these protocols to validate a sample on your device.</span></span> <span data-ttu-id="78e58-187">根据选择的协议，在设备上运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="78e58-187">Based on your choice of protocol, run the following command on device.</span></span>

    <span data-ttu-id="78e58-188">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="78e58-188">**For AMQP protocol:**</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp.c

    <span data-ttu-id="78e58-189">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="78e58-189">**For HTTP protocol:**</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http.c

    <span data-ttu-id="78e58-190">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="78e58-190">**For MQTT protocol:**</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_mqtt/iothub_client_sample_mqtt.c

    <span data-ttu-id="78e58-191">**对于将 WebSocket 与 AMQP 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="78e58-191">**For WebSocket with AMQP protocol:**</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_amqp_websockets/iothub_client_sample_amqp_websockets.c

    <span data-ttu-id="78e58-192">**对于将 WebSocket 与 MQTT 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="78e58-192">**For WebSocket with MQTT protocol:**</span></span>

        nano azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_mqtt_websockets/iothub_client_sample_mqtt_ws.c

-   <span data-ttu-id="78e58-193">此时会启动基于控制台的文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="78e58-193">This launches a console-based text editor.</span></span> <span data-ttu-id="78e58-194">向下滚动到连接信息。</span><span class="sxs-lookup"><span data-stu-id="78e58-194">Scroll down to the connection information.</span></span>

-   <span data-ttu-id="78e58-195">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="78e58-195">Find the following place holder for IoT connection string:</span></span>

        static const char* connectionString = "[device connection string]";

-   <span data-ttu-id="78e58-196">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="78e58-196">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="78e58-197">可根据[步骤 2](#Step-2-Register) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="78e58-197">You can get this from DeviceExplorer as explained in [Step 2](#Step-2-Register), that you copied into Notepad.</span></span>

-   <span data-ttu-id="78e58-198">按 Ctrl+O 保存更改，当 nano 提示是否保存到同一文件时，按 ENTER 即可。</span><span class="sxs-lookup"><span data-stu-id="78e58-198">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

-   <span data-ttu-id="78e58-199">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="78e58-199">Press Ctrl+X to exit nano.</span></span>

-   <span data-ttu-id="78e58-200">使用以下命令生成 SDK。</span><span class="sxs-lookup"><span data-stu-id="78e58-200">Build the SDK using following command.</span></span> <span data-ttu-id="78e58-201">如果在生成期间遇到任何问题，请遵循故障排除[步骤 5](#Step-5-Troubleshooting)。</span><span class="sxs-lookup"><span data-stu-id="78e58-201">If you are facing any issues during build, follow troubleshooting [Step 5](#Step-5-Troubleshooting).</span></span>

        sudo ./azure-iot-sdk-c/build_all/linux/build.sh | tee LogFile.txt

    <span data-ttu-id="78e58-202">对于 WebSocket 协议，请使用以下命令生成 SDK</span><span class="sxs-lookup"><span data-stu-id="78e58-202">For WebSocket Protocols, use below command to build the SDK</span></span>
    
        sudo ./azure-iot-sdk-c/build_all/linux/build.sh --use-websockets
    
    <span data-ttu-id="78e58-203">***注意：****应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*</span><span class="sxs-lookup"><span data-stu-id="78e58-203">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>
    
    <span data-ttu-id="78e58-204">*build.sh 在“~/azure-iot-sdk-c/”下创建名为“cmake”的文件夹。“cmake”中保存了整个软件的所有编译结果。*</span><span class="sxs-lookup"><span data-stu-id="78e58-204">*build.sh creates a folder called "cmake" under "~/azure-iot-sdk-c/". Inside "cmake" are all the results of the compilation of the complete software.*</span></span>


<a name="Step-3-3-Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="78e58-205">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="78e58-205">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="78e58-206">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="78e58-206">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="78e58-207">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="78e58-207">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="78e58-208">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="78e58-208">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="78e58-209">**注意：**请为本部分中执行的所有操作创建屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="78e58-209">**Note:** Take screenshots of all the operations you will perform in this section.</span></span> <span data-ttu-id="78e58-210">[步骤 4](#Step-4-2-Share) 中需要用到这些屏幕截图</span><span class="sxs-lookup"><span data-stu-id="78e58-210">These will be needed in [Step 4](#Step-4-2-Share)</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="78e58-211">3.3.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="78e58-211">3.3.1 Send Device Events to IOT Hub:</span></span>

1.  <span data-ttu-id="78e58-212">如[步骤 2](#Step-2-Register) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="78e58-212">Launch the DeviceExplorer as explained in [Step 2](#Step-2-Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_Monitor](images/3_3_1_01.png)

2.  <span data-ttu-id="78e58-214">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="78e58-214">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="78e58-215">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="78e58-215">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="78e58-216">**如果使用 AMQP 协议：**运行示例 *iothub\_client\_sample\_amqp*</span><span class="sxs-lookup"><span data-stu-id="78e58-216">**If using AMQP protocol:** Run sample *iothub\_client\_sample\_amqp*</span></span>

        ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp


    <span data-ttu-id="78e58-217">**如果使用 HTTP 协议：**运行示例 *iothub\_client\_sample\_http*</span><span class="sxs-lookup"><span data-stu-id="78e58-217">**If using HTTP protocol:** Run sample *iothub\_client\_sample\_http*</span></span>

        ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http


    <span data-ttu-id="78e58-218">**如果使用 MQTT 协议：**运行示例 *iothub\_client\_sample\_mqtt*</span><span class="sxs-lookup"><span data-stu-id="78e58-218">**If using MQTT protocol:** Run sample *iothub\_client\_sample\_mqtt*</span></span>

        ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_mqtt/iothub_client_sample_mqtt
    
    <span data-ttu-id="78e58-219">**如果将 WebSocket 与 AMQP 协议配合使用：**运行示例 *iothub\_client\_sample\_amqp_websocket*</span><span class="sxs-lookup"><span data-stu-id="78e58-219">**If using WebSocket with AMQP protocol:** Run sample *iothub\_client\_sample\_amqp_websocket*</span></span>

                ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_amqp_websockets/iothub_client_sample_amqp_websockets

    <span data-ttu-id="78e58-220">**如果将 WebSocket 与 MQTT 协议配合使用：**运行示例 *iothub\_client\_sample\_amqp_websocket*</span><span class="sxs-lookup"><span data-stu-id="78e58-220">**If using WebSocket with MQTT protocol:** Run sample *iothub\_client\_sample\_mqtt_websocket*</span></span>

        ~/azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_mqtt_websockets/iothub_client_sample_mqtt_websockets

4.  <span data-ttu-id="78e58-221">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="78e58-221">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="78e58-222">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="78e58-222">If not, then you may have incorrectly copied the device hub connection information.</span></span>

    <span data-ttu-id="78e58-223">**如果使用 AMQP 协议：**
    ![SampleAMQP\_result\_terminal](images/3_3_1_02.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-223">**If using AMQP protocol:**
![SampleAMQP\_result\_terminal](images/3_3_1_02.png)</span></span>

    <span data-ttu-id="78e58-224">**如果使用 HTTP 协议：**
    ![SampleHTTP\_result\_terminal](images/3_3_1_03.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-224">**If using HTTP protocol:**
![SampleHTTP\_result\_terminal](images/3_3_1_03.png)</span></span>

    <span data-ttu-id="78e58-225">**如果使用 MQTT 协议：**
    ![SampleMQTT\_result\_terminal](images/3_3_1_09.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-225">**If using MQTT protocol:**
![SampleMQTT\_result\_terminal](images/3_3_1_09.png)</span></span>

    <span data-ttu-id="78e58-226">**如果将 WebSocket 与 AMQP 协议配合使用：**
    ![SampleAMQPWS\_result\_terminal](images/terminal_amqps_ws_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-226">**If using WebSocket with AMQP protocol:**
![SampleAMQPWS\_result\_terminal](images/terminal_amqps_ws_send_event.png)</span></span>
    
    <span data-ttu-id="78e58-227">**如果将 WebSocket 与 MQTT 协议配合使用：**
    ![SampleMQTTWS\_result\_terminal](images/terminal_mqtt_ws_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-227">**If using WebSocket with MQTT protocol:**
![SampleMQTTWS\_result\_terminal](images/terminal_mqtt_ws_send_event.png)</span></span>

5.  <span data-ttu-id="78e58-228">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="78e58-228">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="78e58-229">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="78e58-229">**If using AMQP protocol:**</span></span>
    
    ![SampleAMQP\_result\_DeviceExplorer](images/3_3_1_04.png)

    <span data-ttu-id="78e58-231">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="78e58-231">**If using HTTP protocol:**</span></span>
    
    ![SampleHTTP\_result\_DeviceExplorer](images/3_3_1_05.png)

    <span data-ttu-id="78e58-233">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="78e58-233">**If using MQTT protocol:**</span></span>
    
    ![SampleMQTT\_result\_DeviceExplorer](images/3_3_1_10.png)

    <span data-ttu-id="78e58-235">**如果将 WebSocket 与 AMQP 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="78e58-235">**If using WebSocket with AMQP protocol:**</span></span>

    ![SampleAMQPWS\_result\_DeviceExplorer](images/device_explorer_amqp_ws_message_received.png)
    
    <span data-ttu-id="78e58-237">**如果将 WebSocket 与 MQTT 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="78e58-237">**If using WebSocket with MQTT protocol:**</span></span>

    ![SampleMQTTWS\_result\_DeviceExplorer](images/device_explorer_mqtt_ws_message_received.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="78e58-239">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="78e58-239">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="78e58-240">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="78e58-240">To verify that you can send messages from the IoT Hub to your device, go to the **Message To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="78e58-241">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="78e58-241">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="78e58-242">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="78e58-242">Add some text to the Message field, then click Send.</span></span>

    ![MessageSend\_DeviceExplorer](images/3_3_1_06.png)

4.  <span data-ttu-id="78e58-244">应会在客户端示例的控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="78e58-244">You should be able to see the command received in the console window for the client sample.</span></span>

    <span data-ttu-id="78e58-245">**如果使用 AMQP 协议：**
    ![MessageSend\_terminal](images/3_3_1_07.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-245">**If using AMQP protocol:**
![MessageSend\_terminal](images/3_3_1_07.png)</span></span>

    <span data-ttu-id="78e58-246">**如果使用 HTTP 协议：**
    ![MessageSend\_terminal](images/3_3_1_08.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-246">**If using HTTP protocol:**
![MessageSend\_terminal](images/3_3_1_08.png)</span></span>

    <span data-ttu-id="78e58-247">**如果使用 MQTT 协议：**
    ![MessageSend\_terminal](images/3_3_1_11.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-247">**If using MQTT protocol:**
![MessageSend\_terminal](images/3_3_1_11.png)</span></span>

    <span data-ttu-id="78e58-248">**如果将 WebSocket 与 AMQP 协议配合使用：**
    ![MessageSend\_terminal](images/terminal_amqp_ws_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-248">**If using WebSocket with AMQP protocol:**
![MessageSend\_terminal](images/terminal_amqp_ws_message_received.png)</span></span>
    
    <span data-ttu-id="78e58-249">**如果将 WebSocket 与 MQTT 协议配合使用：**
    ![MessageSend\_terminal](images/terminal_mqtt_ws_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="78e58-249">**If using WebSocket with MQTT protocol:**
![MessageSend\_terminal](images/terminal_mqtt_ws_message_received.png)</span></span>

<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="78e58-250">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="78e58-250">Step 4: Package and Share</span></span>

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="78e58-251">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="78e58-251">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="78e58-252">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="78e58-252">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="78e58-253">在生成运行过程中记录到日志文件中的生成日志。</span><span class="sxs-lookup"><span data-stu-id="78e58-253">Build logs that were logged in the log files during build run.</span></span>

2.  <span data-ttu-id="78e58-254">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="78e58-254">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="78e58-255">前面“**从 IoT 中心接收消息**”部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="78e58-255">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="78e58-256">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="78e58-256">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="78e58-257">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="78e58-257">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="78e58-258">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="78e58-258">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a><span data-ttu-id="78e58-259">4.2 与 Microsoft Azure IoT 团队共享包</span><span class="sxs-lookup"><span data-stu-id="78e58-259">4.2 Share package with Microsoft Azure IoT team</span></span>

1.  <span data-ttu-id="78e58-260">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="78e58-260">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="78e58-261">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="78e58-261">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="78e58-263">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="78e58-263">This will open an upload dialog.</span></span> <span data-ttu-id="78e58-264">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="78e58-264">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="78e58-266">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="78e58-266">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="78e58-267">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="78e58-267">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="78e58-268">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="78e58-268">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="78e58-269">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="78e58-269">4.3 Next steps</span></span>

<span data-ttu-id="78e58-270">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="78e58-270">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="78e58-271">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="78e58-271">Step 5: Troubleshooting</span></span>

<span data-ttu-id="78e58-272">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="78e58-272">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
