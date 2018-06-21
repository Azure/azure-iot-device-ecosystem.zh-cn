<a name="how-to-certify-iot-devices-running-windows-10-iot-core-os-with-azure-iot-sdk"></a><span data-ttu-id="9bf2a-101">如何使用 Azure IoT SDK 认证运行 Windows 10 IoT core OS 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-101">How to Certify IoT devices running Windows 10 IoT core OS with Azure IoT SDK</span></span> 
===
---


# <a name="table-of-contents"></a><span data-ttu-id="9bf2a-102">目录</span><span class="sxs-lookup"><span data-stu-id="9bf2a-102">Table of Contents</span></span>

-   [<span data-ttu-id="9bf2a-103">介绍</span><span class="sxs-lookup"><span data-stu-id="9bf2a-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="9bf2a-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="9bf2a-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1:_Sign_Up)
-   [<span data-ttu-id="9bf2a-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-105">Step 2: Register Device</span></span>](#Step_2:_Register)
-   [<span data-ttu-id="9bf2a-106">步骤 3：使用 C# 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="9bf2a-106">Step 3: Build and Validate the Sample using C# Client Libraries</span></span>](#Step_3:_Build_and_Validate)
    -   [<span data-ttu-id="9bf2a-107">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-107">3.1 Connect the Device</span></span>](#Step_3_1:_Connect)
    -   [<span data-ttu-id="9bf2a-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="9bf2a-108">3.2 Build the Samples</span></span>](#Step_3_2:_Build)
    -   [<span data-ttu-id="9bf2a-109">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="9bf2a-109">3.3 Run and Validate the Samples</span></span>](#Step_3_3:_Run)
-   [<span data-ttu-id="9bf2a-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="9bf2a-110">Step 4: Package and Share</span></span>](#Step_4:_Package_Share)
    -   [<span data-ttu-id="9bf2a-111">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="9bf2a-111">4.1 Package build logs and sample test results</span></span>](#Step_4_1:_Package)
    -   [<span data-ttu-id="9bf2a-112">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="9bf2a-112">4.2 Share package with Engineering Support</span></span>](#Step_4_2:_Share)
    -   [<span data-ttu-id="9bf2a-113">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="9bf2a-113">4.3 Next steps</span></span>](#Step_4_3:_Next)
-   [<span data-ttu-id="9bf2a-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="9bf2a-114">Step 5: Troubleshooting</span></span>](#Step_5:_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="9bf2a-115">介绍</span><span class="sxs-lookup"><span data-stu-id="9bf2a-115">Introduction</span></span>

<span data-ttu-id="9bf2a-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="9bf2a-116">**About this document**</span></span>

<span data-ttu-id="9bf2a-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-117">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="9bf2a-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-118">This multi-step process includes:</span></span>
-   <span data-ttu-id="9bf2a-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="9bf2a-119">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="9bf2a-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-120">Registering your IoT device</span></span>
-   <span data-ttu-id="9bf2a-121">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="9bf2a-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="9bf2a-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="9bf2a-122">Packaging and sharing the logs</span></span>  

<span data-ttu-id="9bf2a-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="9bf2a-123">**Prepare**</span></span>

<span data-ttu-id="9bf2a-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="9bf2a-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="9bf2a-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-126">Computer with GitHub installed and access to the [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub public repository.</span></span>
-   <span data-ttu-id="9bf2a-127">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-127">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="9bf2a-128">可以安装任意版本的 Visual Studio，包括免费的 Community 版。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-128">You can install any edition of Visual Studio, including the free Community edition.</span></span>

    <span data-ttu-id="9bf2a-129">请务必选择“通用 Windows 应用开发工具”，这是编写 Windows 10 应用时必须使用的组件：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-129">Make sure to select the "Universal Windows App Development Tools", the component required for writing apps Windows 10:</span></span>
    
    ![安装\_所需的\_工具](images/vs_install_tools_for_windows10.png)
-   <span data-ttu-id="9bf2a-131">用于认证的、运行 Windows 10 IoT Core 的所需硬件</span><span class="sxs-lookup"><span data-stu-id="9bf2a-131">Required hardware running Windows 10 IoT Core to certify</span></span>

     <span data-ttu-id="9bf2a-132">***注意：****如果在安装 Windows 10 IoT Core 时需要帮助，请访问 <https://www.windowsondevices.com> 或者通过 <iotcert@microsoft.com>* 联系我们</span><span class="sxs-lookup"><span data-stu-id="9bf2a-132">***Note:*** *If you need assistance installing Windows 10 IoT Core , please visit <https://www.windowsondevices.com> or contact us at <iotcert@microsoft.com>*</span></span>

<a name="Step_1:_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="9bf2a-133">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="9bf2a-133">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="9bf2a-134">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-134">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="9bf2a-135">在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-135">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="9bf2a-136">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-136">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2:_Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="9bf2a-137">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-137">Step 2: Register Device</span></span>

<span data-ttu-id="9bf2a-138">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-138">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="9bf2a-139">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-139">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="9bf2a-140">设备管理</span><span class="sxs-lookup"><span data-stu-id="9bf2a-140">Device management</span></span>
    -   <span data-ttu-id="9bf2a-141">创建新设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-141">Create new devices</span></span>
    -   <span data-ttu-id="9bf2a-142">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="9bf2a-142">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="9bf2a-143">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="9bf2a-143">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="9bf2a-144">可删除设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-144">Provides ability to delete a device</span></span>
-   <span data-ttu-id="9bf2a-145">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="9bf2a-145">Monitoring events from your device</span></span>
-   <span data-ttu-id="9bf2a-146">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="9bf2a-146">Sending messages to your device</span></span>

<span data-ttu-id="9bf2a-147">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1:_Sign_Up) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-147">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1:_Sign_Up):</span></span>

-   <span data-ttu-id="9bf2a-148">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="9bf2a-148">IoT Hub Connection String</span></span>

<span data-ttu-id="9bf2a-149">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="9bf2a-149">**Steps:**</span></span>

1.  <span data-ttu-id="9bf2a-150">单击[此处](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-150">Click [here](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="9bf2a-151">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-151">Add connection information under the **Configuration** tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="9bf2a-152">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-152">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="9bf2a-153">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-153">a.</span></span> <span data-ttu-id="9bf2a-154">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-154">Click the **Management** tab.</span></span>    
    
    <span data-ttu-id="9bf2a-155">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-155">b.</span></span> <span data-ttu-id="9bf2a-156">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-156">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="9bf2a-157">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-157">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="9bf2a-158">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-158">If this is your first time, then you shouldn't retrieve anything.</span></span>
       
    <span data-ttu-id="9bf2a-159">c.</span><span class="sxs-lookup"><span data-stu-id="9bf2a-159">c.</span></span> <span data-ttu-id="9bf2a-160">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-160">Click **Create** button to create a device ID and key.</span></span> 
    
    <span data-ttu-id="9bf2a-161">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-161">d.</span></span> <span data-ttu-id="9bf2a-162">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-162">Once created successfully, device will be listed in DeviceExplorer.</span></span> 
    
    <span data-ttu-id="9bf2a-163">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-163">e.</span></span> <span data-ttu-id="9bf2a-164">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-164">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>
    
    <span data-ttu-id="9bf2a-165">f.</span><span class="sxs-lookup"><span data-stu-id="9bf2a-165">f.</span></span> <span data-ttu-id="9bf2a-166">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-166">Save this information in Notepad.</span></span> <span data-ttu-id="9bf2a-167">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-167">You will need this information in later steps.</span></span>

<span data-ttu-id="9bf2a-168">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="9bf2a-168">***Not running Windows on your PC?***</span></span> <span data-ttu-id="9bf2a-169">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-169">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3:_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="9bf2a-170">步骤 3：使用 C# 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="9bf2a-170">Step 3: Build and Validate the Sample using C# Client Libraries</span></span> 

<span data-ttu-id="9bf2a-171">本部分逐步讲解如何在运行 Windows 10 IoT Core 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-171">This section walks you through building, deploying and validating the IoT Client SDK on your device running Windows 10 IoT Core operating system.</span></span> <span data-ttu-id="9bf2a-172">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-172">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="9bf2a-173">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-173">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1:_Connect"></a>
## <a name="31-connect-the-device"></a><span data-ttu-id="9bf2a-174">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="9bf2a-174">3.1 Connect the Device</span></span>

1.  <span data-ttu-id="9bf2a-175">使用以太网电缆将开发板连接到网络。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-175">Connect the board to your network using an Ethernet cable.</span></span> <span data-ttu-id="9bf2a-176">由于示例依赖于 Internet 访问，因此必须执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-176">This step is required, as the sample depends on internet access.</span></span>

2.  <span data-ttu-id="9bf2a-177">使用 micro-USB 电缆将设备插入计算机。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-177">Plug the device into your computer using a micro-USB cable.</span></span>

<a name="Step_3_2:_Build"></a>
## <a name="32--build-the-samples"></a><span data-ttu-id="9bf2a-178">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="9bf2a-178">3.2  Build the Samples</span></span>

1. <span data-ttu-id="9bf2a-179">将 [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp.git) 存储库克隆到计算机。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-179">Clone [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-csharp.git) repository to your machine.</span></span>

2.  <span data-ttu-id="9bf2a-180">启动 Visual Studio 2015 的新实例。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-180">Start a new instance of Visual Studio 2015.</span></span> <span data-ttu-id="9bf2a-181">打开存储库本地副本中的 **iothub_csharp_client.sln** 解决方案 (/azure-iot-sdk-csharp/device)。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-181">Open the **iothub_csharp_client.sln** solution (/azure-iot-sdk-csharp/device) from your local copy of the repository.</span></span>

3.  <span data-ttu-id="9bf2a-182">在 Visual Studio 的“解决方案资源管理器”中，导航到 **UWPSample(Universal Windows)** 项目。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-182">In Visual Studio, from **Solution Explorer**, navigate to the **UWPSample(Universal Windows)** project.</span></span>

4.  <span data-ttu-id="9bf2a-183">在 **ConnectionStrings.cs** 文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-183">Locate the following code in the **ConnectionStrings.cs** file:</span></span>

        public const string DeviceConnectionString = "<replace>";

5.  <span data-ttu-id="9bf2a-184">将 `<replace>` 替换为设备的连接字符串，然后**保存**更改。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-184">Replace `<replace>` with the connection string for your device and **Save** the changes.</span></span> <span data-ttu-id="9bf2a-185">如[步骤 2](#Step_2:_Register) 中所述，可从 DeviceExplorer 获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-185">You can get the connection string from DeviceExplorer as explained in [Step 2](#Step_2:_Register).</span></span>

6.  <span data-ttu-id="9bf2a-186">选择适当的体系结构（x86 或 ARM，具体取决于设备），将调试方法设置为“远程计算机”：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-186">Choose the right architecture (x86 or ARM, depending on your device) and set the debugging method to "Remote Machine":</span></span>

    ![VisualStudio\_Select\_Architecture](images/vs_select_arch.png)
    
7.  <span data-ttu-id="9bf2a-188">若要在设备上部署二进制文件，请在“解决方案资源管理器”中右键单击 UWPSample 项目，选择“属性”，然后导航到“调试”选项卡：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-188">To deploy the binaries on your device, right-click on the UWPSample project in the **Solution Explorer**, select **Properties** and navigate to the **Debug** tab:</span></span>

    ![VisualStudio\_Properties\_Debug](images/vs_properties_debug.png)

    <span data-ttu-id="9bf2a-190">键入设备的名称。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-190">Type in the name of your device.</span></span> <span data-ttu-id="9bf2a-191">确保“使用身份验证”框处于未选中状态。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-191">Make sure the "Use authentication" box is unchecked.</span></span>

8.  <span data-ttu-id="9bf2a-192">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-192">Build the solution.</span></span>


<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="9bf2a-193">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="9bf2a-193">3.3 Run and Validate the Samples</span></span>
    
<span data-ttu-id="9bf2a-194">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-194">In this section you will run the Azure IoT client SDK samples to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="9bf2a-195">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-195">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="9bf2a-196">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-196">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="9bf2a-197">***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2:_Share) 中需要用到这些屏幕截图。*</span><span class="sxs-lookup"><span data-stu-id="9bf2a-197">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2:_Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="9bf2a-198">3.3.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="9bf2a-198">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="9bf2a-199">如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-199">Launch the DeviceExplorer as explained in [Step 2](#Step_2:_Register) and navigate to **Data** tab.</span></span> <span data-ttu-id="9bf2a-200">从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-200">Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_Monitor](images/device_explorer_monitor.png)

2.  <span data-ttu-id="9bf2a-202">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-202">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>
     

3.  <span data-ttu-id="9bf2a-203">在 Visual Studio 的“解决方案资源管理器”中右键单击“UWPSample(Universal Windows)”项目，然后单击“调试”&minus;&gt;“启动新实例”生成并运行示例。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-203">In Visual Studio, from **Solution Explorer**, right-click the **UWPSample(Universal Windows)** project, click **Debug &minus;&gt; Start new instance** to build and run the sample.</span></span> 

       
4. <span data-ttu-id="9bf2a-204">DeviceExplorer 的数据选项卡中应会显示收到的事件。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-204">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

    ![DeviceExplorer\_Events\_Received](images/device_explorer_message_received.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="9bf2a-206">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="9bf2a-206">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="9bf2a-207">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-207">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="9bf2a-208">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-208">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="9bf2a-209">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-209">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_explorer_notification_send.png)

4.  <span data-ttu-id="9bf2a-211">设备控制台窗口中应会显示收到的消息。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-211">You should be able to see the message received in the device console window.</span></span>
    
<a name="Step_4:_Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="9bf2a-212">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="9bf2a-212">Step 4: Package and Share</span></span>

<a name="Step_4_1:_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="9bf2a-213">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="9bf2a-213">4.1 Package build logs and sample test results</span></span>
  
<span data-ttu-id="9bf2a-214">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="9bf2a-214">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="9bf2a-215">第 3.2 部分中所述的生成日志。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-215">Build logs from section 3.2.</span></span>
2. <span data-ttu-id="9bf2a-216">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-216">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>
3.  <span data-ttu-id="9bf2a-217">前面“**从 IoT 中心接收消息**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-217">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>
4.  <span data-ttu-id="9bf2a-218">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-218">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="9bf2a-219">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-iotcore-csharp.md>)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-219">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-iotcore-csharp.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="9bf2a-220">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-220">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2:_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a><span data-ttu-id="9bf2a-221">4.2 与 Azure IoT 认证团队共享包</span><span class="sxs-lookup"><span data-stu-id="9bf2a-221">4.2 Share package with the Azure IoT Certification Team</span></span>

1.  <span data-ttu-id="9bf2a-222">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="9bf2a-222">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="9bf2a-223">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-223">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="9bf2a-225">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-225">This will open an upload dialog.</span></span> <span data-ttu-id="9bf2a-226">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-226">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="9bf2a-228">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-228">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="9bf2a-229">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-229">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="9bf2a-230">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="9bf2a-230">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3:_Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="9bf2a-231">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="9bf2a-231">4.3 Next steps</span></span>

<span data-ttu-id="9bf2a-232">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-232">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5:_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="9bf2a-233">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="9bf2a-233">Step 5: Troubleshooting</span></span>

<span data-ttu-id="9bf2a-234">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="9bf2a-234">Please contact engineering support on <iotcert@microsoft.com> for help with  troubleshooting.</span></span>
