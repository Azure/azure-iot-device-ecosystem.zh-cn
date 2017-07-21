<a name="how-to-certify-ti-cc3200-device-with-azure-iot-sdk"></a><span data-ttu-id="3cda2-101">如何使用 Azure IoT SDK 认证 TI CC3200 设备</span><span class="sxs-lookup"><span data-stu-id="3cda2-101">How to certify TI CC3200 device with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="3cda2-102">目录</span><span class="sxs-lookup"><span data-stu-id="3cda2-102">Table of Contents</span></span>

-   [<span data-ttu-id="3cda2-103">介绍</span><span class="sxs-lookup"><span data-stu-id="3cda2-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="3cda2-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="3cda2-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1)
-   [<span data-ttu-id="3cda2-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="3cda2-105">Step 2: Register Device</span></span>](#Step_2)
-   [<span data-ttu-id="3cda2-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="3cda2-106">Step 3: Build and Validate the sample using C client libraries</span></span>](#Step_3)
    -   [<span data-ttu-id="3cda2-107">3.1 安装必备组件</span><span class="sxs-lookup"><span data-stu-id="3cda2-107">3.1 Install prerequisites</span></span>](#Step_3_1)
    -   [<span data-ttu-id="3cda2-108">3.2 生成 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="3cda2-108">3.2 Build Azure IoT SDK</span></span>](#Step_3_2)
    -   [<span data-ttu-id="3cda2-109">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="3cda2-109">3.3 Run and Validate the Samples</span></span>](#Step_3_3)
-   [<span data-ttu-id="3cda2-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="3cda2-110">Step 4: Package and Share</span></span>](#Step_4)
    -   [<span data-ttu-id="3cda2-111">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="3cda2-111">4.1 Package build logs and sample test results</span></span>](#Step_4_1)
    -   [<span data-ttu-id="3cda2-112">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="3cda2-112">4.2 Share with the Azure IoT Certification team</span></span>](#Step_4_2)
    -   [<span data-ttu-id="3cda2-113">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="3cda2-113">4.3 Next steps</span></span>](#Step_4_3)
-   [<span data-ttu-id="3cda2-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="3cda2-114">Step 5: Troubleshooting</span></span>](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="3cda2-115">介绍</span><span class="sxs-lookup"><span data-stu-id="3cda2-115">Introduction</span></span>

<span data-ttu-id="3cda2-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="3cda2-116">**About this document**</span></span>

<span data-ttu-id="3cda2-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT C SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="3cda2-117">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT C SDK.</span></span> <span data-ttu-id="3cda2-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="3cda2-118">This multi-step process includes:</span></span> 
-   <span data-ttu-id="3cda2-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="3cda2-119">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="3cda2-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="3cda2-120">Registering your IoT device</span></span>
-   <span data-ttu-id="3cda2-121">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="3cda2-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="3cda2-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="3cda2-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="3cda2-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="3cda2-123">**Prepare**</span></span>

<span data-ttu-id="3cda2-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="3cda2-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="3cda2-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="3cda2-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="3cda2-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="3cda2-126">Computer with GitHub installed and access to the [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub public repository.</span></span>
-   <span data-ttu-id="3cda2-127">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="3cda2-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="3cda2-128">所需的硬件：[CC3200 Launchpad](http://www.ti.com/tool/cc3200-launchxl)。</span><span class="sxs-lookup"><span data-stu-id="3cda2-128">Required hardware [CC3200 Launchpad](http://www.ti.com/tool/cc3200-launchxl).</span></span>

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="3cda2-129">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="3cda2-129">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="3cda2-130">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="3cda2-130">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="3cda2-131">在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3cda2-131">As part of the sign up process, you will receive the connection string.</span></span> 

-   <span data-ttu-id="3cda2-132">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="3cda2-132">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="3cda2-133">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="3cda2-133">Step 2: Register Device</span></span>

<span data-ttu-id="3cda2-134">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="3cda2-134">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="3cda2-135">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3cda2-135">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="3cda2-136">设备管理</span><span class="sxs-lookup"><span data-stu-id="3cda2-136">Device management</span></span>
    -   <span data-ttu-id="3cda2-137">创建新设备</span><span class="sxs-lookup"><span data-stu-id="3cda2-137">Create new devices</span></span>
    -   <span data-ttu-id="3cda2-138">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="3cda2-138">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="3cda2-139">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="3cda2-139">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="3cda2-140">可删除设备</span><span class="sxs-lookup"><span data-stu-id="3cda2-140">Provides ability to delete a device</span></span>
-   <span data-ttu-id="3cda2-141">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="3cda2-141">Monitoring events from your device</span></span>
-   <span data-ttu-id="3cda2-142">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="3cda2-142">Sending messages to your device</span></span>

<span data-ttu-id="3cda2-143">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="3cda2-143">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1):</span></span>

-   <span data-ttu-id="3cda2-144">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="3cda2-144">IoT Hub Connection String</span></span>
    

<span data-ttu-id="3cda2-145">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="3cda2-145">**Steps:**</span></span>
1.  <span data-ttu-id="3cda2-146">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="3cda2-146">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="3cda2-147">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="3cda2-147">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="3cda2-148">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="3cda2-148">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="3cda2-149">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="3cda2-149">a.</span></span> <span data-ttu-id="3cda2-150">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="3cda2-150">Click the **Management** tab.</span></span>

    <span data-ttu-id="3cda2-151">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="3cda2-151">b.</span></span> <span data-ttu-id="3cda2-152">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="3cda2-152">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="3cda2-153">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="3cda2-153">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="3cda2-154">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="3cda2-154">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="3cda2-155">c.</span><span class="sxs-lookup"><span data-stu-id="3cda2-155">c.</span></span> <span data-ttu-id="3cda2-156">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="3cda2-156">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="3cda2-157">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="3cda2-157">d.</span></span> <span data-ttu-id="3cda2-158">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="3cda2-158">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="3cda2-159">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3cda2-159">e.</span></span> <span data-ttu-id="3cda2-160">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="3cda2-160">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="3cda2-161">f.</span><span class="sxs-lookup"><span data-stu-id="3cda2-161">f.</span></span> <span data-ttu-id="3cda2-162">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="3cda2-162">Save this information in Notepad.</span></span> <span data-ttu-id="3cda2-163">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="3cda2-163">You will need this information in later steps.</span></span>

<span data-ttu-id="3cda2-164">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="3cda2-164">***Not running Windows on your PC?***</span></span> <span data-ttu-id="3cda2-165">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="3cda2-165">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="3cda2-166">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="3cda2-166">Step 3: Build and Validate the sample using C client libraries</span></span>

<a name="Step_3_1"></a>
## <a name="31-install-prerequisites"></a><span data-ttu-id="3cda2-167">3.1 安装必备组件</span><span class="sxs-lookup"><span data-stu-id="3cda2-167">3.1 Install prerequisites</span></span>

<span data-ttu-id="3cda2-168">尽管不一定非要这样做，但我们建议在同一个目录中安装 TI 提供的以下工具，并使用不包含任何空白字符的目录名称。</span><span class="sxs-lookup"><span data-stu-id="3cda2-168">While not strictly required, we recommend that you install the following tools from TI in the same directory and that you use directory names without any whitespace.</span></span>

<span data-ttu-id="3cda2-169">***注意：****本文档假设在 `C:\ti` 中安装所有组件。*</span><span class="sxs-lookup"><span data-stu-id="3cda2-169">***Note:*** *This documentation assumes that you install everything in `C:\ti`.*</span></span>

-   <span data-ttu-id="3cda2-170">安装适用于 SimpleLink CC3200 的 [Uniflash Tool](http://www.ti.com/tool/Uniflash) 3.2 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3cda2-170">Install [Uniflash Tool](http://www.ti.com/tool/Uniflash) 3.2 or later for SimpleLink CC3200</span></span>

-   <span data-ttu-id="3cda2-171">安装 [CC3200 SDK 1.1.0](http://www.ti.com/tool/cc3200sdk)</span><span class="sxs-lookup"><span data-stu-id="3cda2-171">Install [CC3200 SDK 1.1.0](http://www.ti.com/tool/cc3200sdk)</span></span>

-   <span data-ttu-id="3cda2-172">安装 [TI-RTOS SDK for SimpleLink](http://downloads.ti.com/dsps/dsps_public_sw/sdo_sb/targetcontent/tirtos/index.html) 2.14.01.20 或更高版本</span><span class="sxs-lookup"><span data-stu-id="3cda2-172">Install [TI-RTOS SDK for SimpleLink](http://downloads.ti.com/dsps/dsps_public_sw/sdo_sb/targetcontent/tirtos/index.html) 2.14.01.20 or above</span></span>

-   <span data-ttu-id="3cda2-173">安装 [NS 包](http://software-dl.ti.com/dsps/dsps_public_sw/sdo_sb/targetcontent/ns/ns_1_10_00_00_eng.zip)。</span><span class="sxs-lookup"><span data-stu-id="3cda2-173">Install [NS package](http://software-dl.ti.com/dsps/dsps_public_sw/sdo_sb/targetcontent/ns/ns_1_10_00_00_eng.zip).</span></span> <span data-ttu-id="3cda2-174">请注意，NS 包为预发行版。</span><span class="sxs-lookup"><span data-stu-id="3cda2-174">Please note, the NS package is a pre-release version.</span></span> <span data-ttu-id="3cda2-175">其内容和下载位置随时可能更改。</span><span class="sxs-lookup"><span data-stu-id="3cda2-175">It's content and the download location are subject to change.</span></span>

-   <span data-ttu-id="3cda2-176">安装 [TI ARM Compiler](http://software-dl.ti.com/ccs/esd/test/ti_cgt_tms470_5.2.5_windows_installer.exe) 5.2.2 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="3cda2-176">Install [TI ARM Compiler](http://software-dl.ti.com/ccs/esd/test/ti_cgt_tms470_5.2.5_windows_installer.exe) 5.2.2 or above.</span></span>

<a name="Step_3_2"></a>
## <a name="32-build-azure-iot-sdk"></a><span data-ttu-id="3cda2-177">3.2 生成 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="3cda2-177">3.2 Build Azure IoT SDK</span></span>

1.  <span data-ttu-id="3cda2-178">编辑文件 `products.mak` (*azure-iot-sdk-c\build_all\tirtos*)。</span><span class="sxs-lookup"><span data-stu-id="3cda2-178">Edit file `products.mak` (*azure-iot-sdk-c\build_all\tirtos*).</span></span> 
    <span data-ttu-id="3cda2-179">更新以下变量的值：</span><span class="sxs-lookup"><span data-stu-id="3cda2-179">Update the value of following variables:</span></span>
    
    <span data-ttu-id="3cda2-180">`XDCTOOLS_INSTALLATION_DIR`：Uniflash Tool 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="3cda2-180">`XDCTOOLS_INSTALLATION_DIR`: install location of Uniflash Tool.</span></span>
    <span data-ttu-id="3cda2-181">`TIRTOS_INSTALLATION_DIR`：TI-RTOS SDK 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="3cda2-181">`TIRTOS_INSTALLATION_DIR`: install location of TI-RTOS SDK.</span></span>
    <span data-ttu-id="3cda2-182">`CC3200SDK_INSTALLATION_DIR`：CC3200 SDK 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="3cda2-182">`CC3200SDK_INSTALLATION_DIR`: install location of CC3200 SDK.</span></span>
    <span data-ttu-id="3cda2-183">`NS_INSTALLATION_DIR`：NS 包的安装位置。</span><span class="sxs-lookup"><span data-stu-id="3cda2-183">`NS_INSTALLATION_DIR`: install location of NS package.</span></span>
    <span data-ttu-id="3cda2-184">`ti.targets.arm.elf.M4`：TI ARM Compiler 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="3cda2-184">`ti.targets.arm.elf.M4`: install location of TI ARM compiler.</span></span>

2. <span data-ttu-id="3cda2-185">打开 Windows 命令提示符。</span><span class="sxs-lookup"><span data-stu-id="3cda2-185">Open a Windows command prompt.</span></span>

3. <span data-ttu-id="3cda2-186">在 Windows 命令提示符中运行以下命令（请务必将路径替换为安装路径）。</span><span class="sxs-lookup"><span data-stu-id="3cda2-186">In the Windows command prompt, run the following commands (be sure to replace the paths with your installation paths).</span></span>

  ```
  cd <AZURE_INSTALL_DIR>\azure-iot-sdk-c\build_all\tirtos
  C:\ti\xdctools_3_31_01_33_core\gmake.exe clean
  C:\ti\xdctools_3_31_01_33_core\gmake.exe all
  ```

<a name="Step_3_3"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="3cda2-187">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="3cda2-187">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="3cda2-188">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="3cda2-188">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="3cda2-189">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="3cda2-189">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> 

<span data-ttu-id="3cda2-190">***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2) 中需要用到这些屏幕截图。*</span><span class="sxs-lookup"><span data-stu-id="3cda2-190">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2).*</span></span>

<a name="Step_3_2_1"></a>
### <a name="331-build-the-sample-simplesamplehttp-application"></a><span data-ttu-id="3cda2-191">3.3.1 生成示例 simplesample_http 应用程序</span><span class="sxs-lookup"><span data-stu-id="3cda2-191">3.3.1 Build the sample simplesample_http application</span></span>

1.  <span data-ttu-id="3cda2-192">打开 `azure-iot-sdk-c\serializer\samples\simplesample_http` 目录中的 `simplesample_http.c` 文件。</span><span class="sxs-lookup"><span data-stu-id="3cda2-192">Open the `simplesample_http.c` file from the directory `azure-iot-sdk-c\serializer\samples\simplesample_http`.</span></span>

2.  <span data-ttu-id="3cda2-193">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="3cda2-193">Find the following place holder for IoT connection string:</span></span>
    
        static const char* connectionString = "[device connection string]";

3.  <span data-ttu-id="3cda2-194">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3cda2-194">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="3cda2-195">可根据“步骤 2”中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3cda2-195">You can get this from DeviceExplorer as explained in Step 2, that you copied into Notepad.</span></span>

4.  <span data-ttu-id="3cda2-196">打开 `azure-iot-sdk-c/serializer/samples/simplesample_http/tirtos/cc3200` 目录中的 `main.c` 文件。</span><span class="sxs-lookup"><span data-stu-id="3cda2-196">Open the file `main.c` from the directory `azure-iot-sdk-c/serializer/samples/simplesample_http/tirtos/cc3200`.</span></span> 

5.  <span data-ttu-id="3cda2-197">找到以下日期时间注释：</span><span class="sxs-lookup"><span data-stu-id="3cda2-197">Find the following comment for date-time:</span></span>

        /* USER STEP: update to current date-time */

6.  <span data-ttu-id="3cda2-198">更新当前日期时间值注释下面的当前日期时间宏。</span><span class="sxs-lookup"><span data-stu-id="3cda2-198">Update the current date-time macros below the comment for current date time values.</span></span>

    ```
    #define DAY     15
    #define MONTH   9
    #define YEAR    2015
    #define HOUR    6
    #define MINUTE  21
    #define SECOND  0
    ```

7. <span data-ttu-id="3cda2-199">打开 `azure-iot-sdk-c/serializer/samples/simplesample_http/tirtos/cc3200` 目录中的 `wificonfig.h` 文件。</span><span class="sxs-lookup"><span data-stu-id="3cda2-199">Open the file `wificonfig.h` from the directory `azure-iot-sdk-c/serializer/samples/simplesample_http/tirtos/cc3200`.</span></span>

8.  <span data-ttu-id="3cda2-200">找到以下 USER STEP 注释：</span><span class="sxs-lookup"><span data-stu-id="3cda2-200">Find the following comment for USER STEP:</span></span>

        /* USER STEP: Update these macros */

9.  <span data-ttu-id="3cda2-201">更新注释下面的 wifi 设置宏。</span><span class="sxs-lookup"><span data-stu-id="3cda2-201">Update the wifi setting macros below the comment.</span></span>

        #define SSID ""
        #define SECURITY_KEY ""

10. <span data-ttu-id="3cda2-202">将[适用于 Windows 的 elf2cc32 可执行文件](https://github.com/tisb-vikram/azure-iot-sdks/blob/7da24633b2c4af3bc779998e9950146f061a8a10/c/serializer/samples/simplesample_http/tirtos/cc3200/tools/elf2cc32.exe?raw=true)或[适用于 Linux 的 elf2cc32 可执行文件](https://github.com/tisb-vikram/azure-iot-sdks/blob/7da24633b2c4af3bc779998e9950146f061a8a10/c/serializer/samples/simplesample_http/tirtos/cc3200/tools/elf2cc32?raw=true)下载到文件夹 `azure-iot-sdk-c\serializer\samples\simplesample_http\tirtos\cc3200\tools`。</span><span class="sxs-lookup"><span data-stu-id="3cda2-202">Download the [elf2cc32 executable for Windows](https://github.com/tisb-vikram/azure-iot-sdks/blob/7da24633b2c4af3bc779998e9950146f061a8a10/c/serializer/samples/simplesample_http/tirtos/cc3200/tools/elf2cc32.exe?raw=true) or [elf2cc32 executable for Linux](https://github.com/tisb-vikram/azure-iot-sdks/blob/7da24633b2c4af3bc779998e9950146f061a8a10/c/serializer/samples/simplesample_http/tirtos/cc3200/tools/elf2cc32?raw=true) to the folder `azure-iot-sdk-c\serializer\samples\simplesample_http\tirtos\cc3200\tools`.</span></span> <span data-ttu-id="3cda2-203">需要使用此工具将 **simplesample_http.out** 转换为 **simplesample_http.bin** 文件。</span><span class="sxs-lookup"><span data-stu-id="3cda2-203">This tool is needed for converting the **simplesample_http.out** to **simplesample_http.bin** file.</span></span>

11. <span data-ttu-id="3cda2-204">执行以下命令生成示例：</span><span class="sxs-lookup"><span data-stu-id="3cda2-204">Build the sample by executing following commands:</span></span>

    ```
    cd <AZURE_INSTALL_DIR>\azure-iot-sdk-c\serializer\samples\simplesample_http\tirtos\cc3200
    C:\ti\xdctools_3_31_01_33_core\gmake.exe clean
    C:\ti\xdctools_3_31_01_33_core\gmake.exe all
    ```

<a name="Step_3_3_2"></a>
### <a name="flash-the-sample-simplesamplehttp-and-the-root-certificate"></a><span data-ttu-id="3cda2-205">刷写示例 simplesample_http 和根证书</span><span class="sxs-lookup"><span data-stu-id="3cda2-205">Flash the sample simplesample_http and the root certificate</span></span>

<span data-ttu-id="3cda2-206">将`simplesample_http.bin` 文件刷写到 CC3200 Launchpad。</span><span class="sxs-lookup"><span data-stu-id="3cda2-206">Flash the `simplesample_http.bin` file to your CC3200 Launchpad.</span></span>

> <span data-ttu-id="3cda2-207">注意：必须将根 CA 证书“Baltimore CyberTrust Root”刷写到 CC3200 Launchpad 上的 `/cert/ms.der` 位置。</span><span class="sxs-lookup"><span data-stu-id="3cda2-207">Note: The root CA certificate - "Baltimore CyberTrust Root" has to be flashed to CC3200 Launchpad to the location `/cert/ms.der`.</span></span> <span data-ttu-id="3cda2-208">此位置将在 `tirtos/cc3200/main.c` 中引用，并由 SimpleLink TLS 堆栈使用。</span><span class="sxs-lookup"><span data-stu-id="3cda2-208">This location is referenced in `tirtos/cc3200/main.c` and is used by SimpleLink TLS stack.</span></span>

<span data-ttu-id="3cda2-209">可在 [CC3200 UniFlash wiki](http://processors.wiki.ti.com/index.php/CC31xx_%26_CC32xx_UniFlash) 中找到有关刷写工具的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3cda2-209">The detailed information about the flash tool can be found in the [CC3200 UniFlash wiki](http://processors.wiki.ti.com/index.php/CC31xx_%26_CC32xx_UniFlash).</span></span> <span data-ttu-id="3cda2-210">[GUI 界面](http://processors.wiki.ti.com/index.php/CC31xx_%26_CC32xx_UniFlash#GUI_Interface)部分逐步讲解了 UniFlash 工具的用法步骤。</span><span class="sxs-lookup"><span data-stu-id="3cda2-210">The section [GUI Interface](http://processors.wiki.ti.com/index.php/CC31xx_%26_CC32xx_UniFlash#GUI_Interface) walks through the steps for using the UniFlash tool.</span></span>

<span data-ttu-id="3cda2-211">将应用程序（.bin 文件）刷写到“系统文件”下面的 `/sys/mcuimg.bin`。</span><span class="sxs-lookup"><span data-stu-id="3cda2-211">Flash the application (.bin file) to the `/sys/mcuimg.bin` under System Files.</span></span> <span data-ttu-id="3cda2-212">对于证书，请在路径 `/cert/ms.der` 中[添加一个新文件](http://processors.wiki.ti.com/index.php/CC31xx_%26_CC32xx_UniFlash#Adding_a_new_file_to_the_device)，并提供“Baltimore CyberTrust Root”证书（.der 格式）的路径。</span><span class="sxs-lookup"><span data-stu-id="3cda2-212">For the certificate, [add a new file](http://processors.wiki.ti.com/index.php/CC31xx_%26_CC32xx_UniFlash#Adding_a_new_file_to_the_device) in the path `/cert/ms.der` and provide the path to the "Baltimore CyberTrust Root" certificate (.der format).</span></span> <span data-ttu-id="3cda2-213">ms.der 文件的路径为 <AZURE 安装目录>\azure-iot-sdk-c\certs\ms.der。</span><span class="sxs-lookup"><span data-stu-id="3cda2-213">The ms.der file is available at <AZURE_INSTALL_DIR>\azure-iot-sdk-c\certs\ms.der.</span></span>

<a name="Step_3_3_3"></a>
### <a name="running-the-sample-simplesamplehttp"></a><span data-ttu-id="3cda2-214">运行示例 simplesample_http</span><span class="sxs-lookup"><span data-stu-id="3cda2-214">Running the sample simplesample_http</span></span>
1.  <span data-ttu-id="3cda2-215">刷写示例后，请使用以下设置打开与相应 COM 端口建立的串行会话：</span><span class="sxs-lookup"><span data-stu-id="3cda2-215">After flashing the example, open a serial session to the appropriate COM port with the following settings:</span></span>

    ```
    Baudrate:     9600
    Data bits:       8
    Stop bits:       1
    Parity:       None
    Flow Control: None
    ```

2.  <span data-ttu-id="3cda2-216">在 CC3200 Launchpad 上按重置按钮运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="3cda2-216">Run the application by pressing the reset button on the CC3200 Launchpad.</span></span> <span data-ttu-id="3cda2-217">应用程序将列显如下所示的消息：</span><span class="sxs-lookup"><span data-stu-id="3cda2-217">The application prints a message similar to the following:</span></span>

    ```
    Starting the simplesample_http example
    CC3200 has connected to AP and acquired an IP address.
    IP Address: XXX.XXX.XX.XXX
    IoTHubClient accepted the message for delivery
    Message Id: 1 Received.
    Result Call Back Called! Result is: IOTHUB_CLIENT_CONFIRMATION_OK
    ```

3.  <span data-ttu-id="3cda2-218">可以使用 DeviceExplorer 监视应用程序发送的数据。</span><span class="sxs-lookup"><span data-stu-id="3cda2-218">The DeviceExplorer can be used to monitor the data sent by the application.</span></span> <span data-ttu-id="3cda2-219">在运行应用程序之前，应在 DeviceExplorer 中的“数据”选项卡下面选择“监视”选项。</span><span class="sxs-lookup"><span data-stu-id="3cda2-219">Under the **Data** tab in DeviceExplorer, **Monitor** option should be selected before running the application.</span></span> <span data-ttu-id="3cda2-220">随后在运行应用程序时，“事件中心数据”窗口中会显示如下所示的消息。</span><span class="sxs-lookup"><span data-stu-id="3cda2-220">Later when the application is run, a message similar to the following message is displayed on "Event Hub Data" window.</span></span>

```
9/17/2015 7:28:28 PM> Data:[{"Temperature":67, "Humidity":42}]
```

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="3cda2-221">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="3cda2-221">Step 4: Package and Share</span></span>

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="3cda2-222">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="3cda2-222">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="3cda2-223">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="3cda2-223">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="3cda2-224">来自平台的生成日志和测试结果。</span><span class="sxs-lookup"><span data-stu-id="3cda2-224">Build logs and test results from your platform.</span></span>

2.  <span data-ttu-id="3cda2-225">“**运行示例 simplesample_http**”部分中所示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3cda2-225">All the screenshots that belong to "**Running the sample simplesample_http**" section.</span></span>

3.  <span data-ttu-id="3cda2-226">创建一个文档，说明如何在硬件上运行示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="3cda2-226">Create a document that explains how to run the sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="3cda2-227">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="3cda2-227">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a><span data-ttu-id="3cda2-228">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="3cda2-228">4.2 Share with the Azure IoT Certification team</span></span>

1.  <span data-ttu-id="3cda2-229">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="3cda2-229">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="3cda2-230">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="3cda2-230">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="3cda2-232">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="3cda2-232">This will open an upload dialog.</span></span> <span data-ttu-id="3cda2-233">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="3cda2-233">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="3cda2-235">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="3cda2-235">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="3cda2-236">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="3cda2-236">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="3cda2-237">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="3cda2-237">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a><span data-ttu-id="3cda2-238">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="3cda2-238">4.3 Next steps</span></span>

<span data-ttu-id="3cda2-239">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="3cda2-239">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="3cda2-240">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="3cda2-240">Step 5: Troubleshooting</span></span>

<span data-ttu-id="3cda2-241">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="3cda2-241">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>