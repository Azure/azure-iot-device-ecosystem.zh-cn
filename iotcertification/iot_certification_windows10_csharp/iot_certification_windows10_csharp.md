<a name="how-to-certify-iot-devices-running-windows-10-with-azure-iot-sdk"></a><span data-ttu-id="27286-101">如何使用 Azure IoT SDK 认证运行 Windows 10 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="27286-101">How to certify IoT devices running Windows 10 with Azure IoT SDK</span></span> 
===
---


# <a name="table-of-contents"></a><span data-ttu-id="27286-102">目录</span><span class="sxs-lookup"><span data-stu-id="27286-102">Table of Contents</span></span>

-   [<span data-ttu-id="27286-103">简介</span><span class="sxs-lookup"><span data-stu-id="27286-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="27286-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="27286-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1:_Sign_Up)
-   [<span data-ttu-id="27286-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="27286-105">Step 2: Register Device</span></span>](#Step_2:_Register)
-   [<span data-ttu-id="27286-106">步骤 3：使用 C# 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="27286-106">Step 3: Build and Validate the Sample using C# Client Libraries</span></span>](#Step_3:_Build_and_Validate)
    -   [<span data-ttu-id="27286-107">3.1：准备开发环境</span><span class="sxs-lookup"><span data-stu-id="27286-107">3.1 Prepare your development environment</span></span>](#Step_3_1:_Development)
    -   [<span data-ttu-id="27286-108">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="27286-108">3.2 Build the Samples</span></span>](#Step_3_2:_Build)
    -   [<span data-ttu-id="27286-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="27286-109">3.3 Run and Validate the Samples</span></span>](#Step_3_3:_Run)
    -   [<span data-ttu-id="27286-110">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="27286-110">3.4 Verify Device Configuration</span></span>](#Step3_4)
-   [<span data-ttu-id="27286-111">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="27286-111">Step 4: Package and Share</span></span>](#Step_4:_Package_Share)
    -   [<span data-ttu-id="27286-112">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="27286-112">4.1 Package build logs and sample test results</span></span>](#Step_4_1:_Package)
    -   [<span data-ttu-id="27286-113">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="27286-113">4.2 Share package with Engineering Support</span></span>](#Step_4_2:_Share)
    -   [<span data-ttu-id="27286-114">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="27286-114">4.3 Next steps</span></span>](#Step_4_3:_Next)
-   [<span data-ttu-id="27286-115">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="27286-115">Step 5: Troubleshooting</span></span>](#Step_5:_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="27286-116">简介</span><span class="sxs-lookup"><span data-stu-id="27286-116">Introduction</span></span>

<span data-ttu-id="27286-117">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="27286-117">**About this document**</span></span>

<span data-ttu-id="27286-118">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="27286-118">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="27286-119">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="27286-119">This multi-step process includes:</span></span>
-   <span data-ttu-id="27286-120">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="27286-120">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="27286-121">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="27286-121">Registering your IoT device</span></span>
-   <span data-ttu-id="27286-122">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="27286-122">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="27286-123">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="27286-123">Packaging and sharing the logs</span></span>  

<span data-ttu-id="27286-124">**准备**</span><span class="sxs-lookup"><span data-stu-id="27286-124">**Prepare**</span></span>

<span data-ttu-id="27286-125">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="27286-125">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="27286-126">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="27286-126">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="27286-127">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="27286-127">Computer with GitHub installed and access to the [azure-iot-sdk-csharp](https://github.com/Azure-Samples/azure-iot-samples-csharp) GitHub public repository.</span></span>
-   <span data-ttu-id="27286-128">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="27286-128">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="27286-129">可以安装任何版本的 Visual Studio，包括免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="27286-129">You can install any edition of Visual Studio, including the free Community edition.</span></span>

<a name="Step_1:_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="27286-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="27286-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="27286-131">遵照[此处](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="27286-131">Follow the instructions [here](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="27286-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="27286-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="27286-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="27286-133">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2:_Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="27286-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="27286-134">Step 2: Register Device</span></span>

<span data-ttu-id="27286-135">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="27286-135">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="27286-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="27286-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="27286-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="27286-137">Device management</span></span>
    -   <span data-ttu-id="27286-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="27286-138">Create new devices</span></span>
    -   <span data-ttu-id="27286-139">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="27286-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="27286-140">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="27286-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="27286-141">可删除设备</span><span class="sxs-lookup"><span data-stu-id="27286-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="27286-142">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="27286-142">Monitoring events from your device</span></span>
-   <span data-ttu-id="27286-143">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="27286-143">Sending messages to your device</span></span>

<span data-ttu-id="27286-144">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1:_Sign_Up) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="27286-144">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1:_Sign_Up):</span></span>

-   <span data-ttu-id="27286-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="27286-145">IoT Hub Connection String</span></span>

<span data-ttu-id="27286-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="27286-146">**Steps:**</span></span>

1.  <span data-ttu-id="27286-147">单击[此处](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="27286-147">Click [here](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="27286-148">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。  </span><span class="sxs-lookup"><span data-stu-id="27286-148">Add connection information under the **Configuration** tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="27286-149">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="27286-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="27286-150">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="27286-150">a.</span></span> <span data-ttu-id="27286-151">单击“管理”选项卡。 </span><span class="sxs-lookup"><span data-stu-id="27286-151">Click the **Management** tab.</span></span>    
    
    <span data-ttu-id="27286-152">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="27286-152">b.</span></span> <span data-ttu-id="27286-153">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="27286-153">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="27286-154">如果你的设备未显示在列表中，请单击“刷新”按钮。 </span><span class="sxs-lookup"><span data-stu-id="27286-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="27286-155">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="27286-155">If this is your first time, then you shouldn't retrieve anything.</span></span>
       
    <span data-ttu-id="27286-156">c.</span><span class="sxs-lookup"><span data-stu-id="27286-156">c.</span></span> <span data-ttu-id="27286-157">单击“创建”按钮创建设备 ID 和密钥。 </span><span class="sxs-lookup"><span data-stu-id="27286-157">Click **Create** button to create a device ID and key.</span></span> 
    
    <span data-ttu-id="27286-158">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="27286-158">d.</span></span> <span data-ttu-id="27286-159">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="27286-159">Once created successfully, device will be listed in DeviceExplorer.</span></span> 
    
    <span data-ttu-id="27286-160">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="27286-160">e.</span></span> <span data-ttu-id="27286-161">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。 </span><span class="sxs-lookup"><span data-stu-id="27286-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>
    
    <span data-ttu-id="27286-162">f.</span><span class="sxs-lookup"><span data-stu-id="27286-162">f.</span></span> <span data-ttu-id="27286-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="27286-163">Save this information in Notepad.</span></span> <span data-ttu-id="27286-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="27286-164">You will need this information in later steps.</span></span>

<span data-ttu-id="27286-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="27286-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="27286-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="27286-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3:_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="27286-167">步骤 3：使用 C# 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="27286-167">Step 3: Build and Validate the Sample using C# Client Libraries</span></span> 

<span data-ttu-id="27286-168">本部分逐步讲解如何在运行 Windows 10 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="27286-168">This section walks you through building, deploying and validating the IoT Client SDK on your device running Windows 10 operating system.</span></span> <span data-ttu-id="27286-169">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="27286-169">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="27286-170">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="27286-170">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1:_Development"></a>
## <a name="31-prepare-your-development-environment"></a><span data-ttu-id="27286-171">3.1：准备开发环境</span><span class="sxs-lookup"><span data-stu-id="27286-171">3.1 Prepare your development environment</span></span>

- <span data-ttu-id="27286-172">从 https://dot.net 安装最新的 .NET Core</span><span class="sxs-lookup"><span data-stu-id="27286-172">Install the latest .NET Core from https://dot.net</span></span>
- <span data-ttu-id="27286-173">安装 .NET Framework 4.7 开发人员包： https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs</span><span class="sxs-lookup"><span data-stu-id="27286-173">Install .NET Framework 4.7 Developer Pack: https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs</span></span>
- <span data-ttu-id="27286-174">安装 .NET Framework 4.5.1 开发人员包： https://www.microsoft.com/en-us/download/details.aspx?id=40772</span><span class="sxs-lookup"><span data-stu-id="27286-174">Install .NET Framework 4.5.1 Developer Pack: https://www.microsoft.com/en-us/download/details.aspx?id=40772</span></span>
- <span data-ttu-id="27286-175">以管理员身份（一次性设置）：在系统上启用 Powershell 脚本执行。</span><span class="sxs-lookup"><span data-stu-id="27286-175">As admin (one-time setup): Enable Powershell script execution on your system.</span></span> <span data-ttu-id="27286-176">有关详细信息，请参阅 http://go.microsoft.com/fwlink/?LinkID=135170 。</span><span class="sxs-lookup"><span data-stu-id="27286-176">See http://go.microsoft.com/fwlink/?LinkID=135170 for more information.</span></span>
    `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

<a name="Step_3_2:_Build"></a>
## <a name="32--build-the-samples"></a><span data-ttu-id="27286-177">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="27286-177">3.2  Build the Samples</span></span>

1.  <span data-ttu-id="27286-178">打开设备控制台（命令提示符或 powershell 窗口），并切换到本地 SDK 的 **azure-iot-samples-csharp-master** 目录。</span><span class="sxs-lookup"><span data-stu-id="27286-178">Open a device console (command prompt or a powershell window) and change to your local SDK **azure-iot-samples-csharp-master** directory.</span></span>

2.  <span data-ttu-id="27286-179">在设备上以环境变量的形式添加 IoT 中心设备连接字符串：</span><span class="sxs-lookup"><span data-stu-id="27286-179">Add the Iot Hub device connection string on your device as an environment variable:</span></span>

        setx IOTHUB_DEVICE_CONN_STRING <yourDeviceConnectionString>

3.  <span data-ttu-id="27286-180">运行以下命令生成 SDK：</span><span class="sxs-lookup"><span data-stu-id="27286-180">Run the following command to build the SDK:</span></span>

        build.cmd -config Release

<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="27286-181">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="27286-181">3.3 Run and Validate the Samples</span></span>
    
<span data-ttu-id="27286-182">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="27286-182">In this section you will run the Azure IoT client SDK samples to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="27286-183">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="27286-183">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="27286-184">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="27286-184">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="27286-185">\*\**注意：\*\*\*\*请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2:_Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="27286-185">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2:_Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="27286-186">3.3.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="27286-186">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="27286-187">如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。  从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。 </span><span class="sxs-lookup"><span data-stu-id="27286-187">Launch the DeviceExplorer as explained in [Step 2](#Step_2:_Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="27286-189">DeviceExplorer 现在正在监视从所选设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="27286-189">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>
     

3.  <span data-ttu-id="27286-190">在设备控制台中，使用以下命令运行示例：</span><span class="sxs-lookup"><span data-stu-id="27286-190">From the device console, run the sample using following command:</span></span>

        cd iot-hub\Samples\device\MessageSample\bin\Release\netcoreapp2.1
        dotnet MessageSample.dll
        
<span data-ttu-id="27286-191">**若要为不同的协议运行：**</span><span class="sxs-lookup"><span data-stu-id="27286-191">**To run for the different protocols:**</span></span> 

-   <span data-ttu-id="27286-192">请在设备上执行以下命令。</span><span class="sxs-lookup"><span data-stu-id="27286-192">Follow the below commands on device.</span></span>

        cd iot-hub\Samples\device\MessageSample
        notepad Program.cs

-   <span data-ttu-id="27286-193">这会启动文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="27286-193">This launches a text editor.</span></span> <span data-ttu-id="27286-194">向下滚动到协议信息。</span><span class="sxs-lookup"><span data-stu-id="27286-194">Scroll down to the protocol information.</span></span>
    
-   <span data-ttu-id="27286-195">找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="27286-195">Find the below code:</span></span>

        private static TransportType s_transportType = TransportType.Amqp;
    
    <span data-ttu-id="27286-196">使用的默认协议为 AMQP。</span><span class="sxs-lookup"><span data-stu-id="27286-196">The default protocol used is AMQP.</span></span> <span data-ttu-id="27286-197">脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。</span><span class="sxs-lookup"><span data-stu-id="27286-197">Code for other protocols(HTTP/MQTT) are mentioned just below the above line in the script.</span></span>
    <span data-ttu-id="27286-198">根据要使用的协议对该行进行注释/取消注释，然后按 Ctrl + S 保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="27286-198">Comment/Uncomment the line as per the protocol you want to use and Save the changes by pressing Ctrl+S.</span></span>
    
    <span data-ttu-id="27286-199">我们需要生成该应用以便应用这些更改。</span><span class="sxs-lookup"><span data-stu-id="27286-199">We need to build the app to apply the changes.</span></span> <span data-ttu-id="27286-200">为此，请再次按[步骤 3.2](#Step_3_2:_Build) 中的步骤执行操作。</span><span class="sxs-lookup"><span data-stu-id="27286-200">For that follow the steps again from [Step 3.2](#Step_3_2:_Build).</span></span>

<span data-ttu-id="27286-201">\*\**注意：\*\*\*\*如果遇到与“FileUploadSample”部分相关的任何生成问题，请忽略，并且继续执行步骤。*</span><span class="sxs-lookup"><span data-stu-id="27286-201">***Note:*** *Ignore if you face any build issues related to the “FileUploadSample” section and continue the steps.*</span></span>
   
4. <span data-ttu-id="27286-202">成功执行后，应会看到设备控制台中收到的事件。</span><span class="sxs-lookup"><span data-stu-id="27286-202">You should be able to see the events received in device console on successful execution.</span></span>

    <span data-ttu-id="27286-203">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-203">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_http.png)

    <span data-ttu-id="27286-205">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-205">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_mqtt.png)

    <span data-ttu-id="27286-207">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-207">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_amqp.png)

5. <span data-ttu-id="27286-209">DeviceExplorer 的数据选项卡中应会显示收到的事件。</span><span class="sxs-lookup"><span data-stu-id="27286-209">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

    <span data-ttu-id="27286-210">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-210">**If HTTP protocol:**</span></span>   

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_http.png)

    <span data-ttu-id="27286-212">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-212">**If MQTT protocol:**</span></span>

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_mqtt.png)

    <span data-ttu-id="27286-214">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-214">**If AMQP protocol:**</span></span>
    
     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_amqp.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="27286-216">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="27286-216">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="27286-217">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。 </span><span class="sxs-lookup"><span data-stu-id="27286-217">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="27286-218">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="27286-218">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="27286-219">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="27286-219">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_message_receive_from_device_http.png)

4. <span data-ttu-id="27286-221">设备控制台窗口中应会显示收到的消息。</span><span class="sxs-lookup"><span data-stu-id="27286-221">You should be able to see the message received in the device console window.</span></span>
    
    <span data-ttu-id="27286-222">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-222">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

    <span data-ttu-id="27286-224">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-224">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_mqtt.png)

    <span data-ttu-id="27286-226">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="27286-226">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_amqp.png)
    
<a name="#Step3_4"></a>
### <a name="34-verify-device-configuration"></a><span data-ttu-id="27286-228">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="27286-228">3.4 Verify Device configuration</span></span>

-  <span data-ttu-id="27286-229">在设备上以管理员身份打开 PowerShell 命令提示符，然后运行以下命令</span><span class="sxs-lookup"><span data-stu-id="27286-229">Open PowerShell command prompt as an Administrator on your device and run the below commands</span></span>

-   <span data-ttu-id="27286-230">首先使用以下命令检查 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="27286-230">First check your PowerShell version by using the following command.</span></span>

        $PSversionTable

-  <span data-ttu-id="27286-231">如果你的当前 PowerShell 版本低于 5.0，请从[此处](https://aka.ms/wmf5download)下载 PowerShell 最新版本</span><span class="sxs-lookup"><span data-stu-id="27286-231">If your current PowerShell version is less than 5.0 then download the PowerShell latest version from [here](https://aka.ms/wmf5download)</span></span>

    <span data-ttu-id="27286-232">安装后，请验证新安装的版本，它应为版本 5.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="27286-232">After installation please verify the newly installed version, it should be version 5.1 or greater.</span></span> 

-   <span data-ttu-id="27286-233">运行以下命令来获取设备配置信息。</span><span class="sxs-lookup"><span data-stu-id="27286-233">Run the commands below to get device configuration information.</span></span>

        Get-ComputerInfo -property BiosBIOSVersion, BiosManufacturer, BiosSeralNumber, CsManufacturer, CsModel, CsName, CsNumberOfProcessors, CsProcessors, CsSystemSKUNumber, CsSystemType, OsOperatingSystemSKU | Format-List
          
        Get-NetAdapter
    
    <span data-ttu-id="27286-234">**如果设备已与以太网连接**</span><span class="sxs-lookup"><span data-stu-id="27286-234">**If Device connected with Ethernet**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Ethernet" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

    <span data-ttu-id="27286-235">**如果设备已与 Wi-Fi 连接**</span><span class="sxs-lookup"><span data-stu-id="27286-235">**If Device connected with Wi-fi**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Wi-fi" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

- <span data-ttu-id="27286-236">请查看下面的输出屏幕截图</span><span class="sxs-lookup"><span data-stu-id="27286-236">Please find the output screenshot below</span></span>

    ![deviceinfo\_screenshot](./images/device_configuration.png)

-   <span data-ttu-id="27286-238">请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="27286-238">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Package).</span></span>

<a name="Step_4:_Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="27286-239">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="27286-239">Step 4: Package and Share</span></span>

<a name="Step_4_1:_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="27286-240">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="27286-240">4.1 Package build logs and sample test results</span></span>
  
<span data-ttu-id="27286-241">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="27286-241">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="27286-242">第 3.2 部分中所述的生成日志。</span><span class="sxs-lookup"><span data-stu-id="27286-242">Build logs from section 3.2.</span></span>
2.  <span data-ttu-id="27286-243">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="27286-243">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>
3.  <span data-ttu-id="27286-244">前面“**从 IoT 中心接收消息**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="27286-244">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>
4.  <span data-ttu-id="27286-245">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="27286-245">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="27286-246">请使用[此处](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-csharp.md)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="27286-246">Please use the template available [here](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-csharp.md) to create your device-specific instructions.</span></span>

    <span data-ttu-id="27286-247">有关说明形式的指导，请参考[此处](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started) github 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="27286-247">As a guideline on how the instructions should look please refer the examples published on github repository [here](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started).</span></span>

<a name="Step_4_2:_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a><span data-ttu-id="27286-248">4.2 与 Azure IoT 认证团队共享包</span><span class="sxs-lookup"><span data-stu-id="27286-248">4.2 Share package with the Azure IoT Certification Team</span></span>

1.  <span data-ttu-id="27286-249">转到 [合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="27286-249">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="27286-250">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="27286-250">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="27286-252">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="27286-252">This will open an upload dialog.</span></span> <span data-ttu-id="27286-253">单击“上载”按钮浏览文件。 </span><span class="sxs-lookup"><span data-stu-id="27286-253">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="27286-255">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="27286-255">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="27286-256">上传所有文件后，单击“提交审查”按钮。 </span><span class="sxs-lookup"><span data-stu-id="27286-256">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="27286-257">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="27286-257">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3:_Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="27286-258">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="27286-258">4.3 Next steps</span></span>

<span data-ttu-id="27286-259">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="27286-259">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5:_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="27286-260">步骤 5：疑难解答</span><span class="sxs-lookup"><span data-stu-id="27286-260">Step 5: Troubleshooting</span></span>

<span data-ttu-id="27286-261">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="27286-261">Please contact engineering support on <iotcert@microsoft.com> for help with  troubleshooting.</span></span>
