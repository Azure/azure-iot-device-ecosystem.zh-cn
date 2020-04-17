<a name="how-to-certify-arm-32-iot-devices-running-net-core-within-a-linux-docker-container-linux-is-also-the-host-os"></a><span data-ttu-id="c7774-101">如何认证在 Linux Docker 容器中运行 .NET Core 的 ARM 32 IoT 设备（Linux 也是主机 OS）。</span><span class="sxs-lookup"><span data-stu-id="c7774-101">How to certify ARM 32 IoT devices running .NET Core within a Linux Docker container (Linux is also the host OS).</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="c7774-102">目录</span><span class="sxs-lookup"><span data-stu-id="c7774-102">Table of Contents</span></span>

-   [<span data-ttu-id="c7774-103">简介</span><span class="sxs-lookup"><span data-stu-id="c7774-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="c7774-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c7774-104">Step 1: Configure Azure IoT Hub</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="c7774-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="c7774-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="c7774-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="c7774-106">Step 3: Build and Validate the sample using C client libraries</span></span>](#Step-3-Build)
    -   [<span data-ttu-id="c7774-107">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="c7774-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Step-3-1-Load)
    -   [<span data-ttu-id="c7774-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="c7774-108">3.2 Build the samples</span></span>](#Step-3-2-Build)
    -   [<span data-ttu-id="c7774-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="c7774-109">3.3 Run and Validate the Samples</span></span>](#Step-3-3-Run)
-   [<span data-ttu-id="c7774-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="c7774-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="c7774-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="c7774-111">4.1 Package build logs and sample test results</span></span>](#Step-4-1-Package)
    -   [<span data-ttu-id="c7774-112">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="c7774-112">4.2 Share package with Engineering Support</span></span>](#Step-4-2-Share)
    -   [<span data-ttu-id="c7774-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="c7774-113">4.3 Next steps</span></span>](#Step-4-3-Next)
-   [<span data-ttu-id="c7774-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="c7774-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="c7774-115">简介</span><span class="sxs-lookup"><span data-stu-id="c7774-115">Introduction</span></span>

<span data-ttu-id="c7774-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="c7774-116">**About this document**</span></span>

<span data-ttu-id="c7774-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="c7774-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="c7774-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="c7774-118">This multi-step process includes:</span></span>

-   <span data-ttu-id="c7774-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c7774-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="c7774-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="c7774-120">Registering your IoT device</span></span>
-   <span data-ttu-id="c7774-121">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="c7774-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="c7774-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="c7774-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="c7774-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="c7774-123">**Prepare**</span></span>

<span data-ttu-id="c7774-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="c7774-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="c7774-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="c7774-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="c7774-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="c7774-126">Computer with GitHub installed and access to the [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) GitHub public repository.</span></span>
-   <span data-ttu-id="c7774-127">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="c7774-127">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="c7774-128">可以安装任何版本的 Visual Studio，包括免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="c7774-128">You can install any edition of Visual Studio, including the free Community edition.</span></span>
-   <span data-ttu-id="c7774-129">用于访问设备命令行的 SSH 客户端，例如 PuTTY。</span><span class="sxs-lookup"><span data-stu-id="c7774-129">SSH client, such as PuTTY, so you can access the command line of your device.</span></span>
-   <span data-ttu-id="c7774-130">在开发计算机和设备上安装 Docker： https://www.docker.com/get-started</span><span class="sxs-lookup"><span data-stu-id="c7774-130">Install Docker on both your development machine and your device: https://www.docker.com/get-started</span></span>

<span data-ttu-id="c7774-131">\*\**注意：\*\*\*\*如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://catalog.azureiotsuite.com/>)请求此身份，然后遵照本文中的说明操作。*</span><span class="sxs-lookup"><span data-stu-id="c7774-131">***Note:*** *If you haven't contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://catalog.azureiotsuite.com/>) first to request it and then follow these instructions.*</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="c7774-132">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c7774-132">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="c7774-133">遵照[此处](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub)所述的说明[注册](https://account.windowsazure.com/signup?offer=ms-azr-0044p) Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="c7774-133">[Sign up](https://account.windowsazure.com/signup?offer=ms-azr-0044p) to the Azure IoT Hub service and follow the instructions mentioned [here](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub).</span></span> <span data-ttu-id="c7774-134">若要了解如何查找 IoT 中心的连接字符串，请参阅[此文档](https://devblogs.microsoft.com/iotdev/understand-different-connection-strings-in-azure-iot-hub/)。</span><span class="sxs-lookup"><span data-stu-id="c7774-134">Refer to [this documentation](https://devblogs.microsoft.com/iotdev/understand-different-connection-strings-in-azure-iot-hub/) on how to find the connection string for your IoT Hub.</span></span>

-   <span data-ttu-id="c7774-135">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="c7774-135">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="c7774-136">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="c7774-136">Step 2: Register Device</span></span>

<span data-ttu-id="c7774-137">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="c7774-137">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="c7774-138">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c7774-138">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="c7774-139">设备管理</span><span class="sxs-lookup"><span data-stu-id="c7774-139">Device management</span></span>
    -   <span data-ttu-id="c7774-140">创建新设备</span><span class="sxs-lookup"><span data-stu-id="c7774-140">Create new devices</span></span>
    -   <span data-ttu-id="c7774-141">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="c7774-141">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="c7774-142">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="c7774-142">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="c7774-143">可删除设备</span><span class="sxs-lookup"><span data-stu-id="c7774-143">Provides ability to delete a device</span></span>
-   <span data-ttu-id="c7774-144">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="c7774-144">Monitoring events from your device</span></span>
-   <span data-ttu-id="c7774-145">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="c7774-145">Sending messages to your device</span></span>

<span data-ttu-id="c7774-146">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step-1-Configure) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="c7774-146">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step-1-Configure):</span></span>

-   <span data-ttu-id="c7774-147">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="c7774-147">IoT Hub Connection String</span></span>

<span data-ttu-id="c7774-148">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="c7774-148">**Steps:**</span></span>
1.  <span data-ttu-id="c7774-149">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="c7774-149">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="c7774-150">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。 </span><span class="sxs-lookup"><span data-stu-id="c7774-150">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="c7774-151">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="c7774-151">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="c7774-152">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="c7774-152">a.</span></span> <span data-ttu-id="c7774-153">单击“管理”选项卡。 </span><span class="sxs-lookup"><span data-stu-id="c7774-153">Click the **Management** tab.</span></span>

    <span data-ttu-id="c7774-154">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="c7774-154">b.</span></span> <span data-ttu-id="c7774-155">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="c7774-155">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="c7774-156">如果你的设备未显示在列表中，请单击“刷新”按钮。 </span><span class="sxs-lookup"><span data-stu-id="c7774-156">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="c7774-157">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="c7774-157">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="c7774-158">c.</span><span class="sxs-lookup"><span data-stu-id="c7774-158">c.</span></span> <span data-ttu-id="c7774-159">单击“创建”按钮创建设备 ID 和密钥。 </span><span class="sxs-lookup"><span data-stu-id="c7774-159">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="c7774-160">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="c7774-160">d.</span></span> <span data-ttu-id="c7774-161">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="c7774-161">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="c7774-162">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="c7774-162">e.</span></span> <span data-ttu-id="c7774-163">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。 </span><span class="sxs-lookup"><span data-stu-id="c7774-163">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="c7774-164">f.</span><span class="sxs-lookup"><span data-stu-id="c7774-164">f.</span></span> <span data-ttu-id="c7774-165">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="c7774-165">Save this information in Notepad.</span></span> <span data-ttu-id="c7774-166">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="c7774-166">You will need this information in later steps.</span></span>

<span data-ttu-id="c7774-167">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="c7774-167">***Not running Windows on your PC?***</span></span> <span data-ttu-id="c7774-168">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="c7774-168">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step-3-Build"></a>
# <a name="step-3-build-a-linux-docker-image-that-includes-the-net-core-runtime-and-the-sample-used-for-validating-your-device"></a><span data-ttu-id="c7774-169">步骤 3：生成一个 Linux Docker 映像，其中包含 .NET Core 运行时和示例，用于验证设备。</span><span class="sxs-lookup"><span data-stu-id="c7774-169">Step 3: Build a Linux Docker image that includes the .NET Core runtime and the sample used for validating your device.</span></span>

<span data-ttu-id="c7774-170">本部分逐步讲解如何生成并运行 Linux Docker 映像，以便在 ARM 32 设备上验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="c7774-170">This sections walks you through building a Linux Docker image and running the image to validate the IoT Client SDK on your ARM 32 device.</span></span>  <span data-ttu-id="c7774-171">除非另有说明，否则 Docker 映像会包含运行示例测试所需的所有必备组件。这些测试是在设备上进行 IoT 认证所需的。</span><span class="sxs-lookup"><span data-stu-id="c7774-171">Unless specified otherwise, the Docker image will contain all necessary prerequisites for running the sample tests required for IoT certification on your device.</span></span>

<a name="Step_3_1:_Development"></a>
## <a name="31-prepare-your-development-environment"></a><span data-ttu-id="c7774-172">3.1：准备开发环境</span><span class="sxs-lookup"><span data-stu-id="c7774-172">3.1 Prepare your development environment</span></span>

- <span data-ttu-id="c7774-173">从 https://dot.net 安装最新的 .NET Core</span><span class="sxs-lookup"><span data-stu-id="c7774-173">Install the latest .NET Core from https://dot.net</span></span>
- <span data-ttu-id="c7774-174">安装 .NET Framework 4.7 开发人员包： https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs</span><span class="sxs-lookup"><span data-stu-id="c7774-174">Install .NET Framework 4.7 Developer Pack: https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs</span></span>
- <span data-ttu-id="c7774-175">安装 .NET Framework 4.5.1 开发人员包： https://www.microsoft.com/en-us/download/details.aspx?id=40772</span><span class="sxs-lookup"><span data-stu-id="c7774-175">Install .NET Framework 4.5.1 Developer Pack: https://www.microsoft.com/en-us/download/details.aspx?id=40772</span></span>

<a name="Step_3_2:_Build"></a>
## <a name="32-build-and-push-the-docker-image-to-your-registry"></a><span data-ttu-id="c7774-176">3.2：生成 Docker 映像并将其推送到注册表</span><span class="sxs-lookup"><span data-stu-id="c7774-176">3.2 Build and push the Docker image to your registry</span></span>

<span data-ttu-id="c7774-177">使用[此 Dockerfile](./Dockerfile) 生成一个基于 [.NET Core Arm32 Linux 映像](https://hub.docker.com/_/microsoft-dotnet-core-samples/)的 Docker 映像：</span><span class="sxs-lookup"><span data-stu-id="c7774-177">Using [this Dockerfile](./Dockerfile), build a Docker image that is based on the [.NET Core Arm32 Linux image](https://hub.docker.com/_/microsoft-dotnet-core-samples/):</span></span>

-   <span data-ttu-id="c7774-178">在开发环境中打开包含 [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) 的目录，具体说来就是打开以下目录：</span><span class="sxs-lookup"><span data-stu-id="c7774-178">In your development environment, open the directory containing [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp); specifically, open the following directory:</span></span>

        iot-hub\Samples\device\MessageSample

-   <span data-ttu-id="c7774-179">复制[此 Dockerfile](./Dockerfile) 并将其粘贴到如上所示的 MessageSample 目录。</span><span class="sxs-lookup"><span data-stu-id="c7774-179">Copy and paste [this Dockerfile](./Dockerfile) to the MessageSample directory shown above.</span></span>
-   <span data-ttu-id="c7774-180">在 Dockerfile 中以环境变量的形式添加 IoT 中心设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c7774-180">Add the IoT Hub device connection string as an environment variable within the Dockerfile.</span></span>  <span data-ttu-id="c7774-181">具体说来，请打开 Dockerfile 并将“<your_device_connection_string>”替换为你的设备连接字符串，然后保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="c7774-181">Specifically, open the Dockerfile and replace '<your_device_connection_string>' with your device connection string and save your changes.</span></span>
-   <span data-ttu-id="c7774-182">使用 Docker 和 Dockerfile，生成一个将 .NET Core 消息示例应用容器化的 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="c7774-182">Using Docker and the Dockerfile, build a Docker image that containerizes the .NET Core Message Sample app.</span></span>  <span data-ttu-id="c7774-183">接下来，将此映像推送到 Docker 注册表。</span><span class="sxs-lookup"><span data-stu-id="c7774-183">Next, push this image to your Docker registry.</span></span>  <span data-ttu-id="c7774-184">例如：</span><span class="sxs-lookup"><span data-stu-id="c7774-184">For example:</span></span>

        cd iot-hub\Samples\device\MessageSample
        docker build -t <your_docker_account>/<your_docker_repo>:<your_img_tag> .
        docker push <your_docker_account>/<your_docker_repo>:<your_img_tag>

<span data-ttu-id="c7774-185">此示例包含两类测试 - 一类用于向 IoT 中心发送消息，另一类用于从 IoT 中心接收消息。</span><span class="sxs-lookup"><span data-stu-id="c7774-185">The sample contains two types of tests - one for sending messages to IoT Hub and another for receiving messages from IoT Hub.</span></span> <span data-ttu-id="c7774-186">两类测试都支持不同的协议。</span><span class="sxs-lookup"><span data-stu-id="c7774-186">Both tests support different protocols.</span></span> <span data-ttu-id="c7774-187">在生成 Docker 映像之前，可以修改测试，以便使用所选协议。</span><span class="sxs-lookup"><span data-stu-id="c7774-187">You can modify the tests to use your choice of protocol before building the Docker image.</span></span> <span data-ttu-id="c7774-188">默认情况下，将会使用 AMQP 协议生成测试。</span><span class="sxs-lookup"><span data-stu-id="c7774-188">By default the tests will build using the AMQP protocol.</span></span>

<span data-ttu-id="c7774-189">若要运行不同的协议，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c7774-189">To run different protocols:</span></span>

-   <span data-ttu-id="c7774-190">在开发环境中，使用记事本打开以下文件：</span><span class="sxs-lookup"><span data-stu-id="c7774-190">In your development environment, open the following file in notepad:</span></span>

        iot-hub\Samples\device\MessageSample\Program.cs

-   <span data-ttu-id="c7774-191">向下滚动到包含协议信息的代码节。</span><span class="sxs-lookup"><span data-stu-id="c7774-191">Scroll down to the section of code containing the protocol information.</span></span>

-   <span data-ttu-id="c7774-192">找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="c7774-192">Find the below code:</span></span>

        private static TransportType s_transportType = TransportType.Amqp;

    <span data-ttu-id="c7774-193">使用的默认协议为 AMQP。</span><span class="sxs-lookup"><span data-stu-id="c7774-193">The default protocol used is AMQP.</span></span> <span data-ttu-id="c7774-194">脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。</span><span class="sxs-lookup"><span data-stu-id="c7774-194">Code for other protocols(HTTP/MQTT) are mentioned just below the above line in the script.</span></span> <span data-ttu-id="c7774-195">根据要使用的协议对该行进行注释/取消注释操作，然后保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="c7774-195">Comment/Uncomment the line as per the protocol you want to use and save your changes.</span></span>

-   <span data-ttu-id="c7774-196">使用在步骤 3.2 开头介绍的步骤重新生成 Docker 映像。</span><span class="sxs-lookup"><span data-stu-id="c7774-196">Rebuild the Docker image using the steps described at the beginning of Step 3.2.</span></span>

<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-sample"></a><span data-ttu-id="c7774-197">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="c7774-197">3.3 Run and validate the sample</span></span>

<span data-ttu-id="c7774-198">在本部分，我们将运行此示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="c7774-198">In this section you will run the sample to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="c7774-199">我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="c7774-199">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="c7774-200">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="c7774-200">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="c7774-201">\*\**注意：\*\*\*\*请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2:_Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c7774-201">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2:_Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="c7774-202">3.3.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="c7774-202">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="c7774-203">如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。  从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。 </span><span class="sxs-lookup"><span data-stu-id="c7774-203">Launch the DeviceExplorer as explained in [Step 2](#Step_2:_Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="c7774-205">DeviceExplorer 现在正在监视从所选设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="c7774-205">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="c7774-206">打开 PuTTY 会话并连接到设备，然后通过拉取并运行 Docker 映像来运行示例。</span><span class="sxs-lookup"><span data-stu-id="c7774-206">Open a PuTTY session and connect to the device, run the sample by pulling and running the Docker image.</span></span>  <span data-ttu-id="c7774-207">例如：</span><span class="sxs-lookup"><span data-stu-id="c7774-207">For example:</span></span>
        
        docker run --rm <your_docker_account>/<your_docker_repo>:<your_img_tag>
    
4. <span data-ttu-id="c7774-208">成功执行后，应会看到设备控制台中收到的事件。</span><span class="sxs-lookup"><span data-stu-id="c7774-208">You should be able to see the events received in device console on successful execution.</span></span>

    <span data-ttu-id="c7774-209">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-209">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_http.png)

    <span data-ttu-id="c7774-211">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-211">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_mqtt.png)

    <span data-ttu-id="c7774-213">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-213">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_amqp.png)

5. <span data-ttu-id="c7774-215">DeviceExplorer 的数据选项卡中应会显示收到的事件。</span><span class="sxs-lookup"><span data-stu-id="c7774-215">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

    <span data-ttu-id="c7774-216">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-216">**If HTTP protocol:**</span></span>   

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_http.png)

    <span data-ttu-id="c7774-218">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-218">**If MQTT protocol:**</span></span>

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_mqtt.png)

    <span data-ttu-id="c7774-220">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-220">**If AMQP protocol:**</span></span>
    
     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_amqp.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="c7774-222">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="c7774-222">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="c7774-223">若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。 </span><span class="sxs-lookup"><span data-stu-id="c7774-223">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>  <span data-ttu-id="c7774-224">注意，需在设备上再次运行此示例应用，所使用的命令与上一步的相同，例如：docker run --rm <your_docker_account>/<your_docker_repo>:<your_img_tag></span><span class="sxs-lookup"><span data-stu-id="c7774-224">Note that you will need to run the sample ap again on your device using the same command as in the previous step, such as: docker run --rm <your_docker_account>/<your_docker_repo>:<your_img_tag></span></span>

2.  <span data-ttu-id="c7774-225">使用“设备 ID”下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="c7774-225">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="c7774-226">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="c7774-226">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

4. <span data-ttu-id="c7774-228">设备控制台窗口中应会显示收到的消息。</span><span class="sxs-lookup"><span data-stu-id="c7774-228">You should be able to see the message received in the device console window.</span></span>
    
    <span data-ttu-id="c7774-229">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-229">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

    <span data-ttu-id="c7774-231">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-231">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_mqtt.png)

    <span data-ttu-id="c7774-233">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c7774-233">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_amqp.png)
    
### <a name="333-verify-device-configuration"></a><span data-ttu-id="c7774-235">3.3.3 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="c7774-235">3.3.3 Verify Device configuration</span></span>

-   <span data-ttu-id="c7774-236">请通过执行以下命令安装 python。</span><span class="sxs-lookup"><span data-stu-id="c7774-236">Please install python by following below command.</span></span>

    <span data-ttu-id="c7774-237">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="c7774-237">**Debian or Ubuntu**</span></span>

        sudo apt-get install python

    <span data-ttu-id="c7774-238">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="c7774-238">**Fedora**</span></span>

        sudo dnf install python

-    <span data-ttu-id="c7774-239">*此库还需要 Python 版本 2.7.x。* 可使用以下命令来验证环境中当前安装的版本：</span><span class="sxs-lookup"><span data-stu-id="c7774-239">*This library also requires Python version 2.7.x. You can verify the current version installed in your environment using the following command:*</span></span>
    
          python --version

-   <span data-ttu-id="c7774-240">在运行 `platform_data.py` 之前，请安装以下模块</span><span class="sxs-lookup"><span data-stu-id="c7774-240">Please install the below modules before you run the `platform_data.py`</span></span>

    <span data-ttu-id="c7774-241">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="c7774-241">**Debian or Ubuntu**</span></span> 

        sudo apt-get install python-requests
        sudo apt-get install python-netifaces

    <span data-ttu-id="c7774-242">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="c7774-242">**Fedora**</span></span>

        sudo dnf install python-requests
        sudo dnf install python-netifaces

-   <span data-ttu-id="c7774-243">发出以下命令下载 SDK：</span><span class="sxs-lookup"><span data-stu-id="c7774-243">Download the SDK by issuing following command:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-python.git

-   <span data-ttu-id="c7774-244">通过执行以下命令导航到 tools 文件夹：</span><span class="sxs-lookup"><span data-stu-id="c7774-244">Navigate to tools folder by executing following command:</span></span>

        cd azure-iot-sdk-python/Tools

-   <span data-ttu-id="c7774-245">在设备上运行以下命令</span><span class="sxs-lookup"><span data-stu-id="c7774-245">Run the following command on the device</span></span>
        
        python platform_data.py

    ![deviceinfo\_screenshot](images/python_modified_output.PNG)

-   <span data-ttu-id="c7774-247">请保存设备配置屏幕截图，然后按[步骤 4](#Step-4-1-Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c7774-247">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Step-4-1-Package).</span></span>

<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="c7774-248">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="c7774-248">Step 4: Package and Share</span></span>

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="c7774-249">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="c7774-249">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="c7774-250">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="c7774-250">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="c7774-251">在生成运行期间记录在日志文件中的生成日志。</span><span class="sxs-lookup"><span data-stu-id="c7774-251">Build logs that were logged in the log files during build run.</span></span>

2.  <span data-ttu-id="c7774-252">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。 </span><span class="sxs-lookup"><span data-stu-id="c7774-252">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="c7774-253">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。 </span><span class="sxs-lookup"><span data-stu-id="c7774-253">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="c7774-254">前面“设备配置”  部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c7774-254">All the screenshots that are above in "**Device Configuration**" section.</span></span>

5.  <span data-ttu-id="c7774-255">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="c7774-255">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="c7774-256">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="c7774-256">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-c.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="c7774-257">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="c7774-257">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a><span data-ttu-id="c7774-258">4.2 与 Microsoft Azure IoT 团队共享包</span><span class="sxs-lookup"><span data-stu-id="c7774-258">4.2 Share package with Microsoft Azure IoT team</span></span>

1.  <span data-ttu-id="c7774-259">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="c7774-259">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="c7774-260">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="c7774-260">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="c7774-262">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="c7774-262">This will open an upload dialog.</span></span> <span data-ttu-id="c7774-263">单击“上载”按钮浏览文件。 </span><span class="sxs-lookup"><span data-stu-id="c7774-263">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="c7774-265">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="c7774-265">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="c7774-266">上传所有文件后，单击“提交审查”按钮。 </span><span class="sxs-lookup"><span data-stu-id="c7774-266">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="c7774-267">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="c7774-267">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="c7774-268">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="c7774-268">4.3 Next steps</span></span>

<span data-ttu-id="c7774-269">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="c7774-269">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="c7774-270">步骤 5：疑难解答</span><span class="sxs-lookup"><span data-stu-id="c7774-270">Step 5: Troubleshooting</span></span>

<span data-ttu-id="c7774-271">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="c7774-271">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
