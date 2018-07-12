<a name="how-to-certify-iot-edge-devices-running-linux"></a><span data-ttu-id="5ab6f-101">如何认证运行 Linux 的 IoT Edge 设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-101">How to certify IoT Edge devices running Linux</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="5ab6f-102">目录</span><span class="sxs-lookup"><span data-stu-id="5ab6f-102">Table of Contents</span></span>

-   [<span data-ttu-id="5ab6f-103">介绍</span><span class="sxs-lookup"><span data-stu-id="5ab6f-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="5ab6f-104">步骤 1：配置 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="5ab6f-104">Step 1: Configure Azure IoT Edge</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="5ab6f-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="5ab6f-106">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="5ab6f-106">Step 3: Manual Test for Azure IoT Edge on device</span></span>](#Step-3-Manual)
    -   [<span data-ttu-id="5ab6f-107">3.1：IoT Edge 运行时</span><span class="sxs-lookup"><span data-stu-id="5ab6f-107">3.1 IoT Edge Runtime</span></span>](#Step-3-1-IoTEdgeRunTime)
    -   [<span data-ttu-id="5ab6f-108">3.2：设备管理</span><span class="sxs-lookup"><span data-stu-id="5ab6f-108">3.2 Device Management</span></span>](#Step-3-2-DeviceManagement)
    -   [<span data-ttu-id="5ab6f-109">3.3：安全性</span><span class="sxs-lookup"><span data-stu-id="5ab6f-109">3.3 Security </span></span>](#Step-3-3-Security)
-   [<span data-ttu-id="5ab6f-110">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="5ab6f-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="5ab6f-111">4.1：在原始包装中打包生成日志和设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-111">4.1 Package build logs and Device in original box</span></span>](#Step-4-1-Package-build)
    -   [<span data-ttu-id="5ab6f-112">4.2：与 Microsoft Azure IoT 团队成员共享包</span><span class="sxs-lookup"><span data-stu-id="5ab6f-112">4.2 Share package with Microsoft Azure IoT team</span></span>](#Step-4-2-Share-Package)
    -   [<span data-ttu-id="5ab6f-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="5ab6f-113">4.3 Next steps</span></span>](#Step-4-3-Next-Step)
-   [<span data-ttu-id="5ab6f-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="5ab6f-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="5ab6f-115">介绍</span><span class="sxs-lookup"><span data-stu-id="5ab6f-115">Introduction</span></span>

<span data-ttu-id="5ab6f-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-116">**About this document**</span></span>

<span data-ttu-id="5ab6f-117">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT Edge 的硬件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT Edge enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="5ab6f-118">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-118">This multi-step process includes:</span></span>

-   <span data-ttu-id="5ab6f-119">配置 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="5ab6f-119">Configuring Azure IoT Edge</span></span>
-   <span data-ttu-id="5ab6f-120">注册 IoT Edge 设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-120">Registering your IoT Edge device</span></span>
-   <span data-ttu-id="5ab6f-121">在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="5ab6f-121">Manual Test for Azure IoT Edge on device</span></span>
-   <span data-ttu-id="5ab6f-122">打包并共享文件和设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-122">Packaging and sharing the files and device</span></span>

<span data-ttu-id="5ab6f-123">**准备工作：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-123">**Prepare:**</span></span>

<span data-ttu-id="5ab6f-124">在执行以下任何步骤之前，请仔细阅读每个步骤，确保对整个过程有全面的了解。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-124">Before executing any of the steps below, read through each steps to ensure end to end understanding.</span></span>

<span data-ttu-id="5ab6f-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="5ab6f-126">一台装有 GitHub 的计算机，并且能够访问 [azure-iot-sdk](https://github.com/Azure/azure-iot-sdks) GitHub 公共存储库。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-126">Computer with GitHub installed and access to the [azure-iot-sdk](https://github.com/Azure/azure-iot-sdks) GitHub public repository.</span></span>
-   <span data-ttu-id="5ab6f-127">用于访问命令行的 SSH 客户端，例如 [PuTTY](https://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-127">SSH client, such as [PuTTY](https://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="5ab6f-128">需要认证的硬件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-128">Required hardware to certify.</span></span>

<span data-ttu-id="5ab6f-129">注意：如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](https://catalog.azureiotsolutions.com/)请求此身份，然后遵照本文中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-129">Note: If you haven't contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](https://catalog.azureiotsolutions.com/) first to request it and then follow these instructions.</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="5ab6f-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="5ab6f-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="5ab6f-131">遵照[此处](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux)所述的说明[注册](https://account.windowsazure.com/signup?offer=ms-azr-0044p) Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-131">[Sign up](https://account.windowsazure.com/signup?offer=ms-azr-0044p) to the Azure IoT Hub service and follow the instructions mentioned [here](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux).</span></span> <span data-ttu-id="5ab6f-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="5ab6f-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-133">**IoT Hub Connection String**: An example of IoT hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="5ab6f-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-134">Step 2: Register Device</span></span>

<span data-ttu-id="5ab6f-135">在本部分，我们将使用 DeviceExplorer 注册 Edge 设备。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-135">In this section, you will register your Edge device using DeviceExplorer.</span></span> <span data-ttu-id="5ab6f-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="5ab6f-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="5ab6f-137">Device management</span></span>
    -   <span data-ttu-id="5ab6f-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-138">Create new devices</span></span>
    -   <span data-ttu-id="5ab6f-139">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="5ab6f-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="5ab6f-140">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="5ab6f-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="5ab6f-141">提供删除设备的功能</span><span class="sxs-lookup"><span data-stu-id="5ab6f-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="5ab6f-142">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="5ab6f-142">Monitoring events from your device</span></span>
-   <span data-ttu-id="5ab6f-143">将消息发送到设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-143">Sending messages to your device</span></span>

<span data-ttu-id="5ab6f-144">若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step-1-Configure) 中所述的以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-144">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step-1-Configure):</span></span>

-   <span data-ttu-id="5ab6f-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="5ab6f-145">IoT Hub Connection String</span></span>

<span data-ttu-id="5ab6f-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-146">**Steps:**</span></span>
1.  <span data-ttu-id="5ab6f-147">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-147">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="5ab6f-148">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-148">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="5ab6f-149">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="5ab6f-150">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-150">a.</span></span> <span data-ttu-id="5ab6f-151">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-151">Click the **Management** tab.</span></span>

    <span data-ttu-id="5ab6f-152">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-152">b.</span></span> <span data-ttu-id="5ab6f-153">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-153">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="5ab6f-154">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="5ab6f-155">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-155">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="5ab6f-156">c.</span><span class="sxs-lookup"><span data-stu-id="5ab6f-156">c.</span></span> <span data-ttu-id="5ab6f-157">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-157">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="5ab6f-158">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-158">d.</span></span> <span data-ttu-id="5ab6f-159">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-159">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="5ab6f-160">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-160">e.</span></span> <span data-ttu-id="5ab6f-161">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="5ab6f-162">f.</span><span class="sxs-lookup"><span data-stu-id="5ab6f-162">f.</span></span> <span data-ttu-id="5ab6f-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-163">Save this information in Notepad.</span></span> <span data-ttu-id="5ab6f-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-164">You will need this information in later steps.</span></span>

<span data-ttu-id="5ab6f-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="5ab6f-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="5ab6f-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step-3-Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a><span data-ttu-id="5ab6f-167">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="5ab6f-167">Step 3: Manual Test for Azure IoT Edge on device</span></span>

<span data-ttu-id="5ab6f-168">本部分将引导你在运行 Linux 操作系统的 Edge 设备上执行测试，使该设备符合 Azure IoT Edge 认证的要求</span><span class="sxs-lookup"><span data-stu-id="5ab6f-168">This section walks you through the test to be performed on the Edge devices running the Linux operating system such  that it can qualify for Azure IoT Edge certification</span></span> 

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a><span data-ttu-id="5ab6f-169">3.1：Edge RuntimeEnabled（必需）</span><span class="sxs-lookup"><span data-stu-id="5ab6f-169">3.1 Edge RuntimeEnabled (Mandatory)</span></span>
<span data-ttu-id="5ab6f-170">级别总数：1</span><span class="sxs-lookup"><span data-stu-id="5ab6f-170">*Total number of Level : 1*</span></span>

<span data-ttu-id="5ab6f-171">**说明：** 包含 Azure IoT Edge 运行时和依赖项的设备。从[此链接](https://aka.ms/iotedgeruntime)下载 Azure IoT Edge 运行时</span><span class="sxs-lookup"><span data-stu-id="5ab6f-171">**Description:** A device which includes the Azure IoT Edge runtime and dependencies.Download the Azure IoT Edge Runtime from the [link](https://aka.ms/iotedgeruntime)</span></span>

<span data-ttu-id="5ab6f-172">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-172">**Details of the requirement:**</span></span>

<span data-ttu-id="5ab6f-173">预装以下组件，或者由分销点在设备上为客户安装这些组件：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-173">The following components come pre-installed or at the point of distribution on the device to customer(s):</span></span>

-   <span data-ttu-id="5ab6f-174">Azure IoT Edge 安全守护程序</span><span class="sxs-lookup"><span data-stu-id="5ab6f-174">Azure IoT Edge Security Daemon</span></span>
-   <span data-ttu-id="5ab6f-175">守护程序配置文件</span><span class="sxs-lookup"><span data-stu-id="5ab6f-175">Daemon configuration file</span></span>
-   <span data-ttu-id="5ab6f-176">Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="5ab6f-176">Moby container management system</span></span>
-   <span data-ttu-id="5ab6f-177">版本 `hsmlib`</span><span class="sxs-lookup"><span data-stu-id="5ab6f-177">A version of `hsmlib`</span></span> 

<span data-ttu-id="5ab6f-178">在通过 DPS 集成启动时，或者当用户在 **config** 文件中输入设备凭据后，IoT Edge 运行时将正常运行。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-178">The IoT Edge runtime becomes functional at boot via DPS integration or by the user entering device credentials into the **config** file.</span></span>

<span data-ttu-id="5ab6f-179">**测试步骤：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-179">**Test steps:**</span></span>

-   <span data-ttu-id="5ab6f-180">公司必须将 Edge 设备寄送到 Microsoft 进行额外的验证。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-180">Company must send the edge device to Microsoft for additional validation.</span></span> <span data-ttu-id="5ab6f-181">当公司提交设备进行 Azure IoT Edge 认证时，我们会发送详细说明和我们所需的信息。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-181">We will send detail instructions and information we need when the company submit the device for Azure IoT edge certification.</span></span>
-   <span data-ttu-id="5ab6f-182">公司需确保 Edge 设备上同时预装了 Azure IoT Edge 安全守护程序和 Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="5ab6f-182">Company needs to ensure sure that the edge device comes both Azure IoT Edge Security daemon and Moby container management system pre-installed</span></span>
    -   <span data-ttu-id="5ab6f-183">Microsoft 会检查 Edge 设备上是否附带 Azure IoT Edge 安全守护程序</span><span class="sxs-lookup"><span data-stu-id="5ab6f-183">Microsoft will check that the edge device comes with Azure IoT Edge Security Daemon</span></span>
    -   <span data-ttu-id="5ab6f-184">Microsoft 会检查 Edge 设备上是否附带 Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="5ab6f-184">Microsoft will check that the edge device comes with Moby container management system</span></span>
-   <span data-ttu-id="5ab6f-185">公司需向 Microsoft 提供有关如何通过电子邮件连接到 IoT 中心的说明</span><span class="sxs-lookup"><span data-stu-id="5ab6f-185">Company needs to provide Microsoft the instruction on how to connect to IoT Hub via email</span></span>
    -   <span data-ttu-id="5ab6f-186">用于连接的配置文件</span><span class="sxs-lookup"><span data-stu-id="5ab6f-186">Config file to connect</span></span>
    -   <span data-ttu-id="5ab6f-187">设备的预配方式</span><span class="sxs-lookup"><span data-stu-id="5ab6f-187">How the device is provisioned</span></span>
    -   <span data-ttu-id="5ab6f-188">其他重要信息</span><span class="sxs-lookup"><span data-stu-id="5ab6f-188">Other important information</span></span> 
-   <span data-ttu-id="5ab6f-189">请等待一段时间，让 Microsoft 处理和完成认证过程。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-189">Please allow some time to process and complete the certification process.</span></span> <span data-ttu-id="5ab6f-190">审批后，Microsoft 会寄回 Edge 设备。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-190">Microsoft will ship back the edge device upon approval.</span></span>

<a name="Step-3-2-DeviceManagement"></a>
## <a name="32-device-management-mandatory"></a><span data-ttu-id="5ab6f-191">3.2：设备管理（必需）</span><span class="sxs-lookup"><span data-stu-id="5ab6f-191">3.2 Device Management (Mandatory)</span></span>
<span data-ttu-id="5ab6f-192">级别总数：1</span><span class="sxs-lookup"><span data-stu-id="5ab6f-192">*Total number of Level : 1*</span></span> 

<span data-ttu-id="5ab6f-193">**先决条件：** 设备连接。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-193">**Pre-requisites:** Device Connectivity.</span></span>

<span data-ttu-id="5ab6f-194">**说明：** 可以执行由 IoT 中心发出的消息触发的基本设备管理操作的设备。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-194">**Description:** A device that can perform basic device management operations triggered by messages from IoT Hub.</span></span>

<span data-ttu-id="5ab6f-195">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-195">**Details of the requirement:**</span></span>

<span data-ttu-id="5ab6f-196">设备中必须配备具有以下功能的组件：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-196">The device must have components that are capable of the following:</span></span>

1.  <span data-ttu-id="5ab6f-197">支持使用设备孪生来触发固件或操作系统更新，以及报告状态（包括错误消息或详细信息）</span><span class="sxs-lookup"><span data-stu-id="5ab6f-197">Supports the use of device twins to trigger a firmware or operating system update and to report status including error messages or details</span></span>
2.  <span data-ttu-id="5ab6f-198">支持使用直接方法来触发重新启动，并使用设备孪生来报告上次启动时间。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-198">Supports the use of direct methods to trigger a reboot and uses device twin to report last boot time.</span></span>

<span data-ttu-id="5ab6f-199">组件可以预装，或者在分销点为客户安装。以下手动测试适用于支持通过包管理器（例如 dpkg 或 apt）完成更新，或者以原子映像形式完成更新的 Linux 分发版。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-199">The component may come pre-installed or at the point of distribution to the customer.The following Manual test applies to Linux distributions that support updates either through package managers like dpkg or apt, or by updating as an atomic image.</span></span>

<span data-ttu-id="5ab6f-200">**手动测试 1：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-200">**Manual test 1:**</span></span> 

1.  <span data-ttu-id="5ab6f-201">如果该组件是在设备分销点安装的，请将有关安装组件的分步说明放入 readme.md 文件，并将其随附在提交内容中</span><span class="sxs-lookup"><span data-stu-id="5ab6f-201">If the component comes at the point of distribution of the device, put the step-by-step instructions for installing the components into a readme.md file and include with your submission</span></span>
2.  <span data-ttu-id="5ab6f-202">将设备连接到 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="5ab6f-202">Connect the device to Azure IoT Hub</span></span>
3.  <span data-ttu-id="5ab6f-203">使用 Windows 10 问题步骤记录器（或类似的程序）捕获以下步骤</span><span class="sxs-lookup"><span data-stu-id="5ab6f-203">Use Windows 10 Problem Steps Recorder (or equivalent) to capture the following steps</span></span>

    <span data-ttu-id="5ab6f-204">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-204">a.</span></span> <span data-ttu-id="5ab6f-205">使用 Azure 门户设置设备孪生所需属性，以便启动设备来安装新的更新。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-205">Using the Azure Portal, set the device twin desired properties that will initiate the device to install new updates.</span></span>

    <span data-ttu-id="5ab6f-206">**注意：** 可以编程方式执行此步骤，而不使用门户（如果有此偏好）。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-206">**Note:** You may perform this step pro-grammatically instead of using the portal, if preferred.</span></span>

    <span data-ttu-id="5ab6f-207">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-207">b.</span></span> <span data-ttu-id="5ab6f-208">允许设备更新并通过设备孪生报告属性来报告状态。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-208">Allow the device to update and report status through the device twin reported properties.</span></span>

    <span data-ttu-id="5ab6f-209">c.</span><span class="sxs-lookup"><span data-stu-id="5ab6f-209">c.</span></span> <span data-ttu-id="5ab6f-210">捕获有关每项状态更改的整个设备孪生 JSON 内容。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-210">Capture entire device twin JSON content for each state change.</span></span>
4.  <span data-ttu-id="5ab6f-211">在提交内容中包含通过问题步骤记录器保存的 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-211">Include the .zip file saved from the Problem Steps Recorder as part of your submission.</span></span>

<span data-ttu-id="5ab6f-212">**手动测试 2：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-212">**Manual test 2:**</span></span>

1.  <span data-ttu-id="5ab6f-213">如果该组件是在设备分销点安装的，请将有关安装组件的分步说明放入 readme.md 文件，并将其随附在提交内容中</span><span class="sxs-lookup"><span data-stu-id="5ab6f-213">If the component comes at the point of distribution of the device, put the step-by-step instructions for installing the components into a readme.md file and include with your submission</span></span>
2.  <span data-ttu-id="5ab6f-214">将设备连接到 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="5ab6f-214">Connect the device to Azure IoT Hub</span></span>
3.  <span data-ttu-id="5ab6f-215">使用 Windows 10 问题步骤记录器（或类似的程序）捕获以下步骤</span><span class="sxs-lookup"><span data-stu-id="5ab6f-215">Use Windows 10 Problem Steps Recorder (or equivalent) to capture the following steps</span></span>

    <span data-ttu-id="5ab6f-216">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-216">a.</span></span> <span data-ttu-id="5ab6f-217">使用 Azure 门户向设备发送一个直接方法。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-217">Using the Azure Portal, send a direct method to the device.</span></span> <span data-ttu-id="5ab6f-218">在 .txt 文件中捕获直接方法名称、有效负载和结果。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-218">Capture the direct method name, payload, and result into a .txt file.</span></span>

    <span data-ttu-id="5ab6f-219">**注意：** 可以编程方式执行此步骤，而不使用门户（如果有此偏好）。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-219">**Note:** You may perform this step pro-grammatically instead of using the portal, if preferred.</span></span>

    <span data-ttu-id="5ab6f-220">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-220">b.</span></span>  <span data-ttu-id="5ab6f-221">捕获整个设备孪生 JSON 内容。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-221">Capture the entire device twin JSON content.</span></span> <span data-ttu-id="5ab6f-222">它应该包括一个显示上次重新启动时间的报告属性。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-222">It should include a reported property that shows the last reboot time.</span></span>
4.  <span data-ttu-id="5ab6f-223">在提交内容中包含通过问题步骤记录器保存的 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-223">Include the .zip file saved from the Problem Steps Recorder as part of your submission.</span></span>

<a name="Step-3-3-Security"></a>
## <a name="33-security-optional"></a><span data-ttu-id="5ab6f-224">3.3：安全性（可选）</span><span class="sxs-lookup"><span data-stu-id="5ab6f-224">3.3 Security (Optional)</span></span>
<span data-ttu-id="5ab6f-225">级别总数：4</span><span class="sxs-lookup"><span data-stu-id="5ab6f-225">Total number of Levels: 4</span></span>

 <span data-ttu-id="5ab6f-226">**注意：** Microsoft 正在致力于定义安全要求方面的验证过程，包括审查第三方验证实验室的使用。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-226">**Note:** Microsoft is working on to define validation process for security requirement including exploration of leveraging 3rd party validation labs.</span></span> 
 
#### <a name="331-device-securitylevel1"></a><span data-ttu-id="5ab6f-227">3.3.1：Device Security.Level1</span><span class="sxs-lookup"><span data-stu-id="5ab6f-227">3.3.1 Device Security.Level1</span></span> 

<span data-ttu-id="5ab6f-228">**说明：** 如果设备使用安全协议的自定义实现，而不是使用 Azure IoT 设备 SDK，则设备将认证为“级别 1”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-228">**Description:** Device is certified as Level 1 , if device has custom implementation of security protocols other than use of Azure IoT Device SDK.</span></span> 

<span data-ttu-id="5ab6f-229">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-229">**Details of the requirement:**</span></span>

-   <span data-ttu-id="5ab6f-230">最低安全级别</span><span class="sxs-lookup"><span data-stu-id="5ab6f-230">Minimum security level</span></span> 
-   <span data-ttu-id="5ab6f-231">不使用 Azure IoT 设备 SDK 的 IoT Edge 设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-231">IoT Edge devices without usage of Azure IoT Device SDK</span></span> 
-   <span data-ttu-id="5ab6f-232">此项要求没有测试步骤。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-232">There is no test step for this requirement.</span></span> <span data-ttu-id="5ab6f-233">如果安装了 Edge 运行时并且与 IoT 中心建立了连接，则设备自动符合此级别</span><span class="sxs-lookup"><span data-stu-id="5ab6f-233">Edge Runtime and connectivity to IoT Hub automatically make devices  eligible for this level</span></span> 
 
#### <a name="332-device-securitylevel2"></a><span data-ttu-id="5ab6f-234">3.3.2：Device Security.Level2</span><span class="sxs-lookup"><span data-stu-id="5ab6f-234">3.3.2 Device Security.Level2</span></span> 

<span data-ttu-id="5ab6f-235">**说明：** 如果设备可以使用 Azure IoT 设备 SDK 实现设备安全协议，则设备将认证为“级别 2”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-235">**Description:** Device is certified as Level 2 , if device can use Azure IoT Device SDKs to implement device security protocols.</span></span> 

<span data-ttu-id="5ab6f-236">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-236">**Details of the requirement:**</span></span>

-   <span data-ttu-id="5ab6f-237">验证 Azure IoT 设备 SDK 的使用情况</span><span class="sxs-lookup"><span data-stu-id="5ab6f-237">Validates the usage of Azure IoT Device SDK</span></span> 
 
#### <a name="333-device-securitylevel-3"></a><span data-ttu-id="5ab6f-238">3.3.3：Device Security.Level 3</span><span class="sxs-lookup"><span data-stu-id="5ab6f-238">3.3.3 Device Security.Level 3</span></span> 

<span data-ttu-id="5ab6f-239">**说明：** 如果设备使用硬件安全模块来增强安全性，则设备将认证为“级别 3”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-239">**Description:** Device is certified as Level 3 , if device use hardware secure modules for security hardening.</span></span>  <span data-ttu-id="5ab6f-240">这种验证是通过安全认证完成的。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-240">Its validated through security certifications.</span></span>
 
<span data-ttu-id="5ab6f-241">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="5ab6f-241">**Details of the requirement:**</span></span>

<span data-ttu-id="5ab6f-242">此级别需要满足以下“安全性”认证要求：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-242">This level require below Security certification requirement :</span></span> 

-    <span data-ttu-id="5ab6f-243">FIPS 140-2 级别 2 或更高</span><span class="sxs-lookup"><span data-stu-id="5ab6f-243">FIPS 140-2 Level 2 or higher</span></span> 
-    <span data-ttu-id="5ab6f-244">通用准则 EAL 3+</span><span class="sxs-lookup"><span data-stu-id="5ab6f-244">Common Criteria EAL 3+</span></span> 
 
#### <a name="334-device-securitylevel-4"></a><span data-ttu-id="5ab6f-245">3.3.4：Device Security.Level 4</span><span class="sxs-lookup"><span data-stu-id="5ab6f-245">3.3.4 Device Security.Level 4</span></span> 

<span data-ttu-id="5ab6f-246">**说明：** 如果设备使用硬件安全模块来增强安全性，则设备将认证为“级别 4”。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-246">**Description:** Device is certified as Level 4 , if device use hardware secure modules for security hardening.</span></span>  <span data-ttu-id="5ab6f-247">这种验证是通过安全认证完成的。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-247">Its validated through security certifications.</span></span>
 
<span data-ttu-id="5ab6f-248">**要求详细信息：** 此级别需要满足以下“安全性”认证要求：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-248">**Details of the requirement:** This level require below Security certification requirement :</span></span>

-   <span data-ttu-id="5ab6f-249">FIPS 140-2 级别 3 或更高</span><span class="sxs-lookup"><span data-stu-id="5ab6f-249">FIPS 140-2 Level 3 or higher</span></span> 
-   <span data-ttu-id="5ab6f-250">通用准则 EAL 4+</span><span class="sxs-lookup"><span data-stu-id="5ab6f-250">Common Criteria EAL 4+</span></span> 
    
<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="5ab6f-251">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="5ab6f-251">Step 4: Package and Share</span></span>
<a name="Step-4-1-Package-build"></a>
## <a name="41-package-build-logs-and-device-in-original-box"></a><span data-ttu-id="5ab6f-252">4.1：在原始包装中打包生成日志和设备</span><span class="sxs-lookup"><span data-stu-id="5ab6f-252">4.1 Package build logs and Device in original box</span></span> 
<span data-ttu-id="5ab6f-253">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="5ab6f-253">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="5ab6f-254">“设备管理手动测试”中所述的、由问题步骤记录器记录的 Zip 文件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-254">Zip files recorded by Problem Steps recorder as stated in Device Management manual tests.</span></span>
2.  <span data-ttu-id="5ab6f-255">手动测试 2 中所述的文本文件</span><span class="sxs-lookup"><span data-stu-id="5ab6f-255">Text file as stated in manual test 2</span></span> 
3.  <span data-ttu-id="5ab6f-256">装有 IoT Azure 运行时，并已寄送到 Microsoft 做进一步验证的设备。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-256">Device with IoT Azure Runtime installed and shipped to Microsoft for further validation.</span></span>

<a name="Step-4-2-Share-Package"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a><span data-ttu-id="5ab6f-257">4.2：与 Microsoft Azure IoT 团队成员共享包</span><span class="sxs-lookup"><span data-stu-id="5ab6f-257">4.2 Share package with Microsoft Azure IoT team</span></span>

1.  <span data-ttu-id="5ab6f-258">转到[合作伙伴仪表板](https://catalog.azureiotsolutions.com/devices)</span><span class="sxs-lookup"><span data-stu-id="5ab6f-258">Go to [Partner Dashboard](https://catalog.azureiotsolutions.com/devices)</span></span>
2.  <span data-ttu-id="5ab6f-259">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-259">Click on Upload icon at top-right corner of device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="5ab6f-261">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-261">This will open an upload dialog.</span></span> <span data-ttu-id="5ab6f-262">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-262">Browse your file(s) by clicking Upload button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="5ab6f-264">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-264">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="5ab6f-265">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-265">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="5ab6f-266">***注意：*** 提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-266">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>

<a name="Step-4-3-Next-Step"></a>
## <a name="43-next-steps"></a><span data-ttu-id="5ab6f-267">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="5ab6f-267">4.3 Next steps</span></span>

<span data-ttu-id="5ab6f-268">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-268">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="5ab6f-269">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="5ab6f-269">Step 5: Troubleshooting</span></span>

<span data-ttu-id="5ab6f-270">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="5ab6f-270">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
