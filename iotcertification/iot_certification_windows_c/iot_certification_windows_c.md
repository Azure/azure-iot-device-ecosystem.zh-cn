<a name="how-to-certify-iot-devices-running-windows-with-azure-iot-sdk"></a><span data-ttu-id="0bcad-101">如何使用 Azure IoT SDK 认证运行 Windows 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-101">How to certify IoT devices running Windows with Azure IoT SDK</span></span> 
===
---


# <a name="table-of-contents"></a><span data-ttu-id="0bcad-102">目录</span><span class="sxs-lookup"><span data-stu-id="0bcad-102">Table of Contents</span></span>

-   [<span data-ttu-id="0bcad-103">介绍</span><span class="sxs-lookup"><span data-stu-id="0bcad-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="0bcad-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="0bcad-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1_Sign_Up)
-   [<span data-ttu-id="0bcad-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-105">Step 2: Register Device</span></span>](#Step_2_Register)
-   [<span data-ttu-id="0bcad-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="0bcad-106">Step 3: Build and Validate the Sample using C Client Libraries</span></span>](#Step_3_Build_and_Validate)
    -   [<span data-ttu-id="0bcad-107">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-107">3.1 Connect the Device</span></span>](#Step_3_1_Connect)
    -   [<span data-ttu-id="0bcad-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="0bcad-108">3.2 Build the Samples</span></span>](#Step_3_2_Build)
    -   [<span data-ttu-id="0bcad-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="0bcad-109">3.3 Run and Validate the Samples</span></span>](#Step_3_3_Run)
    -   [<span data-ttu-id="0bcad-110">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="0bcad-110">3.4 Verify Device Configuration</span></span>](#Step3_4)
-   [<span data-ttu-id="0bcad-111">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="0bcad-111">Step 4: Package and Share</span></span>](#Step_4_Package_Share)
    -   [<span data-ttu-id="0bcad-112">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="0bcad-112">4.1 Package build logs and sample test results</span></span>](#Step_4_1_Package)
    -   [<span data-ttu-id="0bcad-113">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="0bcad-113">4.2 Share package with Engineering Support</span></span>](#Step_4_2_Share)
    -   [<span data-ttu-id="0bcad-114">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="0bcad-114">4.3 Next steps</span></span>](#Step_4_3_Next)
-   [<span data-ttu-id="0bcad-115">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="0bcad-115">Step 5: Troubleshooting</span></span>](#Step_5_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="0bcad-116">介绍</span><span class="sxs-lookup"><span data-stu-id="0bcad-116">Introduction</span></span>

<span data-ttu-id="0bcad-117">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="0bcad-117">**About this document**</span></span>

<span data-ttu-id="0bcad-118">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-118">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="0bcad-119">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="0bcad-119">This multi-step process includes:</span></span>
-   <span data-ttu-id="0bcad-120">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="0bcad-120">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="0bcad-121">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-121">Registering your IoT device</span></span>
-   <span data-ttu-id="0bcad-122">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="0bcad-122">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="0bcad-123">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="0bcad-123">Packaging and sharing the logs</span></span>  

<span data-ttu-id="0bcad-124">**准备**</span><span class="sxs-lookup"><span data-stu-id="0bcad-124">**Prepare**</span></span>

<span data-ttu-id="0bcad-125">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="0bcad-125">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span> 

<span data-ttu-id="0bcad-126">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="0bcad-126">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="0bcad-127">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="0bcad-127">Computer with GitHub installed and access to the [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub public repository.</span></span>
-   <span data-ttu-id="0bcad-128">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="0bcad-128">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="0bcad-129">可以安装任何版本的 Visual Studio，包括免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="0bcad-129">You can install any edition of Visual Studio, including the free Community edition.</span></span>

<a name="Step_1_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="0bcad-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="0bcad-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="0bcad-131">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="0bcad-131">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="0bcad-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="0bcad-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="0bcad-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="0bcad-133">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2_Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="0bcad-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-134">Step 2: Register Device</span></span>

<span data-ttu-id="0bcad-135">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="0bcad-135">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="0bcad-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="0bcad-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="0bcad-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="0bcad-137">Device management</span></span>
    -   <span data-ttu-id="0bcad-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-138">Create new devices</span></span>
    -   <span data-ttu-id="0bcad-139">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="0bcad-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="0bcad-140">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="0bcad-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="0bcad-141">提供删除设备的功能</span><span class="sxs-lookup"><span data-stu-id="0bcad-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="0bcad-142">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="0bcad-142">Monitoring events from your device</span></span>
-   <span data-ttu-id="0bcad-143">将消息发送到设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-143">Sending messages to your device</span></span>

<span data-ttu-id="0bcad-144">若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step_1_Sign_Up) 中所述的以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="0bcad-144">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1_Sign_Up):</span></span>

-   <span data-ttu-id="0bcad-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="0bcad-145">IoT Hub Connection String</span></span>

<span data-ttu-id="0bcad-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-146">**Steps:**</span></span>

1.  <span data-ttu-id="0bcad-147">单击[此处](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="0bcad-147">Click [here](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="0bcad-148">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="0bcad-148">Add connection information under the **Configuration** tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="0bcad-149">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="0bcad-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="0bcad-150">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-150">a.</span></span> <span data-ttu-id="0bcad-151">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="0bcad-151">Click the **Management** tab.</span></span>    
    
    <span data-ttu-id="0bcad-152">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-152">b.</span></span> <span data-ttu-id="0bcad-153">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="0bcad-153">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="0bcad-154">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="0bcad-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="0bcad-155">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-155">If this is your first time, then you shouldn't retrieve anything.</span></span>
       
    <span data-ttu-id="0bcad-156">c.</span><span class="sxs-lookup"><span data-stu-id="0bcad-156">c.</span></span> <span data-ttu-id="0bcad-157">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="0bcad-157">Click **Create** button to create a device ID and key.</span></span> 
    
    <span data-ttu-id="0bcad-158">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-158">d.</span></span> <span data-ttu-id="0bcad-159">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="0bcad-159">Once created successfully, device will be listed in DeviceExplorer.</span></span> 
    
    <span data-ttu-id="0bcad-160">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-160">e.</span></span> <span data-ttu-id="0bcad-161">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>
    
    <span data-ttu-id="0bcad-162">f.</span><span class="sxs-lookup"><span data-stu-id="0bcad-162">f.</span></span> <span data-ttu-id="0bcad-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-163">Save this information in Notepad.</span></span> <span data-ttu-id="0bcad-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-164">You will need this information in later steps.</span></span>

<span data-ttu-id="0bcad-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="0bcad-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="0bcad-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="0bcad-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="0bcad-167">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="0bcad-167">Step 3: Build and Validate the Sample using C Client Libraries</span></span> 

<span data-ttu-id="0bcad-168">本部分逐步讲解如何在运行 Windows 10 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="0bcad-168">This section walks you through building, deploying and validating the IoT Client SDK on your device running Windows 10 operating system.</span></span> <span data-ttu-id="0bcad-169">我们将在设备上安装所需的必备组件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-169">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="0bcad-170">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="0bcad-170">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1_Connect"></a>
## <a name="31-connect-the-device"></a><span data-ttu-id="0bcad-171">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="0bcad-171">3.1 Connect the Device</span></span>

1.  <span data-ttu-id="0bcad-172">使用以太网电缆将开发板连接到网络。</span><span class="sxs-lookup"><span data-stu-id="0bcad-172">Connect the board to your network using an Ethernet cable.</span></span> <span data-ttu-id="0bcad-173">由于示例依赖于 Internet 访问，因此必须执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="0bcad-173">This step is required, as the sample depends on internet access.</span></span>

2.  <span data-ttu-id="0bcad-174">使用 micro-USB 电缆将设备插入计算机。</span><span class="sxs-lookup"><span data-stu-id="0bcad-174">Plug the device into your computer using a micro-USB cable.</span></span>

<a name="Step_3_2_Build"></a>
## <a name="32--build-the-samples"></a><span data-ttu-id="0bcad-175">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="0bcad-175">3.2  Build the Samples</span></span>

1. <span data-ttu-id="0bcad-176">遵照[此处](<https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md>)的说明准备开发环境。</span><span class="sxs-lookup"><span data-stu-id="0bcad-176">Follow the instructions [here](<https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md>) to prepare your development environment.</span></span> 

2. <span data-ttu-id="0bcad-177">将在用户配置文件文件夹下创建 **cmake_Win32** 文件夹，例如 **c:\user\[yourusername]\cmake_Win32**。</span><span class="sxs-lookup"><span data-stu-id="0bcad-177">A folder **cmake_Win32** will be created under your user profile folder e.g. **c:\user\[yourusername]\cmake_Win32**.</span></span> 

3. <span data-ttu-id="0bcad-178">启动 Visual Studio 2015 的新实例。</span><span class="sxs-lookup"><span data-stu-id="0bcad-178">Start a new instance of Visual Studio 2015.</span></span> <span data-ttu-id="0bcad-179">打开 **cmake_Win32** 文件夹中的 **azure_iot_sdks.sln** 解决方案。</span><span class="sxs-lookup"><span data-stu-id="0bcad-179">Open the **azure_iot_sdks.sln** solution in the **cmake_Win32** folder.</span></span>

4.  <span data-ttu-id="0bcad-180">在 Visual Studio 的“解决方案资源管理器”中，根据所选的协议导航到相应的项目：</span><span class="sxs-lookup"><span data-stu-id="0bcad-180">In Visual Studio, from **Solution Explorer**, navigate to project based on your choice of protocol:</span></span>

    <span data-ttu-id="0bcad-181">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-181">**For AMQP protocol:**</span></span>

    <span data-ttu-id="0bcad-182">导航到 **simplesample_amqp** 项目，然后打开 **simplesample_amqp.c** 文件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-182">Navigate to **simplesample_amqp** project and open the **simplesample_amqp.c** file.</span></span>

    <span data-ttu-id="0bcad-183">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-183">**For HTTP protocol:**</span></span>
    
    <span data-ttu-id="0bcad-184">导航到 **simplesample_http** 项目，然后打开 **simplesample_http.c** 文件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-184">Navigate to **simplesample_http** project and open the **simplesample_http.c** file.</span></span>

    <span data-ttu-id="0bcad-185">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-185">**For MQTT protocol:**</span></span>
    
    <span data-ttu-id="0bcad-186">导航到 **simplesample_mqtt** 项目，然后打开 **simplesample_mqtt.c** 文件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-186">Navigate to **simplesample_mqtt** project and open the **simplesample_mqtt.c** file.</span></span>

    ![Navigate\_file](images/navigate_simplesampleamqp.png)


5.  <span data-ttu-id="0bcad-188">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="0bcad-188">Find the following place holder for IoT connection string:</span></span>

        static const char* connectionString = "[device connection string]";
    
6.  <span data-ttu-id="0bcad-189">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="0bcad-189">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="0bcad-190">可根据[步骤 2](#Step_2_Register) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="0bcad-190">You can get this from DeviceExplorer as explained in [Step 2](#Step_2_Register), that you copied into Notepad.</span></span>

    ![Replace\_device\_connection\_string](images/project_amqp_config.png)

<a name="Step_3_3_Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="0bcad-192">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="0bcad-192">3.3 Run and Validate the Samples</span></span>
    
<span data-ttu-id="0bcad-193">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="0bcad-193">In this section you will run the Azure IoT client SDK samples to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="0bcad-194">我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="0bcad-194">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="0bcad-195">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-195">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="0bcad-196">**注意：** 请对本部分中执行的所有操作进行屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="0bcad-196">**Note:** Take screenshots of all the operations you will perform in this section.</span></span> <span data-ttu-id="0bcad-197">[步骤 4](#Step_4_2_Share) 中需要用到这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="0bcad-197">These will be needed in [Step 4](#Step_4_2_Share).</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="0bcad-198">3.3.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="0bcad-198">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="0bcad-199">如[步骤 2](#Step_2_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="0bcad-199">Launch the DeviceExplorer as explained in [Step 2](#Step_2_Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="0bcad-201">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="0bcad-201">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>
     
3.  <span data-ttu-id="0bcad-202">在 Visual Studio 的“解决方案资源管理器”中右键单击项目，然后单击“调试”->“启动新实例”生成并运行示例。</span><span class="sxs-lookup"><span data-stu-id="0bcad-202">In Visual Studio, from **Solution Explorer**, right-click on the project and click **Debug -> Start new instance** to build and run the sample.</span></span> 

    ![Debug\_start](images/project_amqp_debug.png)
       
4. <span data-ttu-id="0bcad-204">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-204">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="0bcad-205">如果没有，请检查设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-205">If not, then verify the device hub connection information.</span></span>

    <span data-ttu-id="0bcad-206">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-206">**If HTTP protocol:**</span></span>

    ![Console\_Notification\_Send\_http](images/terminal_message_send_from_device_http.png)

    <span data-ttu-id="0bcad-208">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-208">**If AMQP protocol:**</span></span>

    ![Console\_Notification\_Send\_amqp](images/terminal_message_send_from_device_amqp.png)

    <span data-ttu-id="0bcad-210">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-210">**If MQTT protocol:**</span></span>

    ![Console\_Notification\_Send\_mqtt](images/terminal_message_send_from_device_mqtt.png)

5. <span data-ttu-id="0bcad-212">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="0bcad-212">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="0bcad-213">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-213">**If HTTP protocol:**</span></span>   

    ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_http.png)

    <span data-ttu-id="0bcad-215">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-215">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_amqp.png)

    <span data-ttu-id="0bcad-217">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-217">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_mqtt.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="0bcad-219">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="0bcad-219">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="0bcad-220">若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="0bcad-220">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="0bcad-221">使用“设备 ID”下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="0bcad-221">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="0bcad-222">在“消息”字段中添加一些文本，并单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="0bcad-222">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/explorer_send_message_to_device.png)

4. <span data-ttu-id="0bcad-224">设备控制台窗口中应会显示收到的消息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-224">You should be able to see the message received in the device console window.</span></span>
    
    <span data-ttu-id="0bcad-225">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-225">**If using HTTP protocol:**</span></span>

    ![Console\_Notification\_Receive\_http](images/terminal_message_receive_from_device_http.png)

    <span data-ttu-id="0bcad-227">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-227">**If using AMQP protocol:**</span></span>

    ![Console\_Notification\_Receive\_amqp](images/terminal_message_receive_from_device_amqp.png)
    
    <span data-ttu-id="0bcad-229">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="0bcad-229">**If using MQTT protocol:**</span></span>

    ![Console\_Notification\_Receive\_mqtt](images/terminal_message_receive_from_device_mqtt.png)

<a name="#Step3_4"></a>
### <a name="34-verify-device-configuration"></a><span data-ttu-id="0bcad-231">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="0bcad-231">3.4 Verify Device configuration</span></span>

-  <span data-ttu-id="0bcad-232">在设备上以管理员身份打开 PowerShell 命令提示符，然后运行以下命令</span><span class="sxs-lookup"><span data-stu-id="0bcad-232">Open PowerShell command prompt as an Administrator on your device and run the below commands</span></span>

-   <span data-ttu-id="0bcad-233">首先使用以下命令检查 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="0bcad-233">First check your PowerShell version by using the following command.</span></span>

        $PSversionTable

-  <span data-ttu-id="0bcad-234">如果你的当前 PowerShell 版本低于 5.0，请从[此处](https://aka.ms/wmf5download)下载 PowerShell 最新版本</span><span class="sxs-lookup"><span data-stu-id="0bcad-234">If your current PowerShell version is less than 5.0 then download the PowerShell latest version from [here](https://aka.ms/wmf5download)</span></span>

    <span data-ttu-id="0bcad-235">安装后，请验证新安装的版本，它应为版本 5.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="0bcad-235">After installation please verify the newly installed version, it should be version 5.1 or greater.</span></span> 

-   <span data-ttu-id="0bcad-236">运行以下命令来获取设备配置信息。</span><span class="sxs-lookup"><span data-stu-id="0bcad-236">Run the commands below to get device configuration information.</span></span>

        Get-ComputerInfo -property BiosBIOSVersion, BiosManufacturer, BiosSeralNumber, CsManufacturer, CsModel, CsName, CsNumberOfProcessors, CsProcessors, CsSystemSKUNumber, CsSystemType, OsOperatingSystemSKU | Format-List
          
        Get-NetAdapter
    
    <span data-ttu-id="0bcad-237">**如果设备已与以太网连接**</span><span class="sxs-lookup"><span data-stu-id="0bcad-237">**If Device connected with Ethernet**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Ethernet" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

    <span data-ttu-id="0bcad-238">**如果设备已与 Wi-Fi 连接**</span><span class="sxs-lookup"><span data-stu-id="0bcad-238">**If Device connected with Wi-fi**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Wi-fi" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

- <span data-ttu-id="0bcad-239">请查看下面的输出屏幕截图</span><span class="sxs-lookup"><span data-stu-id="0bcad-239">Please find the output screenshot below</span></span>

    ![deviceinfo\_screenshot](images/device_configuration.png)

-   <span data-ttu-id="0bcad-241">请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="0bcad-241">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Package).</span></span>

<a name="Step_4_Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="0bcad-242">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="0bcad-242">Step 4: Package and Share</span></span>

<a name="Step_4_1_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="0bcad-243">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="0bcad-243">4.1 Package build logs and sample test results</span></span>
  
<span data-ttu-id="0bcad-244">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="0bcad-244">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="0bcad-245">第 3.2 部分所述的生成日志。</span><span class="sxs-lookup"><span data-stu-id="0bcad-245">Build logs from section 3.2.</span></span>
2. <span data-ttu-id="0bcad-246">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="0bcad-246">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>
3.  <span data-ttu-id="0bcad-247">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="0bcad-247">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>
4.  <span data-ttu-id="0bcad-248">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="0bcad-248">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="0bcad-249">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-c.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="0bcad-249">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-c.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="0bcad-250">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="0bcad-250">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a><span data-ttu-id="0bcad-251">4.2 与 Azure IoT 认证团队共享包</span><span class="sxs-lookup"><span data-stu-id="0bcad-251">4.2 Share package with the Azure IoT Certification Team</span></span>

1.  <span data-ttu-id="0bcad-252">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="0bcad-252">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="0bcad-253">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="0bcad-253">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="0bcad-255">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="0bcad-255">This will open an upload dialog.</span></span> <span data-ttu-id="0bcad-256">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-256">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="0bcad-258">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="0bcad-258">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="0bcad-259">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="0bcad-259">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="0bcad-260">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="0bcad-260">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3_Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="0bcad-261">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="0bcad-261">4.3 Next steps</span></span>

<span data-ttu-id="0bcad-262">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="0bcad-262">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="0bcad-263">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="0bcad-263">Step 5: Troubleshooting</span></span>

<span data-ttu-id="0bcad-264">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="0bcad-264">Please contact engineering support on <iotcert@microsoft.com> for help with  troubleshooting.</span></span>
