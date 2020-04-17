<a name="how-to-certify-iot-edge-devices-running-linux"></a><span data-ttu-id="a21f5-101">如何认证运行 Linux 的 IoT Edge 设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-101">How to certify IoT Edge devices running Linux</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="a21f5-102">目录</span><span class="sxs-lookup"><span data-stu-id="a21f5-102">Table of Contents</span></span>

-   [<span data-ttu-id="a21f5-103">介绍</span><span class="sxs-lookup"><span data-stu-id="a21f5-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="a21f5-104">步骤 1：配置 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="a21f5-104">Step 1: Configure Azure IoT Edge</span></span>](#Step-1-Configure)
-   [<span data-ttu-id="a21f5-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-105">Step 2: Register Device</span></span>](#Step-2-Register)
-   [<span data-ttu-id="a21f5-106">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="a21f5-106">Step 3: Manual Test for Azure IoT Edge on device</span></span>](#Step-3-Manual)
    -   [<span data-ttu-id="a21f5-107">3.1：IoT Edge 运行时</span><span class="sxs-lookup"><span data-stu-id="a21f5-107">3.1 IoT Edge Runtime</span></span>](#Step-3-1-IoTEdgeRunTime)
    -   [<span data-ttu-id="a21f5-108">3.2：设备管理</span><span class="sxs-lookup"><span data-stu-id="a21f5-108">3.2 Device Management</span></span>](#Step-3-2-DeviceManagement)
    -   [<span data-ttu-id="a21f5-109">3.3：安全性</span><span class="sxs-lookup"><span data-stu-id="a21f5-109">3.3 Security </span></span>](#Step-3-3-Security)
-   [<span data-ttu-id="a21f5-110">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="a21f5-110">Step 4: Package and Share</span></span>](#Step-4-Package_Share)
    -   [<span data-ttu-id="a21f5-111">4.1：在原始包装中打包生成日志和设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-111">4.1 Package build logs and Device in original box</span></span>](#Step-4-1-Package-build)
    -   [<span data-ttu-id="a21f5-112">4.2：与 Microsoft Azure IoT 团队成员共享包</span><span class="sxs-lookup"><span data-stu-id="a21f5-112">4.2 Share package with Microsoft Azure IoT team</span></span>](#Step-4-2-Share-Package)
    -   [<span data-ttu-id="a21f5-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="a21f5-113">4.3 Next steps</span></span>](#Step-4-3-Next-Step)
-   [<span data-ttu-id="a21f5-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="a21f5-114">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="a21f5-115">介绍</span><span class="sxs-lookup"><span data-stu-id="a21f5-115">Introduction</span></span>

<span data-ttu-id="a21f5-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="a21f5-116">**About this document**</span></span>

<span data-ttu-id="a21f5-117">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT Edge 的硬件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT Edge enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="a21f5-118">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="a21f5-118">This multi-step process includes:</span></span>

-   <span data-ttu-id="a21f5-119">配置 Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="a21f5-119">Configuring Azure IoT Edge</span></span>
-   <span data-ttu-id="a21f5-120">注册 IoT Edge 设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-120">Registering your IoT Edge device</span></span>
-   <span data-ttu-id="a21f5-121">在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="a21f5-121">Manual Test for Azure IoT Edge on device</span></span>
-   <span data-ttu-id="a21f5-122">打包并共享文件和设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-122">Packaging and sharing the files and device</span></span>

<span data-ttu-id="a21f5-123">**准备工作：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-123">**Prepare:**</span></span>

<span data-ttu-id="a21f5-124">在执行以下任何步骤之前，请仔细阅读每个步骤，确保对整个过程有全面的了解。</span><span class="sxs-lookup"><span data-stu-id="a21f5-124">Before executing any of the steps below, read through each steps to ensure end to end understanding.</span></span>

<span data-ttu-id="a21f5-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="a21f5-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="a21f5-126">一台装有 GitHub 的计算机，并且能够访问 [azure-iot-sdk](https://github.com/Azure/azure-iot-sdks) GitHub 公共存储库。</span><span class="sxs-lookup"><span data-stu-id="a21f5-126">Computer with GitHub installed and access to the [azure-iot-sdk](https://github.com/Azure/azure-iot-sdks) GitHub public repository.</span></span>
-   <span data-ttu-id="a21f5-127">用于访问命令行的 SSH 客户端，例如 [PuTTY](https://www.putty.org/)。</span><span class="sxs-lookup"><span data-stu-id="a21f5-127">SSH client, such as [PuTTY](https://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="a21f5-128">需要认证的硬件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-128">Required hardware to certify.</span></span>

<span data-ttu-id="a21f5-129">注意：如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](https://catalog.azureiotsolutions.com/)请求此身份，然后遵照本文中的说明操作。</span><span class="sxs-lookup"><span data-stu-id="a21f5-129">Note: If you haven't contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](https://catalog.azureiotsolutions.com/) first to request it and then follow these instructions.</span></span>

<a name="Step-1-Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="a21f5-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="a21f5-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="a21f5-131">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明[注册](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux) Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="a21f5-131">[Sign up](https://account.windowsazure.com/signup?offer=ms-azr-0044p) to the Azure IoT Hub service and follow the instructions mentioned [here](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux).</span></span> <span data-ttu-id="a21f5-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="a21f5-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="a21f5-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="a21f5-133">**IoT Hub Connection String**: An example of IoT hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step-2-Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="a21f5-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-134">Step 2: Register Device</span></span>

<span data-ttu-id="a21f5-135">在本部分，我们将使用 DeviceExplorer 注册 Edge 设备。</span><span class="sxs-lookup"><span data-stu-id="a21f5-135">In this section, you will register your Edge device using DeviceExplorer.</span></span> <span data-ttu-id="a21f5-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="a21f5-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="a21f5-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="a21f5-137">Device management</span></span>
    -   <span data-ttu-id="a21f5-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-138">Create new devices</span></span>
    -   <span data-ttu-id="a21f5-139">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="a21f5-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="a21f5-140">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="a21f5-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="a21f5-141">提供删除设备的功能</span><span class="sxs-lookup"><span data-stu-id="a21f5-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="a21f5-142">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="a21f5-142">Monitoring events from your device</span></span>
-   <span data-ttu-id="a21f5-143">将消息发送到设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-143">Sending messages to your device</span></span>

<span data-ttu-id="a21f5-144">若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step-1-Configure) 中所述的以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="a21f5-144">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step-1-Configure):</span></span>

-   <span data-ttu-id="a21f5-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="a21f5-145">IoT Hub Connection String</span></span>

<span data-ttu-id="a21f5-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-146">**Steps:**</span></span>
1.  <span data-ttu-id="a21f5-147">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="a21f5-147">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="a21f5-148">在“配置”选项卡下添加连接信息，并单击“更新”按钮。 </span><span class="sxs-lookup"><span data-stu-id="a21f5-148">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="a21f5-149">使用以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="a21f5-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="a21f5-150">a.</span><span class="sxs-lookup"><span data-stu-id="a21f5-150">a.</span></span> <span data-ttu-id="a21f5-151">单击“管理”选项卡。 </span><span class="sxs-lookup"><span data-stu-id="a21f5-151">Click the **Management** tab.</span></span>

    <span data-ttu-id="a21f5-152">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-152">b.</span></span> <span data-ttu-id="a21f5-153">列表中会显示已注册的设备。</span><span class="sxs-lookup"><span data-stu-id="a21f5-153">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="a21f5-154">如果该设备未显示在列表中，请单击“刷新”按钮。 </span><span class="sxs-lookup"><span data-stu-id="a21f5-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="a21f5-155">如果这是第一次执行此操作，则不应检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="a21f5-155">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="a21f5-156">c.</span><span class="sxs-lookup"><span data-stu-id="a21f5-156">c.</span></span> <span data-ttu-id="a21f5-157">单击“创建”按钮创建设备 ID 和密钥。 </span><span class="sxs-lookup"><span data-stu-id="a21f5-157">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="a21f5-158">d.</span><span class="sxs-lookup"><span data-stu-id="a21f5-158">d.</span></span> <span data-ttu-id="a21f5-159">成功创建后，设备会列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="a21f5-159">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="a21f5-160">e.</span><span class="sxs-lookup"><span data-stu-id="a21f5-160">e.</span></span> <span data-ttu-id="a21f5-161">右键单击该设备，并从上下文菜单中选择“复制所选设备的连接字符串”。 </span><span class="sxs-lookup"><span data-stu-id="a21f5-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="a21f5-162">f.</span><span class="sxs-lookup"><span data-stu-id="a21f5-162">f.</span></span> <span data-ttu-id="a21f5-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="a21f5-163">Save this information in Notepad.</span></span> <span data-ttu-id="a21f5-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="a21f5-164">You will need this information in later steps.</span></span>

<span data-ttu-id="a21f5-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="a21f5-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="a21f5-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="a21f5-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step-3-Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a><span data-ttu-id="a21f5-167">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="a21f5-167">Step 3: Manual Test for Azure IoT Edge on device</span></span>

<span data-ttu-id="a21f5-168">本部分将引导你在运行 Linux 操作系统的 Edge 设备上执行测试，使该设备符合 Azure IoT Edge 认证的要求</span><span class="sxs-lookup"><span data-stu-id="a21f5-168">This section walks you through the test to be performed on the Edge devices running the Linux operating system such  that it can qualify for Azure IoT Edge certification</span></span> 

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a><span data-ttu-id="a21f5-169">3.1：Edge RuntimeEnabled（必需）</span><span class="sxs-lookup"><span data-stu-id="a21f5-169">3.1 Edge RuntimeEnabled (Mandatory)</span></span>
<span data-ttu-id="a21f5-170">级别总数：1 </span><span class="sxs-lookup"><span data-stu-id="a21f5-170">*Total number of Level : 1*</span></span>

<span data-ttu-id="a21f5-171">**说明：** 一个包含 Azure IoT Edge 运行时和依赖项的设备。请从以下途径下载 Azure IoT Edge 运行时：</span><span class="sxs-lookup"><span data-stu-id="a21f5-171">**Description:** A device which includes the Azure IoT Edge runtime and dependencies.Download the Azure IoT Edge Runtime from the following path:</span></span>

<span data-ttu-id="a21f5-172">对于 Linux (ARM32V7/armhf)，请从该[链接](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-edge-linux-arm.md)安装运行时。</span><span class="sxs-lookup"><span data-stu-id="a21f5-172">For Linux (ARM32V7/armhf), install runtime from the [link](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-edge-linux-arm.md).</span></span>

<span data-ttu-id="a21f5-173">对于 Linux x64 (Intel/AMD)，请从该[链接](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-edge-linux.md)安装运行时。</span><span class="sxs-lookup"><span data-stu-id="a21f5-173">For Linux x64 (Intel/AMD), install runtime from the [link](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/iot-edge/how-to-install-iot-edge-linux.md).</span></span>

<span data-ttu-id="a21f5-174">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-174">**Details of the requirement:**</span></span>

<span data-ttu-id="a21f5-175">预装以下组件，或者由分销点在设备上为客户安装这些组件：</span><span class="sxs-lookup"><span data-stu-id="a21f5-175">The following components come pre-installed or at the point of distribution on the device to customer(s):</span></span>

-   <span data-ttu-id="a21f5-176">Azure IoT Edge 安全守护程序</span><span class="sxs-lookup"><span data-stu-id="a21f5-176">Azure IoT Edge Security Daemon</span></span>
-   <span data-ttu-id="a21f5-177">守护程序配置文件</span><span class="sxs-lookup"><span data-stu-id="a21f5-177">Daemon configuration file</span></span>
-   <span data-ttu-id="a21f5-178">Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="a21f5-178">Moby container management system</span></span>
-   <span data-ttu-id="a21f5-179">版本 `hsmlib`</span><span class="sxs-lookup"><span data-stu-id="a21f5-179">A version of `hsmlib`</span></span> 

<span data-ttu-id="a21f5-180">在通过 DPS 集成启动时，或者当用户在 **config** 文件中输入设备凭据后，IoT Edge 运行时将正常运行。</span><span class="sxs-lookup"><span data-stu-id="a21f5-180">The IoT Edge runtime becomes functional at boot via DPS integration or by the user entering device credentials into the **config** file.</span></span>

<span data-ttu-id="a21f5-181">**测试步骤：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-181">**Test steps:**</span></span>

-   <span data-ttu-id="a21f5-182">公司必须将 Edge 设备寄送到 Microsoft 进行额外的验证。</span><span class="sxs-lookup"><span data-stu-id="a21f5-182">Company must send the edge device to Microsoft for additional validation.</span></span> <span data-ttu-id="a21f5-183">当公司提交设备进行 Azure IoT Edge 认证时，我们会发送详细说明和我们所需的信息。</span><span class="sxs-lookup"><span data-stu-id="a21f5-183">We will send detail instructions and information we need when the company submit the device for Azure IoT edge certification.</span></span>
-   <span data-ttu-id="a21f5-184">公司需确保 Edge 设备上同时预装了 Azure IoT Edge 安全守护程序和 Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="a21f5-184">Company needs to ensure sure that the edge device comes both Azure IoT Edge Security daemon and Moby container management system pre-installed</span></span>
    -   <span data-ttu-id="a21f5-185">Microsoft 会检查 Edge 设备上是否附带 Azure IoT Edge 安全守护程序</span><span class="sxs-lookup"><span data-stu-id="a21f5-185">Microsoft will check that the edge device comes with Azure IoT Edge Security Daemon</span></span>
    -   <span data-ttu-id="a21f5-186">Microsoft 会检查 Edge 设备上是否附带 Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="a21f5-186">Microsoft will check that the edge device comes with Moby container management system</span></span>
-   <span data-ttu-id="a21f5-187">公司需向 Microsoft 提供有关如何通过电子邮件连接到 IoT 中心的说明</span><span class="sxs-lookup"><span data-stu-id="a21f5-187">Company needs to provide Microsoft the instruction on how to connect to IoT Hub via email</span></span>
    -   <span data-ttu-id="a21f5-188">用于连接的配置文件</span><span class="sxs-lookup"><span data-stu-id="a21f5-188">Config file to connect</span></span>
    -   <span data-ttu-id="a21f5-189">设备的预配方式</span><span class="sxs-lookup"><span data-stu-id="a21f5-189">How the device is provisioned</span></span>
    -   <span data-ttu-id="a21f5-190">其他重要信息</span><span class="sxs-lookup"><span data-stu-id="a21f5-190">Other important information</span></span> 
-   <span data-ttu-id="a21f5-191">请等待一段时间，让 Microsoft 处理和完成认证过程。</span><span class="sxs-lookup"><span data-stu-id="a21f5-191">Please allow some time to process and complete the certification process.</span></span> <span data-ttu-id="a21f5-192">审批后，Microsoft 会寄回 Edge 设备。</span><span class="sxs-lookup"><span data-stu-id="a21f5-192">Microsoft will ship back the edge device upon approval.</span></span>

<a name="Step-3-2-DeviceManagement"></a>
## <a name="32-device-management-optional"></a><span data-ttu-id="a21f5-193">3.2 设备管理（可选）</span><span class="sxs-lookup"><span data-stu-id="a21f5-193">3.2 Device Management (Optional)</span></span>
<span data-ttu-id="a21f5-194">级别总数：1 </span><span class="sxs-lookup"><span data-stu-id="a21f5-194">*Total number of Level : 1*</span></span> 

<span data-ttu-id="a21f5-195">**先决条件：** 设备连接。</span><span class="sxs-lookup"><span data-stu-id="a21f5-195">**Pre-requisites:** Device Connectivity.</span></span>

<span data-ttu-id="a21f5-196">**说明：** 可以执行由 IoT 中心发出的消息触发的基本设备管理操作的设备。</span><span class="sxs-lookup"><span data-stu-id="a21f5-196">**Description:** A device that can perform basic device management operations triggered by messages from IoT Hub.</span></span>

<span data-ttu-id="a21f5-197">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-197">**Details of the requirement:**</span></span>

<span data-ttu-id="a21f5-198">设备中必须配备具有以下功能的组件：</span><span class="sxs-lookup"><span data-stu-id="a21f5-198">The device must have components that are capable of the following:</span></span>

1.  <span data-ttu-id="a21f5-199">支持使用设备孪生来触发固件或操作系统更新，以及报告状态（包括错误消息或详细信息）</span><span class="sxs-lookup"><span data-stu-id="a21f5-199">Supports the use of device twins to trigger a firmware or operating system update and to report status including error messages or details</span></span>
2.  <span data-ttu-id="a21f5-200">支持使用直接方法来触发重新启动，并使用设备孪生来报告上次启动时间。</span><span class="sxs-lookup"><span data-stu-id="a21f5-200">Supports the use of direct methods to trigger a reboot and uses device twin to report last boot time.</span></span>

<span data-ttu-id="a21f5-201">组件可以预装，或者在分销点为客户安装。以下手动测试适用于支持通过包管理器（例如 dpkg 或 apt）完成更新，或者以原子映像形式完成更新的 Linux 分发版。</span><span class="sxs-lookup"><span data-stu-id="a21f5-201">The component may come pre-installed or at the point of distribution to the customer.The following Manual test applies to Linux distributions that support updates either through package managers like dpkg or apt, or by updating as an atomic image.</span></span>

<span data-ttu-id="a21f5-202">**手动测试 1：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-202">**Manual test 1:**</span></span> 

1.  <span data-ttu-id="a21f5-203">如果该组件是在设备分销点安装的，请将有关安装组件的分步说明放入 readme.md 文件，并将其随附在提交内容中。</span><span class="sxs-lookup"><span data-stu-id="a21f5-203">If the component comes at the point of distribution of the device, put the step-by-step instructions for installing the components into a readme.md file and include with your submission.</span></span> <span data-ttu-id="a21f5-204">如果使用的是 Microsoft SDK 示例，请使用此[链接](https://docs.microsoft.com/en-us/azure/iot-hub/tutorial-firmware-update#run-the-sample)</span><span class="sxs-lookup"><span data-stu-id="a21f5-204">If you are using Microsoft SDK samples please use the [link](https://docs.microsoft.com/en-us/azure/iot-hub/tutorial-firmware-update#run-the-sample)</span></span>
2.  <span data-ttu-id="a21f5-205">将设备连接到 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="a21f5-205">Connect the device to Azure IoT Hub</span></span>
3.  <span data-ttu-id="a21f5-206">使用 Windows 10 问题步骤记录器（或类似的程序）捕获以下步骤</span><span class="sxs-lookup"><span data-stu-id="a21f5-206">Use Windows 10 Problem Steps Recorder (or equivalent) to capture the following steps</span></span>

    <span data-ttu-id="a21f5-207">a.</span><span class="sxs-lookup"><span data-stu-id="a21f5-207">a.</span></span> <span data-ttu-id="a21f5-208">使用 Azure 门户设置设备孪生所需属性，以便启动设备来安装新的更新。</span><span class="sxs-lookup"><span data-stu-id="a21f5-208">Using the Azure Portal, set the device twin desired properties that will initiate the device to install new updates.</span></span>

    <span data-ttu-id="a21f5-209">**注意：** 可以编程方式执行此步骤，而不使用门户（如果有此偏好）。</span><span class="sxs-lookup"><span data-stu-id="a21f5-209">**Note:** You may perform this step pro-grammatically instead of using the portal, if preferred.</span></span>

    <span data-ttu-id="a21f5-210">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-210">b.</span></span> <span data-ttu-id="a21f5-211">允许设备更新并通过设备孪生报告属性来报告状态。</span><span class="sxs-lookup"><span data-stu-id="a21f5-211">Allow the device to update and report status through the device twin reported properties.</span></span>

    <span data-ttu-id="a21f5-212">c.</span><span class="sxs-lookup"><span data-stu-id="a21f5-212">c.</span></span> <span data-ttu-id="a21f5-213">捕获有关每项状态更改的整个设备孪生 JSON 内容。</span><span class="sxs-lookup"><span data-stu-id="a21f5-213">Capture entire device twin JSON content for each state change.</span></span>
4.  <span data-ttu-id="a21f5-214">在提交内容中包含通过问题步骤记录器保存的 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-214">Include the .zip file saved from the Problem Steps Recorder as part of your submission.</span></span>

<span data-ttu-id="a21f5-215">**手动测试 2：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-215">**Manual test 2:**</span></span>

1.  <span data-ttu-id="a21f5-216">如果该组件是在设备分销点安装的，请将有关安装组件的分步说明放入 readme.md 文件，并将其随附在提交内容中。</span><span class="sxs-lookup"><span data-stu-id="a21f5-216">If the component comes at the point of distribution of the device, put the step-by-step instructions for installing the components into a readme.md file and include with your submission.</span></span> <span data-ttu-id="a21f5-217">如果使用的是 Microsoft SDK 示例，请使用此[链接](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-node-node-device-management-get-started)</span><span class="sxs-lookup"><span data-stu-id="a21f5-217">If you are using Microsoft SDK samples please use the [link](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-node-node-device-management-get-started)</span></span>
2.  <span data-ttu-id="a21f5-218">将设备连接到 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="a21f5-218">Connect the device to Azure IoT Hub</span></span>
3.  <span data-ttu-id="a21f5-219">使用 Windows 10 问题步骤记录器（或类似的程序）捕获以下步骤</span><span class="sxs-lookup"><span data-stu-id="a21f5-219">Use Windows 10 Problem Steps Recorder (or equivalent) to capture the following steps</span></span>

    <span data-ttu-id="a21f5-220">a.</span><span class="sxs-lookup"><span data-stu-id="a21f5-220">a.</span></span> <span data-ttu-id="a21f5-221">使用 Azure 门户向设备发送一个直接方法。</span><span class="sxs-lookup"><span data-stu-id="a21f5-221">Using the Azure Portal, send a direct method to the device.</span></span> <span data-ttu-id="a21f5-222">在 .txt 文件中捕获直接方法名称、有效负载和结果。</span><span class="sxs-lookup"><span data-stu-id="a21f5-222">Capture the direct method name, payload, and result into a .txt file.</span></span>

    <span data-ttu-id="a21f5-223">**注意：** 可以编程方式执行此步骤，而不使用门户（如果有此偏好）。</span><span class="sxs-lookup"><span data-stu-id="a21f5-223">**Note:** You may perform this step pro-grammatically instead of using the portal, if preferred.</span></span>

    <span data-ttu-id="a21f5-224">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-224">b.</span></span>  <span data-ttu-id="a21f5-225">捕获整个设备孪生 JSON 内容。</span><span class="sxs-lookup"><span data-stu-id="a21f5-225">Capture the entire device twin JSON content.</span></span> <span data-ttu-id="a21f5-226">它应该包括一个显示上次重新启动时间的报告属性。</span><span class="sxs-lookup"><span data-stu-id="a21f5-226">It should include a reported property that shows the last reboot time.</span></span>
4.  <span data-ttu-id="a21f5-227">在提交内容中包含通过问题步骤记录器保存的 .zip 文件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-227">Include the .zip file saved from the Problem Steps Recorder as part of your submission.</span></span>

<a name="Step-3-3-Security"></a>
## <a name="33-security-optional"></a><span data-ttu-id="a21f5-228">3.3：安全性（可选）</span><span class="sxs-lookup"><span data-stu-id="a21f5-228">3.3 Security (Optional)</span></span>
<span data-ttu-id="a21f5-229">级别总数：4</span><span class="sxs-lookup"><span data-stu-id="a21f5-229">Total number of Levels: 4</span></span>

 <span data-ttu-id="a21f5-230">**注意：** Microsoft 正在致力于定义安全要求方面的验证过程，包括审查第三方验证实验室的使用。</span><span class="sxs-lookup"><span data-stu-id="a21f5-230">**Note:** Microsoft is working on to define validation process for security requirement including exploration of leveraging 3rd party validation labs.</span></span> 
 
#### <a name="331-device-securitylevel1"></a><span data-ttu-id="a21f5-231">3.3.1：Device Security.Level1</span><span class="sxs-lookup"><span data-stu-id="a21f5-231">3.3.1 Device Security.Level1</span></span> 

<span data-ttu-id="a21f5-232">**说明：** 如果设备使用安全协议的自定义实现，而不是使用 Azure IoT 设备 SDK，则设备将认证为“级别 1”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-232">**Description:** Device is certified as Level 1 , if device has custom implementation of security protocols other than use of Azure IoT Device SDK.</span></span> 

<span data-ttu-id="a21f5-233">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-233">**Details of the requirement:**</span></span>

-   <span data-ttu-id="a21f5-234">最低安全级别</span><span class="sxs-lookup"><span data-stu-id="a21f5-234">Minimum security level</span></span> 
-   <span data-ttu-id="a21f5-235">不使用 Azure IoT 设备 SDK 的 IoT Edge 设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-235">IoT Edge devices without usage of Azure IoT Device SDK</span></span> 
-   <span data-ttu-id="a21f5-236">此项要求没有测试步骤。</span><span class="sxs-lookup"><span data-stu-id="a21f5-236">There is no test step for this requirement.</span></span> <span data-ttu-id="a21f5-237">如果安装了 Edge 运行时并且与 IoT 中心建立了连接，则设备自动符合此级别</span><span class="sxs-lookup"><span data-stu-id="a21f5-237">Edge Runtime and connectivity to IoT Hub automatically make devices  eligible for this level</span></span> 
 
#### <a name="332-device-securitylevel2"></a><span data-ttu-id="a21f5-238">3.3.2：Device Security.Level2</span><span class="sxs-lookup"><span data-stu-id="a21f5-238">3.3.2 Device Security.Level2</span></span> 

<span data-ttu-id="a21f5-239">**说明：** 如果设备可以使用 Azure IoT 设备 SDK 实现设备安全协议，则设备将认证为“级别 2”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-239">**Description:** Device is certified as Level 2 , if device can use Azure IoT Device SDKs to implement device security protocols.</span></span> 

<span data-ttu-id="a21f5-240">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-240">**Details of the requirement:**</span></span>

-   <span data-ttu-id="a21f5-241">验证 Azure IoT 设备 SDK 的使用情况</span><span class="sxs-lookup"><span data-stu-id="a21f5-241">Validates the usage of Azure IoT Device SDK</span></span> 
 
#### <a name="333-device-securitylevel-3"></a><span data-ttu-id="a21f5-242">3.3.3：Device Security.Level 3</span><span class="sxs-lookup"><span data-stu-id="a21f5-242">3.3.3 Device Security.Level 3</span></span> 

<span data-ttu-id="a21f5-243">**说明：** 如果设备使用硬件安全模块来增强安全性，则设备将认证为“级别 3”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-243">**Description:** Device is certified as Level 3 , if device use hardware secure modules for security hardening.</span></span>  <span data-ttu-id="a21f5-244">这种验证是通过安全认证完成的。</span><span class="sxs-lookup"><span data-stu-id="a21f5-244">Its validated through security certifications.</span></span>
 
<span data-ttu-id="a21f5-245">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="a21f5-245">**Details of the requirement:**</span></span>

<span data-ttu-id="a21f5-246">此级别需要满足以下“安全性”认证要求：</span><span class="sxs-lookup"><span data-stu-id="a21f5-246">This level require below Security certification requirement :</span></span> 

-    <span data-ttu-id="a21f5-247">FIPS 140-2 级别 2 或更高</span><span class="sxs-lookup"><span data-stu-id="a21f5-247">FIPS 140-2 Level 2 or higher</span></span> 
-    <span data-ttu-id="a21f5-248">通用准则 EAL 3+</span><span class="sxs-lookup"><span data-stu-id="a21f5-248">Common Criteria EAL 3+</span></span> 
 
#### <a name="334-device-securitylevel-4"></a><span data-ttu-id="a21f5-249">3.3.4：Device Security.Level 4</span><span class="sxs-lookup"><span data-stu-id="a21f5-249">3.3.4 Device Security.Level 4</span></span> 

<span data-ttu-id="a21f5-250">**说明：** 如果设备使用硬件安全模块来增强安全性，则设备将认证为“级别 4”。</span><span class="sxs-lookup"><span data-stu-id="a21f5-250">**Description:** Device is certified as Level 4 , if device use hardware secure modules for security hardening.</span></span>  <span data-ttu-id="a21f5-251">这种验证是通过安全认证完成的。</span><span class="sxs-lookup"><span data-stu-id="a21f5-251">Its validated through security certifications.</span></span>
 
<span data-ttu-id="a21f5-252">**要求详细信息：** 此级别需要满足以下“安全性”认证要求：</span><span class="sxs-lookup"><span data-stu-id="a21f5-252">**Details of the requirement:** This level require below Security certification requirement :</span></span>

-   <span data-ttu-id="a21f5-253">FIPS 140-2 级别 3 或更高</span><span class="sxs-lookup"><span data-stu-id="a21f5-253">FIPS 140-2 Level 3 or higher</span></span> 
-   <span data-ttu-id="a21f5-254">通用准则 EAL 4+</span><span class="sxs-lookup"><span data-stu-id="a21f5-254">Common Criteria EAL 4+</span></span> 
    
<a name="Step-4-Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="a21f5-255">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="a21f5-255">Step 4: Package and Share</span></span>
<a name="Step-4-1-Package-build"></a>
## <a name="41-package-build-logs-and-device-in-original-box"></a><span data-ttu-id="a21f5-256">4.1：在原始包装中打包生成日志和设备</span><span class="sxs-lookup"><span data-stu-id="a21f5-256">4.1 Package build logs and Device in original box</span></span> 
<span data-ttu-id="a21f5-257">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="a21f5-257">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="a21f5-258">“设备管理手动测试”中所述的、由问题步骤记录器记录的 Zip 文件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-258">Zip files recorded by Problem Steps recorder as stated in Device Management manual tests.</span></span>
2.  <span data-ttu-id="a21f5-259">手动测试 2 中所述的文本文件</span><span class="sxs-lookup"><span data-stu-id="a21f5-259">Text file as stated in manual test 2</span></span> 
3.  <span data-ttu-id="a21f5-260">装有 IoT Azure 运行时，并已寄送到 Microsoft 做进一步验证的设备。</span><span class="sxs-lookup"><span data-stu-id="a21f5-260">Device with IoT Azure Runtime installed and shipped to Microsoft for further validation.</span></span>

<a name="Step-4-2-Share-Package"></a>
## <a name="42-share-package-with-microsoft-azure-iot-team"></a><span data-ttu-id="a21f5-261">4.2：与 Microsoft Azure IoT 团队成员共享包</span><span class="sxs-lookup"><span data-stu-id="a21f5-261">4.2 Share package with Microsoft Azure IoT team</span></span>

1.  <span data-ttu-id="a21f5-262">转到[合作伙伴仪表板](https://catalog.azureiotsolutions.com/devices)</span><span class="sxs-lookup"><span data-stu-id="a21f5-262">Go to [Partner Dashboard](https://catalog.azureiotsolutions.com/devices)</span></span>
2.  <span data-ttu-id="a21f5-263">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="a21f5-263">Click on Upload icon at top-right corner of device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="a21f5-265">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="a21f5-265">This will open an upload dialog.</span></span> <span data-ttu-id="a21f5-266">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-266">Browse your file(s) by clicking Upload button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="a21f5-268">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="a21f5-268">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="a21f5-269">上传所有文件后，单击“提交审查”按钮。 </span><span class="sxs-lookup"><span data-stu-id="a21f5-269">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="a21f5-270">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="a21f5-270">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>

<a name="Step-4-3-Next-Step"></a>
## <a name="43-next-steps"></a><span data-ttu-id="a21f5-271">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="a21f5-271">4.3 Next steps</span></span>

<span data-ttu-id="a21f5-272">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="a21f5-272">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="a21f5-273">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="a21f5-273">Step 5: Troubleshooting</span></span>

<span data-ttu-id="a21f5-274">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="a21f5-274">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
