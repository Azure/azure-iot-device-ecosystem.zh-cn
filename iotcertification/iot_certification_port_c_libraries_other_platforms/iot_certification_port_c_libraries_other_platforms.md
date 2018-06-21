<a name="how-to-certify-iot-devices-on-non-supported-platforms-with-azure-iot-sdk"></a><span data-ttu-id="214e7-101">如何使用 Azure IoT SDK 认证不支持的平台上的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="214e7-101">How to certify IoT devices on Non-Supported Platforms with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="214e7-102">目录</span><span class="sxs-lookup"><span data-stu-id="214e7-102">Table of Contents</span></span>

-   [<span data-ttu-id="214e7-103">介绍</span><span class="sxs-lookup"><span data-stu-id="214e7-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="214e7-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="214e7-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1)
-   [<span data-ttu-id="214e7-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="214e7-105">Step 2: Register Device</span></span>](#Step_2)
-   [<span data-ttu-id="214e7-106">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="214e7-106">Step 3: Build and Validate the sample using C client libraries</span></span>](#Step_3)
    -   [<span data-ttu-id="214e7-107">3.1 将 C 库移植到其他平台</span><span class="sxs-lookup"><span data-stu-id="214e7-107">3.1 Port the C Libraries to Other Platforms</span></span>](#Step_3_1)
    -   [<span data-ttu-id="214e7-108">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="214e7-108">3.2 Run and Validate the Samples</span></span>](#Step_3_2)
-   [<span data-ttu-id="214e7-109">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="214e7-109">Step 4: Package and Share</span></span>](#Step_4)
    -   [<span data-ttu-id="214e7-110">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="214e7-110">4.1 Package build logs and sample test results</span></span>](#Step_4_1)
    -   [<span data-ttu-id="214e7-111">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="214e7-111">4.2 Share with the Azure IoT Certification team</span></span>](#Step_4_2)
    -   [<span data-ttu-id="214e7-112">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="214e7-112">4.3 Next steps</span></span>](#Step_4_3)
-   [<span data-ttu-id="214e7-113">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="214e7-113">Step 5: Troubleshooting</span></span>](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="214e7-114">介绍</span><span class="sxs-lookup"><span data-stu-id="214e7-114">Introduction</span></span>

<span data-ttu-id="214e7-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="214e7-115">**About this document**</span></span>

<span data-ttu-id="214e7-116">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT C SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="214e7-116">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT C SDK.</span></span> <span data-ttu-id="214e7-117">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="214e7-117">This multi-step process includes:</span></span> 
-   <span data-ttu-id="214e7-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="214e7-118">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="214e7-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="214e7-119">Registering your IoT device</span></span>
-   <span data-ttu-id="214e7-120">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="214e7-120">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="214e7-121">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="214e7-121">Packaging and sharing the logs</span></span>

<span data-ttu-id="214e7-122">**准备**</span><span class="sxs-lookup"><span data-stu-id="214e7-122">**Prepare**</span></span>

<span data-ttu-id="214e7-123">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="214e7-123">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="214e7-124">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="214e7-124">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="214e7-125">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="214e7-125">Computer with GitHub installed and access to the [azure-iot-sdk-c](https://github.com/Azure/azure-iot-sdk-c) GitHub public repository.</span></span>
-   <span data-ttu-id="214e7-126">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="214e7-126">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="214e7-127">用于认证的所需硬件。</span><span class="sxs-lookup"><span data-stu-id="214e7-127">Required hardware to certify.</span></span>

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="214e7-128">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="214e7-128">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="214e7-129">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="214e7-129">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="214e7-130">在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="214e7-130">As part of the sign up process, you will receive the connection string.</span></span> 

-   <span data-ttu-id="214e7-131">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="214e7-131">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="214e7-132">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="214e7-132">Step 2: Register Device</span></span>

<span data-ttu-id="214e7-133">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="214e7-133">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="214e7-134">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="214e7-134">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="214e7-135">设备管理</span><span class="sxs-lookup"><span data-stu-id="214e7-135">Device management</span></span>
    -   <span data-ttu-id="214e7-136">创建新设备</span><span class="sxs-lookup"><span data-stu-id="214e7-136">Create new devices</span></span>
    -   <span data-ttu-id="214e7-137">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="214e7-137">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="214e7-138">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="214e7-138">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="214e7-139">可删除设备</span><span class="sxs-lookup"><span data-stu-id="214e7-139">Provides ability to delete a device</span></span>
-   <span data-ttu-id="214e7-140">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="214e7-140">Monitoring events from your device</span></span>
-   <span data-ttu-id="214e7-141">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="214e7-141">Sending messages to your device</span></span>

<span data-ttu-id="214e7-142">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="214e7-142">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1):</span></span>

-   <span data-ttu-id="214e7-143">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="214e7-143">IoT Hub Connection String</span></span>
    

<span data-ttu-id="214e7-144">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="214e7-144">**Steps:**</span></span>
1.  <span data-ttu-id="214e7-145">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="214e7-145">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="214e7-146">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="214e7-146">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="214e7-147">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="214e7-147">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="214e7-148">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="214e7-148">a.</span></span> <span data-ttu-id="214e7-149">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="214e7-149">Click the **Management** tab.</span></span>

    <span data-ttu-id="214e7-150">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="214e7-150">b.</span></span> <span data-ttu-id="214e7-151">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="214e7-151">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="214e7-152">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="214e7-152">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="214e7-153">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="214e7-153">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="214e7-154">c.</span><span class="sxs-lookup"><span data-stu-id="214e7-154">c.</span></span> <span data-ttu-id="214e7-155">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="214e7-155">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="214e7-156">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="214e7-156">d.</span></span> <span data-ttu-id="214e7-157">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="214e7-157">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="214e7-158">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="214e7-158">e.</span></span> <span data-ttu-id="214e7-159">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="214e7-159">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="214e7-160">f.</span><span class="sxs-lookup"><span data-stu-id="214e7-160">f.</span></span> <span data-ttu-id="214e7-161">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="214e7-161">Save this information in Notepad.</span></span> <span data-ttu-id="214e7-162">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="214e7-162">You will need this information in later steps.</span></span>

<span data-ttu-id="214e7-163">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="214e7-163">***Not running Windows on your PC?***</span></span> <span data-ttu-id="214e7-164">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="214e7-164">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-c-client-libraries"></a><span data-ttu-id="214e7-165">步骤 3：使用 C 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="214e7-165">Step 3: Build and Validate the sample using C client libraries</span></span>

<a name="Step_3_1"></a>
## <a name="31-port-the-c-libraries-to-other-platforms"></a><span data-ttu-id="214e7-166">3.1 将 C 库移植到其他平台</span><span class="sxs-lookup"><span data-stu-id="214e7-166">3.1 Port the C Libraries to Other Platforms</span></span>

<span data-ttu-id="214e7-167">以下文档提供有关如何将 C 物联网 (IoT) 客户端库移植到不现成支持的平台的指南。</span><span class="sxs-lookup"><span data-stu-id="214e7-167">Following document provide guidance on how to port the C Internet of Things (IoT) client library to platforms not supported out of the box.</span></span> <span data-ttu-id="214e7-168">该文档包含有关任何特定平台的具体信息。</span><span class="sxs-lookup"><span data-stu-id="214e7-168">The document does cover the specifics of any particular platform.</span></span>

<span data-ttu-id="214e7-169"><https://github.com/Azure/azure-c-shared-utility/blob/master/devdoc/porting_guide.md></span><span class="sxs-lookup"><span data-stu-id="214e7-169"><https://github.com/Azure/azure-c-shared-utility/blob/master/devdoc/porting_guide.md></span></span>

<a name="Step_3_2"></a>
## <a name="32-run-and-validate-the-samples"></a><span data-ttu-id="214e7-170">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="214e7-170">3.2 Run and Validate the Samples</span></span>

<span data-ttu-id="214e7-171">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="214e7-171">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="214e7-172">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="214e7-172">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> 

<span data-ttu-id="214e7-173">***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2) 中需要用到这些屏幕截图。*</span><span class="sxs-lookup"><span data-stu-id="214e7-173">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2).*</span></span>

<a name="Step_3_2_1"></a>
### <a name="321-send-device-events-to-iot-hub"></a><span data-ttu-id="214e7-174">3.2.1 向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="214e7-174">3.2.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="214e7-175">如[步骤 2](#Step_2) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="214e7-175">Launch the DeviceExplorer as explained in [Step 2](#Step_2) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_Monitor](images/3_2_1_01.png)

2.  <span data-ttu-id="214e7-177">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="214e7-177">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="214e7-178">使用移植客户端库之后创建的、用于将设备事件发送到 IoT 中心的简单示例。</span><span class="sxs-lookup"><span data-stu-id="214e7-178">Use simple sample created after porting client libraries to send device events to IoT Hub.</span></span>

<a name="Step_3_2_2"></a>
### <a name="322-receive-messages-from-iot-hub"></a><span data-ttu-id="214e7-179">3.2.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="214e7-179">3.2.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="214e7-180">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="214e7-180">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="214e7-181">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="214e7-181">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="214e7-182">在“通知”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="214e7-182">Add some text to the Notification field, then click Send.</span></span>

    ![DeviceExplorer\_NotificationSend](images/3_2_2_01.png)

4.  <span data-ttu-id="214e7-184">使用移植客户端库之后创建的、用于从 IoT 中心接收通知消息的示例。</span><span class="sxs-lookup"><span data-stu-id="214e7-184">Use the sample you have created after porting client libraries to receive notification messages from IoT hub.</span></span> <span data-ttu-id="214e7-185">应会看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="214e7-185">You should be able to see the command received.</span></span>

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="214e7-186">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="214e7-186">Step 4: Package and Share</span></span>

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="214e7-187">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="214e7-187">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="214e7-188">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="214e7-188">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="214e7-189">来自平台的生成日志和测试结果。</span><span class="sxs-lookup"><span data-stu-id="214e7-189">Build logs and test results from your platform.</span></span>

2.  <span data-ttu-id="214e7-190">“**向 IoT 中心发送设备事件**”部分中所示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="214e7-190">All the screenshots that belong to "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="214e7-191">“**从 IoT 中心接收消息**”部分中所示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="214e7-191">All the screenshots that belong to "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="214e7-192">创建一个文档，说明如何在硬件上运行示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="214e7-192">Create a document that explains how to run the sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="214e7-193">有关说明形式的指导，请参考[此处](<https://github.com/neeraj-khanna/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="214e7-193">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/neeraj-khanna/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a><span data-ttu-id="214e7-194">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="214e7-194">4.2 Share with the Azure IoT Certification team</span></span>

1.  <span data-ttu-id="214e7-195">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="214e7-195">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="214e7-196">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="214e7-196">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="214e7-198">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="214e7-198">This will open an upload dialog.</span></span> <span data-ttu-id="214e7-199">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="214e7-199">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="214e7-201">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="214e7-201">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="214e7-202">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="214e7-202">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="214e7-203">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="214e7-203">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a><span data-ttu-id="214e7-204">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="214e7-204">4.3 Next steps</span></span>

<span data-ttu-id="214e7-205">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="214e7-205">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="214e7-206">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="214e7-206">Step 5: Troubleshooting</span></span>

<span data-ttu-id="214e7-207">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="214e7-207">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
