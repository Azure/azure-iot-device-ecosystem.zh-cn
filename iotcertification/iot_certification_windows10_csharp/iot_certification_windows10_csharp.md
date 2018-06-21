<a name="how-to-certify-iot-devices-running-windows-10-with-azure-iot-sdk"></a><span data-ttu-id="fbc1a-101">如何使用 Azure IoT SDK 认证运行 Windows 10 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="fbc1a-101">How to certify IoT devices running Windows 10 with Azure IoT SDK</span></span> 
===
---


# <a name="table-of-contents"></a><span data-ttu-id="fbc1a-102">目录</span><span class="sxs-lookup"><span data-stu-id="fbc1a-102">Table of Contents</span></span>

-   [<span data-ttu-id="fbc1a-103">介绍</span><span class="sxs-lookup"><span data-stu-id="fbc1a-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="fbc1a-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="fbc1a-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1:_Sign_Up)
-   [<span data-ttu-id="fbc1a-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="fbc1a-105">Step 2: Register Device</span></span>](#Step_2:_Register)
-   [<span data-ttu-id="fbc1a-106">步骤 3：使用 C# 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="fbc1a-106">Step 3: Build and Validate the Sample using C# Client Libraries</span></span>](#Step_3:_Build_and_Validate)
    -   [<span data-ttu-id="fbc1a-107">3.1：准备开发环境</span><span class="sxs-lookup"><span data-stu-id="fbc1a-107">3.1 Prepare your development environment</span></span>](#Step_3_1:_Development)
    -   [<span data-ttu-id="fbc1a-108">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="fbc1a-108">3.2 Build the Samples</span></span>](#Step_3_2:_Build)
    -   [<span data-ttu-id="fbc1a-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="fbc1a-109">3.3 Run and Validate the Samples</span></span>](#Step_3_3:_Run)
-   [<span data-ttu-id="fbc1a-110">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="fbc1a-110">Step 4: Package and Share</span></span>](#Step_4:_Package_Share)
    -   [<span data-ttu-id="fbc1a-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="fbc1a-111">4.1 Package build logs and sample test results</span></span>](#Step_4_1:_Package)
    -   [<span data-ttu-id="fbc1a-112">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="fbc1a-112">4.2 Share package with Engineering Support</span></span>](#Step_4_2:_Share)
    -   [<span data-ttu-id="fbc1a-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="fbc1a-113">4.3 Next steps</span></span>](#Step_4_3:_Next)
-   [<span data-ttu-id="fbc1a-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="fbc1a-114">Step 5: Troubleshooting</span></span>](#Step_5:_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="fbc1a-115">介绍</span><span class="sxs-lookup"><span data-stu-id="fbc1a-115">Introduction</span></span>

<span data-ttu-id="fbc1a-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-116">**About this document**</span></span>

<span data-ttu-id="fbc1a-117">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-117">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="fbc1a-118">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-118">This multi-step process includes:</span></span>
-   <span data-ttu-id="fbc1a-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="fbc1a-119">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="fbc1a-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="fbc1a-120">Registering your IoT device</span></span>
-   <span data-ttu-id="fbc1a-121">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="fbc1a-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="fbc1a-122">打包和共享日志</span><span class="sxs-lookup"><span data-stu-id="fbc1a-122">Packaging and sharing the logs</span></span>  

<span data-ttu-id="fbc1a-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-123">**Prepare**</span></span>

<span data-ttu-id="fbc1a-124">在执行以下任何步骤之前，请先仔细阅读每个过程的每个步骤，确保对整个过程有全面的了解。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="fbc1a-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="fbc1a-126">一台装有 GitHub 的计算机，并且能够访问 [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub 公共存储库。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-126">Computer with GitHub installed and access to the [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub public repository.</span></span>
-   <span data-ttu-id="fbc1a-127">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-127">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="fbc1a-128">可以安装任何版本的 Visual Studio，包括免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-128">You can install any edition of Visual Studio, including the free Community edition.</span></span>

<a name="Step_1:_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="fbc1a-129">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="fbc1a-129">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="fbc1a-130">遵照[此处](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-130">Follow the instructions [here](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-csharp-csharp-getstarted#create-an-iot-hub) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="fbc1a-131">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-131">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="fbc1a-132">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-132">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2:_Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="fbc1a-133">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="fbc1a-133">Step 2: Register Device</span></span>

<span data-ttu-id="fbc1a-134">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-134">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="fbc1a-135">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-135">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="fbc1a-136">设备管理</span><span class="sxs-lookup"><span data-stu-id="fbc1a-136">Device management</span></span>
    -   <span data-ttu-id="fbc1a-137">创建新设备</span><span class="sxs-lookup"><span data-stu-id="fbc1a-137">Create new devices</span></span>
    -   <span data-ttu-id="fbc1a-138">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="fbc1a-138">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="fbc1a-139">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="fbc1a-139">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="fbc1a-140">提供删除设备的功能</span><span class="sxs-lookup"><span data-stu-id="fbc1a-140">Provides ability to delete a device</span></span>
-   <span data-ttu-id="fbc1a-141">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="fbc1a-141">Monitoring events from your device</span></span>
-   <span data-ttu-id="fbc1a-142">将消息发送到设备</span><span class="sxs-lookup"><span data-stu-id="fbc1a-142">Sending messages to your device</span></span>

<span data-ttu-id="fbc1a-143">若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step_1:_Sign_Up) 中所述的以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-143">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1:_Sign_Up):</span></span>

-   <span data-ttu-id="fbc1a-144">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="fbc1a-144">IoT Hub Connection String</span></span>

<span data-ttu-id="fbc1a-145">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-145">**Steps:**</span></span>

1.  <span data-ttu-id="fbc1a-146">单击[此处](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-146">Click [here](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/readme.md) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="fbc1a-147">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-147">Add connection information under the **Configuration** tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="fbc1a-148">使用以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-148">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="fbc1a-149">a.</span><span class="sxs-lookup"><span data-stu-id="fbc1a-149">a.</span></span> <span data-ttu-id="fbc1a-150">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-150">Click the **Management** tab.</span></span>    
    
    <span data-ttu-id="fbc1a-151">b.</span><span class="sxs-lookup"><span data-stu-id="fbc1a-151">b.</span></span> <span data-ttu-id="fbc1a-152">列表中会显示已注册的设备。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-152">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="fbc1a-153">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-153">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="fbc1a-154">如果这是第一次执行此操作，则不应检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-154">If this is your first time, then you shouldn't retrieve anything.</span></span>
       
    <span data-ttu-id="fbc1a-155">c.</span><span class="sxs-lookup"><span data-stu-id="fbc1a-155">c.</span></span> <span data-ttu-id="fbc1a-156">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-156">Click **Create** button to create a device ID and key.</span></span> 
    
    <span data-ttu-id="fbc1a-157">d.</span><span class="sxs-lookup"><span data-stu-id="fbc1a-157">d.</span></span> <span data-ttu-id="fbc1a-158">成功创建后，设备会列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-158">Once created successfully, device will be listed in DeviceExplorer.</span></span> 
    
    <span data-ttu-id="fbc1a-159">e.</span><span class="sxs-lookup"><span data-stu-id="fbc1a-159">e.</span></span> <span data-ttu-id="fbc1a-160">右键单击该设备，并从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-160">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>
    
    <span data-ttu-id="fbc1a-161">f.</span><span class="sxs-lookup"><span data-stu-id="fbc1a-161">f.</span></span> <span data-ttu-id="fbc1a-162">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-162">Save this information in Notepad.</span></span> <span data-ttu-id="fbc1a-163">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-163">You will need this information in later steps.</span></span>

<span data-ttu-id="fbc1a-164">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="fbc1a-164">***Not running Windows on your PC?***</span></span> <span data-ttu-id="fbc1a-165">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-165">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3:_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="fbc1a-166">步骤 3：使用 C# 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="fbc1a-166">Step 3: Build and Validate the Sample using C# Client Libraries</span></span> 

<span data-ttu-id="fbc1a-167">本部分逐步讲解如何在运行 Windows 10 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-167">This section walks you through building, deploying and validating the IoT Client SDK on your device running Windows 10 operating system.</span></span> <span data-ttu-id="fbc1a-168">我们将在设备上安装所需的必备组件。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-168">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="fbc1a-169">完成后，将会生成并部署 IoT 客户端 SDK，并使用 Azure IoT SDK 来验证 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-169">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1:_Development"></a>
## <a name="31-prepare-your-development-environment"></a><span data-ttu-id="fbc1a-170">3.1：准备开发环境</span><span class="sxs-lookup"><span data-stu-id="fbc1a-170">3.1 Prepare your development environment</span></span>

- <span data-ttu-id="fbc1a-171">从 https://dot.net 安装最新的 .NET Core</span><span class="sxs-lookup"><span data-stu-id="fbc1a-171">Install the latest .NET Core from https://dot.net</span></span>
- <span data-ttu-id="fbc1a-172">安装 .NET Framework 4.7 开发人员包：https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs</span><span class="sxs-lookup"><span data-stu-id="fbc1a-172">Install .NET Framework 4.7 Developer Pack: https://support.microsoft.com/en-us/help/3186612/the-net-framework-4-7-developer-pack-and-language-packs</span></span>
- <span data-ttu-id="fbc1a-173">安装 .NET Framework 4.5.1 开发人员包：https://www.microsoft.com/en-us/download/details.aspx?id=40772</span><span class="sxs-lookup"><span data-stu-id="fbc1a-173">Install .NET Framework 4.5.1 Developer Pack: https://www.microsoft.com/en-us/download/details.aspx?id=40772</span></span>
- <span data-ttu-id="fbc1a-174">在系统上以管理员身份启用 Powershell 脚本执行（一次性设置）。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-174">As admin (one-time setup): Enable Powershell script execution on your system.</span></span> <span data-ttu-id="fbc1a-175">有关详细信息，请参阅 http://go.microsoft.com/fwlink/?LinkID=135170。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-175">See http://go.microsoft.com/fwlink/?LinkID=135170 for more information.</span></span>
    `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

<a name="Step_3_2:_Build"></a>
## <a name="32--build-the-samples"></a><span data-ttu-id="fbc1a-176">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="fbc1a-176">3.2  Build the Samples</span></span>

1.  <span data-ttu-id="fbc1a-177">打开设备控制台（命令提示符或 PowerShell 窗口），并切换到本地 SDK 的 **azure-iot-sdk-csharp** 目录。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-177">Open a device console (command prompt or a powershell window) and change to your local SDK **azure-iot-sdk-csharp** directory.</span></span>

2.  <span data-ttu-id="fbc1a-178">在设备上以环境变量的形式添加 IoT 中心设备连接字符串：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-178">Add the Iot Hub device connection string on your device as an environment variable:</span></span>

        setx IOTHUB_DEVICE_CONN_STRING <yourDeviceConnectionString>

3.  <span data-ttu-id="fbc1a-179">运行以下命令生成 SDK：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-179">Run the following command to build the SDK:</span></span>

        build.cmd -config Release

<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="fbc1a-180">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="fbc1a-180">3.3 Run and Validate the Samples</span></span>
    
<span data-ttu-id="fbc1a-181">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-181">In this section you will run the Azure IoT client SDK samples to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="fbc1a-182">我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-182">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="fbc1a-183">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-183">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="fbc1a-184">***注意：*** 请对本部分中执行的所有操作截图。在[步骤 4](#Step_4_2:_Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-184">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2:_Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="fbc1a-185">3.3.1：向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="fbc1a-185">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="fbc1a-186">如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-186">Launch the DeviceExplorer as explained in [Step 2](#Step_2:_Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="fbc1a-188">DeviceExplorer 现在正在监视从所选设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-188">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>
     

3.  <span data-ttu-id="fbc1a-189">在设备控制台中，使用以下命令运行示例：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-189">From the device console, run the sample using following command:</span></span>

    <span data-ttu-id="fbc1a-190">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-190">**If HTTP protocol:**</span></span>

        cd iothub\device\samples\DeviceClientHttpSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientHttpSample.dll

    <span data-ttu-id="fbc1a-191">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-191">**If MQTT protocol:**</span></span>

        cd iothub\device\samples\DeviceClientMqttSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientMqttSample.dll
        
    <span data-ttu-id="fbc1a-192">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-192">**If AMQP protocol:**</span></span>

        cd iothub\device\samples\DeviceClientAmqpSample\bin\Debug\netcoreapp2.0
        dotnet DeviceClientAmqpSample.dll
   
4. <span data-ttu-id="fbc1a-193">成功执行后，应会看到设备控制台中收到的事件。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-193">You should be able to see the events received in device console on successful execution.</span></span>

    <span data-ttu-id="fbc1a-194">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-194">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_http.png)

    <span data-ttu-id="fbc1a-196">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-196">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_mqtt.png)

    <span data-ttu-id="fbc1a-198">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-198">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_send_from_device_amqp.png)

5. <span data-ttu-id="fbc1a-200">应会看到 DeviceExplorer 的数据选项卡中收到的事件。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-200">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

    <span data-ttu-id="fbc1a-201">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-201">**If HTTP protocol:**</span></span>   

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_http.png)

    <span data-ttu-id="fbc1a-203">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-203">**If MQTT protocol:**</span></span>

     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_mqtt.png)

    <span data-ttu-id="fbc1a-205">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-205">**If AMQP protocol:**</span></span>
    
     ![DeviceExplorer\_Notification\_Send](images/device_message_send_from_device_amqp.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="fbc1a-207">3.3.2：从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="fbc1a-207">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="fbc1a-208">若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-208">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="fbc1a-209">使用“设备 ID”下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-209">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="fbc1a-210">在“消息”字段中添加一些文本，并单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-210">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_message_receive_from_device_http.png)

4. <span data-ttu-id="fbc1a-212">应会看到设备控制台窗口中收到的消息。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-212">You should be able to see the message received in the device console window.</span></span>
    
    <span data-ttu-id="fbc1a-213">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-213">**If HTTP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_http.png)

    <span data-ttu-id="fbc1a-215">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-215">**If MQTT protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_mqtt.png)

    <span data-ttu-id="fbc1a-217">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="fbc1a-217">**If AMQP protocol:**</span></span>

    ![DeviceExplorer\_Notification\_Send](images/terminal_message_receive_from_device_amqp.png)
    
<a name="Step_4:_Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="fbc1a-219">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="fbc1a-219">Step 4: Package and Share</span></span>

<a name="Step_4_1:_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="fbc1a-220">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="fbc1a-220">4.1 Package build logs and sample test results</span></span>
  
<span data-ttu-id="fbc1a-221">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="fbc1a-221">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="fbc1a-222">第 3.2 部分所述的生成日志。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-222">Build logs from section 3.2.</span></span>
2.  <span data-ttu-id="fbc1a-223">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-223">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>
3.  <span data-ttu-id="fbc1a-224">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-224">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>
4.  <span data-ttu-id="fbc1a-225">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-225">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="fbc1a-226">请使用[此处](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-csharp.md)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-226">Please use the template available [here](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-csharp.md) to create your device-specific instructions.</span></span>

    <span data-ttu-id="fbc1a-227">有关说明的大致形式的指导，请参阅[此](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started) github 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-227">As a guideline on how the instructions should look please refer the examples published on github repository [here](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started).</span></span>

<a name="Step_4_2:_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a><span data-ttu-id="fbc1a-228">4.2：与 Azure IoT 认证团队共享包</span><span class="sxs-lookup"><span data-stu-id="fbc1a-228">4.2 Share package with the Azure IoT Certification Team</span></span>

1.  <span data-ttu-id="fbc1a-229">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-229">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="fbc1a-230">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-230">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="fbc1a-232">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-232">This will open an upload dialog.</span></span> <span data-ttu-id="fbc1a-233">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-233">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="fbc1a-235">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-235">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="fbc1a-236">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-236">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="fbc1a-237">***注意：*** 提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-237">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3:_Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="fbc1a-238">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="fbc1a-238">4.3 Next steps</span></span>

<span data-ttu-id="fbc1a-239">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-239">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5:_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="fbc1a-240">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="fbc1a-240">Step 5: Troubleshooting</span></span>

<span data-ttu-id="fbc1a-241">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="fbc1a-241">Please contact engineering support on <iotcert@microsoft.com> for help with  troubleshooting.</span></span>
