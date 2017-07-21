<a name="how-to-certify-iot-devices-running-mbed-os-with-azure-iot-sdk"></a><span data-ttu-id="bbe6c-101">如何使用 Azure IoT SDK 认证运行 Mbed OS 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-101">How to Certify IoT devices running Mbed OS with Azure IoT SDK</span></span>
===
---


# <a name="table-of-contents"></a><span data-ttu-id="bbe6c-102">目录</span><span class="sxs-lookup"><span data-stu-id="bbe6c-102">Table of Contents</span></span>

-   [<span data-ttu-id="bbe6c-103">介绍</span><span class="sxs-lookup"><span data-stu-id="bbe6c-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="bbe6c-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bbe6c-104">Step 1: Configure Azure IoT Hub</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="bbe6c-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="bbe6c-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-106">Step 3: Build and Validate the sample using C client libraries</span></span>](#Step-3-Build)
    -   [<span data-ttu-id="bbe6c-107">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-107">3.1 Connect the Device</span></span>](#Step-3-1-Load)
    -   [<span data-ttu-id="bbe6c-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-108">3.2 Build the samples</span></span>](#Step-3-2-Build)
    -   [<span data-ttu-id="bbe6c-109">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-109">3.3 Run and Validate the Samples</span></span>](#Step-3-3-Run)
-   [<span data-ttu-id="bbe6c-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="bbe6c-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="bbe6c-111">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="bbe6c-111">4.1 Package build logs and sample test results</span></span>](#Step-4-1-Package)
    -   [<span data-ttu-id="bbe6c-112">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="bbe6c-112">4.2 Share package with Engineering Support</span></span>](#Step-4-2-Share)
    -   [<span data-ttu-id="bbe6c-113">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="bbe6c-113">4.3 Next steps</span></span>](#Step-4-3-Next)
-   [<span data-ttu-id="bbe6c-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="bbe6c-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="bbe6c-115">介绍</span><span class="sxs-lookup"><span data-stu-id="bbe6c-115">Introduction</span></span>

<span data-ttu-id="bbe6c-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="bbe6c-116">**About this document**</span></span>

<span data-ttu-id="bbe6c-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="bbe6c-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-118">This multi-step process includes:</span></span>
-   <span data-ttu-id="bbe6c-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bbe6c-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="bbe6c-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-120">Registering your IoT device</span></span>
-   <span data-ttu-id="bbe6c-121">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="bbe6c-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="bbe6c-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="bbe6c-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="bbe6c-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="bbe6c-123">**Prepare**</span></span>

<span data-ttu-id="bbe6c-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="bbe6c-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="bbe6c-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 专用存储库的计算机</span><span class="sxs-lookup"><span data-stu-id="bbe6c-126">Computer with GitHub installed and access to the [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub private repository</span></span>
-   <span data-ttu-id="bbe6c-127">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行</span><span class="sxs-lookup"><span data-stu-id="bbe6c-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line</span></span>
-   <span data-ttu-id="bbe6c-128">用于认证的所需硬件</span><span class="sxs-lookup"><span data-stu-id="bbe6c-128">Required hardware to certify</span></span>

<span data-ttu-id="bbe6c-129">***注意：****如果你尚未咨询 Microsoft 如何成为 Azure 认证的 IoT 合作伙伴，请先提交此[表单](<https://iotcert.cloudapp.net/>)来提出请求，然后遵照本文中的说明。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-129">***Note:*** *If you haven’t contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://iotcert.cloudapp.net/>) first to request it and then follow these instructions.*</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="bbe6c-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bbe6c-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="bbe6c-131">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-131">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="bbe6c-132">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-132">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];CredentialType=SharedAccessSignature;CredentialScope=[ContosoIotHub];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="bbe6c-133">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-133">Step 2: Register Device</span></span>

<span data-ttu-id="bbe6c-134">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-134">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="bbe6c-135">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-135">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="bbe6c-136">设备管理</span><span class="sxs-lookup"><span data-stu-id="bbe6c-136">Device management</span></span>
    -   <span data-ttu-id="bbe6c-137">创建新设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-137">Create new devices</span></span>
    -   <span data-ttu-id="bbe6c-138">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="bbe6c-138">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="bbe6c-139">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="bbe6c-139">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="bbe6c-140">可删除设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-140">Provides ability to delete a device</span></span>
-   <span data-ttu-id="bbe6c-141">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="bbe6c-141">Monitoring events from your device</span></span>
-   <span data-ttu-id="bbe6c-142">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="bbe6c-142">Sending messages to your device</span></span>

<span data-ttu-id="bbe6c-143">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step-1-Configure) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-143">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step-1-Configure):</span></span>

-   <span data-ttu-id="bbe6c-144">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="bbe6c-144">IoT Hub Connection String</span></span>


1.  <span data-ttu-id="bbe6c-145">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-145">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="bbe6c-146">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-146">Add connection information under the **Configuration** tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="bbe6c-147">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-147">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="bbe6c-148">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-148">a.</span></span> <span data-ttu-id="bbe6c-149">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-149">Click the **Management** tab.</span></span>

    <span data-ttu-id="bbe6c-150">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-150">b.</span></span> <span data-ttu-id="bbe6c-151">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-151">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="bbe6c-152">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-152">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="bbe6c-153">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-153">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="bbe6c-154">c.</span><span class="sxs-lookup"><span data-stu-id="bbe6c-154">c.</span></span> <span data-ttu-id="bbe6c-155">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-155">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="bbe6c-156">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-156">d.</span></span> <span data-ttu-id="bbe6c-157">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-157">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="bbe6c-158">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-158">e.</span></span> <span data-ttu-id="bbe6c-159">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-159">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="bbe6c-160">f.</span><span class="sxs-lookup"><span data-stu-id="bbe6c-160">f.</span></span> <span data-ttu-id="bbe6c-161">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-161">Save this information in Notepad.</span></span> <span data-ttu-id="bbe6c-162">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-162">You will need this information in later steps.</span></span>

<span data-ttu-id="bbe6c-163">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="bbe6c-163">***Not running Windows on your PC?***</span></span> <span data-ttu-id="bbe6c-164">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-164">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step-3-Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="bbe6c-165">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-165">Step 3: Build and Validate the sample using C client libraries</span></span>

<span data-ttu-id="bbe6c-166">本部分逐步讲解如何在运行 mbed 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-166">This section walks you through building, deploying and validating the IoT Client SDK on your device running a mbed operating system.</span></span> <span data-ttu-id="bbe6c-167">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-167">You will install necessary prerequisites on your device.</span></span>  <span data-ttu-id="bbe6c-168">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-168">Once done,  you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step-3-1-Load"></a>
## <a name="31-connect-the-device"></a><span data-ttu-id="bbe6c-169">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="bbe6c-169">3.1 Connect the Device</span></span>

1.  <span data-ttu-id="bbe6c-170">使用以太网电缆将开发板连接到网络。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-170">Connect the board to your network using an Ethernet cable.</span></span> <span data-ttu-id="bbe6c-171">由于示例依赖于 Internet 访问，因此必须执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-171">This step is required, as the sample depends on internet access.</span></span>

2.  <span data-ttu-id="bbe6c-172">使用 micro-USB 电缆将设备插入计算机。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-172">Plug the device into your computer using a micro-USB cable.</span></span>

3.  <span data-ttu-id="bbe6c-173">安装[此处](http://developer.mbed.org/handbook/Windows-serial-configuration#1-download-the-mbed-windows-serial-port)提供的 Windows 串行端口驱动程序。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-173">Install the Windows serial port drivers located [here](http://developer.mbed.org/handbook/Windows-serial-configuration#1-download-the-mbed-windows-serial-port).</span></span>

4.  <span data-ttu-id="bbe6c-174">安装[此处](http://www.7-zip.org)提供的 7-Zip 软件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-174">Install the 7-Zip software from [here](http://www.7-zip.org).</span></span>

<a name="Step-3-2-Build"></a>
## <a name="32--build-the-samples"></a><span data-ttu-id="bbe6c-175">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-175">3.2  Build the samples</span></span>

1. <span data-ttu-id="bbe6c-176">将 [GitHub  SDK](https://github.com/Azure/azure-iot-sdk-c.git) 存储库克隆到计算机。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-176">Clone [GitHub  SDK](https://github.com/Azure/azure-iot-sdk-c.git) repository  to your machine.</span></span>

2.  <span data-ttu-id="bbe6c-177">浏览到文件夹</span><span class="sxs-lookup"><span data-stu-id="bbe6c-177">Browse to the folder</span></span>

        /azure-iot-sdk-c/iothub_client/samples/iothub_client_sample_amqp/mbed

3.  <span data-ttu-id="bbe6c-178">运行 **mkmbedzip.bat** 文件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-178">Run the **mkmbedzip.bat** file.</span></span> <span data-ttu-id="bbe6c-179">这会在同一文件夹中生成 **iothub\_client\_sample\_amqp.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-179">This will generate **iothub\_client\_sample\_amqp.zip** file in the same folder.</span></span>

      <span data-ttu-id="bbe6c-180">***注意：****将 zip 文件上载到编译器网页后，浏览器会保持打开该 zip 文件。在浏览器打开的情况下尝试创建另一个 zip 文件将会失败。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-180">***NOTE:*** *When the zip file is uploaded to the compiler web page, the browser will keep the zip file open. Attempting to create another zip while your browsers are open will fail.*</span></span>

4.  <span data-ttu-id="bbe6c-181">在 Web 浏览器中，转到 [mbed 开发人员站点](https://developer.mbed.org/)。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-181">In your web browser, go to the [mbed developer's site](https://developer.mbed.org/).</span></span> <span data-ttu-id="bbe6c-182">如果你尚未注册，则会看到一个用于创建新帐户（它是免费的）的选项。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-182">If you haven't signed up, you will see an option to create a new account (it's free).</span></span> <span data-ttu-id="bbe6c-183">否则，使用你的帐户凭据登录。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-183">Otherwise, log in with your account credentials.</span></span>

5.  <span data-ttu-id="bbe6c-184">单击页面右上角的“编译器”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-184">Click on **Compiler** in the upper right-hand corner of the page.</span></span>
    <span data-ttu-id="bbe6c-185">随后将会转到“工作区管理”界面。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-185">This should bring you to the **Workspace Management** interface.</span></span>

6.  <span data-ttu-id="bbe6c-186">确保所用的硬件平台显示在窗口右上角。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-186">Make sure the hardware platform you're using appears in the upper right-hand corner of the window.</span></span> <span data-ttu-id="bbe6c-187">如果没有，请单击右上角的“未选择设备”按钮选择硬件平台。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-187">If not, click the **No device selected** button in the right-hand corner to select your hardware platform.</span></span>

7.  <span data-ttu-id="bbe6c-188">在“工作区管理”菜单中，选择“新建”&minus;&gt;“新建程序”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-188">From Workspace Management menu, select **New &minus;&gt; New Program**.</span></span>

    ![Import\_Library](images/3_2_01_a.png)

8.  <span data-ttu-id="bbe6c-190">此时将显示“创建新程序”对话框。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-190">The **Create new program** dialog is displayed.</span></span> <span data-ttu-id="bbe6c-191">平台字段中应已预先填充所选的硬件平台。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-191">The platform field should be pre-populated with the hardware platform you selected.</span></span>

9.  <span data-ttu-id="bbe6c-192">将“模板”字段设置为“空程序”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-192">Set the **Template** field to **Empty Program**.</span></span> <span data-ttu-id="bbe6c-193">在“程序名称”字段中使用所需的任何程序名称，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-193">Use any program name you want in the **Program Name** field, then click OK.</span></span>

       ![](images/3_2_02.png)

10.  <span data-ttu-id="bbe6c-194">在主菜单上单击“**导入**”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-194">Click **Import** on the main menu.</span></span> <span data-ttu-id="bbe6c-195">随后将会打开“导入向导”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-195">This will bring up **Import Wizard**.</span></span>

       ![](images/3_2_03.png)

11.  <span data-ttu-id="bbe6c-196">在导入向导中转到“上载”选项卡，然后单击页面底部的“浏览...”按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-196">Go to the **Upload** tab on Import Wizard and click the **Browse...** button at the bottom of the page.</span></span>

12.  <span data-ttu-id="bbe6c-197">浏览到（使用 mkmbedzip.bat）创建 zip 文件的目录并双击它。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-197">Browse to the directory in which you created your zip file (using mkmbedzip.bat) and double-click it.</span></span> <span data-ttu-id="bbe6c-198">随后将返回到“导入向导”页，zip 文件名已显示在“名称”列中。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-198">You will be back at the Import Wizard page, and the zip file name is displayed in the Name column.</span></span>

13.  <span data-ttu-id="bbe6c-199">在导入向导的右上角单击“导入!”</span><span class="sxs-lookup"><span data-stu-id="bbe6c-199">Click the **Import!**</span></span> <span data-ttu-id="bbe6c-200">按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-200">button in the upper right-hand corner of the Import Wizard.</span></span> <span data-ttu-id="bbe6c-201">此时将显示“导入库”对话框。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-201">The **Import Library** dialog is displayed.</span></span>

14.  <span data-ttu-id="bbe6c-202">确保目标路径与创建的项目名称匹配，然后单击“导入”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-202">Ensure that the target path matches the name of the project you created and then click **Import**.</span></span>

  <span data-ttu-id="bbe6c-203">***注意：****目标路径与从主菜单中选择“导入”之前，最后一次选择的程序名称匹配。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-203">***NOTE:*** *The target path matches the name of the program that was last selected before Import was selected from the main menu.*</span></span>

15.  <span data-ttu-id="bbe6c-204">打开 **iothub\_client\_sample\_amqp.c** 文件，将 \[Iothub connection string\] 替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-204">Open **iothub\_client\_sample\_amqp.c** file and replace the \[Iothub connection string\] with your device connection string.</span></span> <span data-ttu-id="bbe6c-205">可根据[步骤 2](#Step-2-Register) 中所述，从 DeviceExplorer 获取此连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-205">You can get this from DeviceExplorer as explained in [Step 2](#Step-2-Register).</span></span>

16.  <span data-ttu-id="bbe6c-206">在“程序工作区”窗格中突出显示你的项目，然后再次单击“导入”菜单项。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-206">Highlight your project in the Program Workspace pane and click the **Import** menu item again.</span></span>

17.  <span data-ttu-id="bbe6c-207">在窗口顶部，单击“单击此处”链接从某个 URL 导入库。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-207">At the top of the window, click the **Click Here** link to import from a URL.</span></span> <span data-ttu-id="bbe6c-208">此时将显示“导入库”对话框。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-208">The **Import Library** dialog appears.</span></span>

       ![](images/3_2_04.png)

18.  <span data-ttu-id="bbe6c-209">在“源 URL”字段中输入以下 URL。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-209">Enter the following URL into the Source URL field.</span></span>

          http://developer.mbed.org/users/donatien/code/NTPClient/

19.  <span data-ttu-id="bbe6c-210">完成后，单击“导入”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-210">Once done click **Import**.</span></span>

       ![](images/3_2_05.png)

20.  <span data-ttu-id="bbe6c-211">重复步骤 16 和 17，在“源 URL”字段中输入以下 URL。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-211">Repeat Steps 16 and 17 and enter the following URL into the Source URL field.</span></span> <span data-ttu-id="bbe6c-212">完成后，单击“导入”：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-212">Once done click **Import**:</span></span>

         https://developer.mbed.org/users/wolfSSL/code/wolfSSL/
         http://developer.mbed.org/users/mbed_official/code/EthernetInterface/
         http://developer.mbed.org/users/mbed_official/code/mbed-rtos/
         http://mbed.org/users/mbed_official/code/mbed/

21.  <span data-ttu-id="bbe6c-213">重复步骤 16 和 17 导入 azure-uamqp-c 库，然后在“源 URL”字段中输入以下 URL。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-213">Import the azure-uamqp-c library by repeating Steps 16 and 17 and enter the following URL into the Source URL field.</span></span> <span data-ttu-id="bbe6c-214">完成后，单击“导入”：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-214">Once done click **Import**:</span></span>

         https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp_c/

22.  <span data-ttu-id="bbe6c-215">在主菜单中单击“编译”生成程序。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-215">Click **Compile** from main menu to build the program.</span></span> <span data-ttu-id="bbe6c-216">如果生成成功，将会生成包含项目名称的 .bin 文件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-216">If the build is successful, a .bin file with the name of your project will get generated.</span></span> <span data-ttu-id="bbe6c-217">在计算机上保存此文件，</span><span class="sxs-lookup"><span data-stu-id="bbe6c-217">Save this file on your machine.</span></span> <span data-ttu-id="bbe6c-218">因为后面的步骤将要用到。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-218">It will be used in next step.</span></span>
    <span data-ttu-id="bbe6c-219">![Import\_Library](images/3_2_06.png)</span><span class="sxs-lookup"><span data-stu-id="bbe6c-219">![Import\_Library](images/3_2_06.png)</span></span>

  <span data-ttu-id="bbe6c-220">***注意：****可以放心地忽略所有警告，但如果生成时出错，请先解决错误，然后继续。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-220">***Note:*** *You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.*</span></span>

<a name="Step-3-3-Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="bbe6c-221">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-221">3.3 Run and Validate the samples</span></span>

<span data-ttu-id="bbe6c-222">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-222">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="bbe6c-223">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-223">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="bbe6c-224">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-224">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="bbe6c-225">***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step-4-2-Share) 中需要用到这些屏幕截图。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-225">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step-4-2-Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="bbe6c-226">3.3.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="bbe6c-226">3.3.1 Send Device Events to IOT Hub</span></span>

1.  <span data-ttu-id="bbe6c-227">如[步骤 2](#Step-2-Register) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-227">Launch the DeviceExplorer as explained in [Step 2](#Step-2-Register) and navigate to **Data** tab.</span></span> <span data-ttu-id="bbe6c-228">从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-228">Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

     ![DeviceExplorer\_Monitor](images/3_3_1_01.PNG)

2.  <span data-ttu-id="bbe6c-230">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-230">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="bbe6c-231">将最后一个步骤生成的 .bin 文件复制到设备。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-231">Copy the .bin file generated in last step to the device.</span></span>

    <span data-ttu-id="bbe6c-232">***注意：****将 .bin 文件保存到设备会重置当前与设备建立的终端会话。重新连接设备时，请再次手动重置终端，或启动新的终端。这样，mbed 设备便会重置并开始执行程序。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-232">***Note:*** *Saving the .bin file to the device causes the current terminal session to the device to reset. When it reconnects, reset the terminal again manually, or start a new terminal. This enables the mbed device to reset and start executing the program.*</span></span>

4.  <span data-ttu-id="bbe6c-233">使用 PuTTY 等 SSH 终端程序连接到设备。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-233">Connect to the device using an SSH terminal program, such as PuTTY.</span></span> <span data-ttu-id="bbe6c-234">可以通过检查 Windows 设备管理器来确定设备使用的串行端口。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-234">You can determine which serial port your device uses by checking the Windows Device Manager.</span></span>

    ![Windows\_SerialPort](images/3_3_1_02.png)

5.  <span data-ttu-id="bbe6c-236">在 PuTTY 中，单击“**串行**”连接类型。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-236">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="bbe6c-237">设备很有可能以 115200 的速率进行连接，因此请在“速度”框中输入该值。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-237">The device most likely connects at 115200, so enter that value in the Speed box.</span></span>
    <span data-ttu-id="bbe6c-238">然后单击“打开”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-238">Then click Open.</span></span>

    ![PuTTY](images/3_3_1_03.png)

6.  <span data-ttu-id="bbe6c-240">iothub\_client\_sample\_amqp 程序开始执行。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-240">The iothub\_client\_sample\_amqp program starts executing.</span></span>

    ![Event\_Data](images/3_3_1_04.png)

    <span data-ttu-id="bbe6c-242">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-242">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="bbe6c-243">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-243">If not, then you may have incorrectly copied the device hub connection information.</span></span>

      <span data-ttu-id="bbe6c-244">***注意：****如果程序不启动，请手动重置开发板。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-244">***NOTE:*** *If the program does not starts, reset the board manually.*</span></span>

7. <span data-ttu-id="bbe6c-245">DeviceExplorer 的数据选项卡中应会显示收到的事件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-245">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

     ![Monitor\_Data](images/3_3_1_05.PNG)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="bbe6c-247">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="bbe6c-247">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="bbe6c-248">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-248">To verify that you can send messages from the IoT Hub to your device, go to the **Message To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="bbe6c-249">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-249">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="bbe6c-250">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-250">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Message](images/3_3_2_01.PNG)

4.  <span data-ttu-id="bbe6c-252">终端窗口中应会显示收到的消息。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-252">You should be able to see the message received in the terminal window.</span></span>

    ![Terminal\_MessageReceive](images/3_3_2_02.png)

<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="bbe6c-254">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="bbe6c-254">Step 4: Package and Share</span></span>

<a name="Step-4-1-Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="bbe6c-255">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="bbe6c-255">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="bbe6c-256">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="bbe6c-256">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="bbe6c-257">在 [mbed 开发人员站点](https://developer.mbed.org/)上编译时生成的生成结果屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-257">Screenshot for the build results generated while compiling on the [mbed developer's site](https://developer.mbed.org/).</span></span>
2.  <span data-ttu-id="bbe6c-258">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-258">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>
2.  <span data-ttu-id="bbe6c-259">前面“**从 IoT 中心接收消息**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-259">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>
3.  <span data-ttu-id="bbe6c-260">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-260">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="bbe6c-261">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) github 存储库中发布的示例</span><span class="sxs-lookup"><span data-stu-id="bbe6c-261">As a guideline on how the instructions should look please refer the examples published on github repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>)</span></span>

<a name="Step-4-2-Share"></a>
## <a name="42-share-package-with-engineering-support"></a><span data-ttu-id="bbe6c-262">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="bbe6c-262">4.2 Share package with Engineering Support</span></span>

1.  <span data-ttu-id="bbe6c-263">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="bbe6c-263">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="bbe6c-264">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-264">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="bbe6c-266">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-266">This will open an upload dialog.</span></span> <span data-ttu-id="bbe6c-267">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-267">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="bbe6c-269">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-269">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="bbe6c-270">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-270">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="bbe6c-271">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="bbe6c-271">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step-4-3-Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="bbe6c-272">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="bbe6c-272">4.3 Next steps</span></span>

<span data-ttu-id="bbe6c-273">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-273">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="bbe6c-274">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="bbe6c-274">Step 5: Troubleshooting</span></span>

<span data-ttu-id="bbe6c-275">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="bbe6c-275">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
