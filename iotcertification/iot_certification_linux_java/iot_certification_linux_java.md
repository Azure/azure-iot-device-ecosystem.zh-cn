<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a><span data-ttu-id="2ee6b-101">如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="2ee6b-101">How to certify IoT devices running Linux with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="2ee6b-102">目录</span><span class="sxs-lookup"><span data-stu-id="2ee6b-102">Table of Contents</span></span>

-   [<span data-ttu-id="2ee6b-103">介绍</span><span class="sxs-lookup"><span data-stu-id="2ee6b-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="2ee6b-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2ee6b-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1)
-   [<span data-ttu-id="2ee6b-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="2ee6b-105">Step 2: Register Device</span></span>](#Step_2)
-   [<span data-ttu-id="2ee6b-106">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="2ee6b-106">Step 3: Build and Validate the sample using Java client libraries</span></span>](#Step_3)
    -   [<span data-ttu-id="2ee6b-107">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="2ee6b-107">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>](#Step_3_1)
    -   [<span data-ttu-id="2ee6b-108">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="2ee6b-108">3.2 Run and Validate the Samples</span></span>](#Step_3_2)
-   [<span data-ttu-id="2ee6b-109">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="2ee6b-109">Step 4: Package and Share</span></span>](#Step_4)
    -   [<span data-ttu-id="2ee6b-110">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="2ee6b-110">4.1 Package build logs and sample test results</span></span>](#Step_4_1)
    -   [<span data-ttu-id="2ee6b-111">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="2ee6b-111">4.2 Share with the Azure IoT Certification team</span></span>](#Step_4_2)
    -   [<span data-ttu-id="2ee6b-112">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="2ee6b-112">4.3 Next steps</span></span>](#Step_4_3)
-   [<span data-ttu-id="2ee6b-113">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="2ee6b-113">Step 5: Troubleshooting</span></span>](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="2ee6b-114">介绍</span><span class="sxs-lookup"><span data-stu-id="2ee6b-114">Introduction</span></span>

<span data-ttu-id="2ee6b-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-115">**About this document**</span></span>

<span data-ttu-id="2ee6b-116">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT Java SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-116">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT Java SDK.</span></span> <span data-ttu-id="2ee6b-117">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-117">This multi-step process includes:</span></span> 
-   <span data-ttu-id="2ee6b-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2ee6b-118">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="2ee6b-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="2ee6b-119">Registering your IoT device</span></span>
-   <span data-ttu-id="2ee6b-120">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="2ee6b-120">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="2ee6b-121">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="2ee6b-121">Packaging and sharing the logs</span></span>

<span data-ttu-id="2ee6b-122">**准备**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-122">**Prepare**</span></span>

<span data-ttu-id="2ee6b-123">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-123">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="2ee6b-124">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-124">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="2ee6b-125">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-125">Computer with GitHub installed and access to the [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub public repository.</span></span>
-   <span data-ttu-id="2ee6b-126">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-126">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="2ee6b-127">用于认证的所需硬件。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-127">Required hardware to certify.</span></span>

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="2ee6b-128">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2ee6b-128">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="2ee6b-129">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-129">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="2ee6b-130">在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-130">As part of the sign up process, you will receive the connection string.</span></span> 

-   <span data-ttu-id="2ee6b-131">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-131">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="2ee6b-132">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="2ee6b-132">Step 2: Register Device</span></span>

<span data-ttu-id="2ee6b-133">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-133">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="2ee6b-134">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-134">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="2ee6b-135">设备管理</span><span class="sxs-lookup"><span data-stu-id="2ee6b-135">Device management</span></span>
    -   <span data-ttu-id="2ee6b-136">创建新设备</span><span class="sxs-lookup"><span data-stu-id="2ee6b-136">Create new devices</span></span>
    -   <span data-ttu-id="2ee6b-137">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="2ee6b-137">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="2ee6b-138">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="2ee6b-138">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="2ee6b-139">可删除设备</span><span class="sxs-lookup"><span data-stu-id="2ee6b-139">Provides ability to delete a device</span></span>
-   <span data-ttu-id="2ee6b-140">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="2ee6b-140">Monitoring events from your device</span></span>
-   <span data-ttu-id="2ee6b-141">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="2ee6b-141">Sending messages to your device</span></span>

<span data-ttu-id="2ee6b-142">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-142">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1):</span></span>

-   <span data-ttu-id="2ee6b-143">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="2ee6b-143">IoT Hub Connection String</span></span>
    

<span data-ttu-id="2ee6b-144">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-144">**Steps:**</span></span>
1.  <span data-ttu-id="2ee6b-145">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer</span><span class="sxs-lookup"><span data-stu-id="2ee6b-145">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer</span></span>

2.  <span data-ttu-id="2ee6b-146">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-146">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="2ee6b-147">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-147">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="2ee6b-148">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-148">a.</span></span> <span data-ttu-id="2ee6b-149">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-149">Click the **Management** tab.</span></span>

    <span data-ttu-id="2ee6b-150">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-150">b.</span></span> <span data-ttu-id="2ee6b-151">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-151">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="2ee6b-152">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-152">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="2ee6b-153">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-153">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="2ee6b-154">c.</span><span class="sxs-lookup"><span data-stu-id="2ee6b-154">c.</span></span> <span data-ttu-id="2ee6b-155">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-155">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="2ee6b-156">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-156">d.</span></span> <span data-ttu-id="2ee6b-157">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-157">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="2ee6b-158">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-158">e.</span></span> <span data-ttu-id="2ee6b-159">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-159">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="2ee6b-160">f.</span><span class="sxs-lookup"><span data-stu-id="2ee6b-160">f.</span></span> <span data-ttu-id="2ee6b-161">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-161">Save this information in Notepad.</span></span> <span data-ttu-id="2ee6b-162">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-162">You will need this information in later steps.</span></span>

<span data-ttu-id="2ee6b-163">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="2ee6b-163">***Not running Windows on your PC?***</span></span> <span data-ttu-id="2ee6b-164">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-164">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-java-client-libraries"></a><span data-ttu-id="2ee6b-165">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="2ee6b-165">Step 3: Build and Validate the sample using Java client libraries</span></span>

<span data-ttu-id="2ee6b-166">本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-166">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Linux operating system.</span></span> <span data-ttu-id="2ee6b-167">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-167">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="2ee6b-168">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-168">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1"></a>
## <a name="31-install-azure-iot-device-sdk-and-prerequisites-on-device"></a><span data-ttu-id="2ee6b-169">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="2ee6b-169">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>

-   <span data-ttu-id="2ee6b-170">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-170">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="2ee6b-171">在设备上的命令行中发出以下命令，安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-171">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span>

<a name="Step_3_1_1"></a>
### <a name="311--install-java-jdk-and-set-up-environment-variables"></a><span data-ttu-id="2ee6b-172">3.1.1 安装 Java JDK 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="2ee6b-172">3.1.1  Install Java JDK and set up environment variables</span></span>
        
1.  <span data-ttu-id="2ee6b-173">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-173">Choose your commands based on the OS running on your device.</span></span>
        
    <span data-ttu-id="2ee6b-174">**Debian**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-174">**Debian**</span></span>

        sudo apt-get update        
        sudo apt-get install openjdk-8-jdk      
   
    <span data-ttu-id="2ee6b-175">***注意：****如果 openjdk-8-jdk 包不可用，请使用以下步骤在 sources.list 中添加源，然后再次重新运行上述命令。*</span><span class="sxs-lookup"><span data-stu-id="2ee6b-175">***Note:*** *If openjdk-8-jdk package is not available, use following steps to add source in sources.list and rerun above commands again.*</span></span>
    
    -   <span data-ttu-id="2ee6b-176">编辑 /etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="2ee6b-176">Edit /etc/apt/sources.list</span></span>
    
    -   <span data-ttu-id="2ee6b-177">添加以下代码行并保存更改。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-177">Add below line and save the changes.</span></span>
        
        `deb http://ftp.debian.org/debian testing main`
   
    <span data-ttu-id="2ee6b-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-178">**Ubuntu**</span></span>

        sudo apt-get update        
        sudo apt-get install openjdk-8-jdk 
   
    <span data-ttu-id="2ee6b-179">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-179">**Fedora**</span></span>
   
        sudo dnf check-update -y
        sudo dnf install java-1.8.0-openjdk-devel
        
    <span data-ttu-id="2ee6b-180">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-180">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS
       
2.  <span data-ttu-id="2ee6b-181">更新 PATH 环境变量，加入包含 Java 的 bin 文件夹的完整路径。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-181">Update the PATH environment variable to include the full path to the bin folder containing Java.</span></span> <span data-ttu-id="2ee6b-182">为确保 Java 路径正确，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-182">To ensure the correct path of Java run below command:</span></span>     
       
        which java
        
3.  <span data-ttu-id="2ee6b-183">确保 `which java` 命令显示的目录与 $PATH 变量中显示的某个目录匹配。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-183">Ensure that the directory shown by the `which java` command matches one of the directories shown in your $PATH variable.</span></span> <span data-ttu-id="2ee6b-184">可运行以下命令来确认是否存在匹配项：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-184">You can confirm this by running following command.</span></span>

        echo $PATH

4.  <span data-ttu-id="2ee6b-185">如果 PATH 环境变量中缺少 Java 路径，请运行以下命令设置相同的路径。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-185">If Java path is missing in PATH environment variable, run following command to set the same.</span></span>    

        export PATH=[PathToJava]/bin:$PATH       

    <span data-ttu-id="2ee6b-186">***注意：****此处的 **[PathToJava]** 是 `which java` 命令的输出。例如，如果 `which java` 输出为 /usr/bin/java，则导出命令为* **export PATH=/usr/bin/java/bin:$PATH**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-186">***NOTE:*** *Here **[PathToJava]** is output of `which java` command. For example, if `which java` output is /usr/bin/java, then export command will be* **export PATH=/usr/bin/java/bin:$PATH**</span></span>

5.  <span data-ttu-id="2ee6b-187">确保 JAVA_HOME 环境变量包含 JDK 的完整路径。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-187">Make sure that the JAVA_HOME environment variable includes the full path to the JDK.</span></span> <span data-ttu-id="2ee6b-188">使用以下命令获取 JDK 路径。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-188">Use below command to get the JDK path.</span></span>

        update-alternatives --config java

6.  <span data-ttu-id="2ee6b-189">记下 JDK 位置。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-189">Take note of the JDK location.</span></span> <span data-ttu-id="2ee6b-190">`update-alternatives` 的输出类似于 **/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java**。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-190">`update-alternatives` output will show something similar to **/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java**.</span></span> <span data-ttu-id="2ee6b-191">在此情况下，JDK 目录为 **/usr/lib/jvm/java-8-openjdk-amd64/**。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-191">The JDK directory would then be **/usr/lib/jvm/java-8-openjdk-amd64/**.</span></span>

7.  <span data-ttu-id="2ee6b-192">运行以下命令设置 **JAVA_HOME** 环境变量。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-192">Run the following command to set **JAVA_HOME** environment variable.</span></span>

        export JAVA_HOME=[PathToJDK]

    <span data-ttu-id="2ee6b-193">***注意***：*此处的 [PathToJDK] 是 JDK 目录。例如，如果 jdk 目录为 /usr/lib/jvm/java-8-openjdk-amd64/，则导出命令为* **export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-193">***Note***: *Here [PathToJDK] is JDK directory. For example if jdk directory is /usr/lib/jvm/java-8-openjdk-amd64/, export command will be* **export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/**</span></span>

<a name="Step_3_1_2"></a>
### <a name="312--install-maven-and-set-up-environment-variables"></a><span data-ttu-id="2ee6b-194">3.1.2 安装 Maven 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="2ee6b-194">3.1.2  Install Maven and set up environment variables</span></span>

1.  <span data-ttu-id="2ee6b-195">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-195">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="2ee6b-196">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-196">**Debian or Ubuntu**</span></span>

        sudo apt-get install maven

    <span data-ttu-id="2ee6b-197">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-197">**Fedora**</span></span>

        sudo dnf install maven
   
    <span data-ttu-id="2ee6b-198">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-198">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

2.  <span data-ttu-id="2ee6b-199">更新 PATH 环境变量，加入包含 Maven 的 bin 文件夹的完整路径。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-199">Update the PATH environment variable to include the full path to the bin folder containing maven.</span></span> <span data-ttu-id="2ee6b-200">为确保 Maven 路径正确，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-200">To ensure the correct path of maven, run below command:</span></span>     
       
        which mvn
         
3.  <span data-ttu-id="2ee6b-201">确保 `which mvn` 命令显示的目录与 $PATH 变量中显示的某个目录匹配。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-201">Ensure that the directory shown by the `which mvn` command matches one of the directories shown in your $PATH variable.</span></span> <span data-ttu-id="2ee6b-202">可运行以下命令来确认是否存在匹配项：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-202">You can confirm this by running following command.</span></span>
 
        echo $PATH

4.  <span data-ttu-id="2ee6b-203">如果 PATH 环境变量中缺少 Maven 路径，请运行以下命令设置相同的路径。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-203">If maven path is missing in PATH environment variable, run following command to set the same.</span></span>     

        export PATH=[PathToMvn]/bin:$PATH

    <span data-ttu-id="2ee6b-204">***注意***：*此处的 [PathToMvn] 是 `which mvn` 的输出。例如，如果 `which mvn` 输出为 /usr/bin/mvn，则导出命令为* **export PATH=/usr/bin/mvn/bin:$PATH**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-204">***Note***: *Here [PathToMvn] is output of `which mvn`. For example if `which mvn` output is /usr/bin/mvn, export command will be* **export PATH=/usr/bin/mvn/bin:$PATH**</span></span>
   
5.  <span data-ttu-id="2ee6b-205">可以运行 `mvn --version` 来验证是否已正确设置用于运行 Maven 3 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-205">You can verify that the environment variables necessary to run Maven 3 have been set correctly by running `mvn --version`.</span></span>

<a name="Step_3_1_3"></a>
### <a name="313--install-git"></a><span data-ttu-id="2ee6b-206">3.1.3 安装 GIT</span><span class="sxs-lookup"><span data-stu-id="2ee6b-206">3.1.3  Install GIT</span></span>

1.  <span data-ttu-id="2ee6b-207">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-207">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="2ee6b-208">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-208">**Debian or Ubuntu**</span></span>

        sudo apt-get install git

    <span data-ttu-id="2ee6b-209">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-209">**Fedora**</span></span>

        sudo dnf install git   

    <span data-ttu-id="2ee6b-210">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-210">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

<a name="Step_3_1_4"></a>
### <a name="314-build-the-azure-iot-device-sdk-for-java"></a><span data-ttu-id="2ee6b-211">3.1.4 生成适用于 Java 的 Azure IoT 设备 SDK</span><span class="sxs-lookup"><span data-stu-id="2ee6b-211">3.1.4 Build the Azure IoT Device SDK for Java</span></span>

1.  <span data-ttu-id="2ee6b-212">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-212">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-java.git

2.  <span data-ttu-id="2ee6b-213">验证 **azure-iot-sdk-java** 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-213">Verify that you now have a copy of the source code under the directory **azure-iot-sdk-java**.</span></span>

3.  <span data-ttu-id="2ee6b-214">在设备上按顺序运行以下命令，生成 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-214">Run the following commands on device in sequence to build Azure IoT SDK.</span></span>

        cd azure-iot-sdk-java/device
        mvn install | tee JavaSDK_Build_Logs.txt

4.  <span data-ttu-id="2ee6b-215">上述命令将生成包含所有依赖项的已编译 JAR 文件。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-215">Above command will generate the compiled JAR files with all dependencies.</span></span> <span data-ttu-id="2ee6b-216">可在以下位置找到此捆绑包：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-216">This bundle can be found at:</span></span>

        azure-iot-sdk-java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"></a>
## <a name="32-run-and-validate-the-samples"></a><span data-ttu-id="2ee6b-217">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="2ee6b-217">3.2 Run and Validate the Samples</span></span>

<span data-ttu-id="2ee6b-218">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-218">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="2ee6b-219">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-219">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="2ee6b-220">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-220">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="2ee6b-221">***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2) 中需要用到这些屏幕截图。*</span><span class="sxs-lookup"><span data-stu-id="2ee6b-221">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2).*</span></span>

<a name="Step_3_2_1"></a>
### <a name="321-send-device-events-to-iot-hub"></a><span data-ttu-id="2ee6b-222">3.2.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-222">3.2.1 Send Device Events to IoT Hub:</span></span>

1.  <span data-ttu-id="2ee6b-223">如[步骤 2](#Step_2) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-223">Launch the DeviceExplorer as explained in [Step 2](#Step_2) and navigate to **Data** tab.</span></span> <span data-ttu-id="2ee6b-224">从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-224">Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_Monitor](images/3_3_1_01.png)

2.  <span data-ttu-id="2ee6b-226">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-226">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="2ee6b-227">导航到包含发送事件示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-227">Navigate to the folder containing the executable JAR file for send event sample.</span></span>

        cd azure-iot-sdk-java/device/samples/send-event/target

4.  <span data-ttu-id="2ee6b-228">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-228">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="2ee6b-229">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-229">**If using AMQP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps"
    
    <span data-ttu-id="2ee6b-230">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-230">**If using HTTP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "https"

    <span data-ttu-id="2ee6b-231">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-231">**If using MQTT protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "mqtt"
    
    <span data-ttu-id="2ee6b-232">**如果将 Web Socket 与 AMQP 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-232">**If using Web Sockets with AMQP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps_ws"    

    <span data-ttu-id="2ee6b-233">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-233">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="2ee6b-234">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="2ee6b-234">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="2ee6b-235">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="2ee6b-235">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="2ee6b-236">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="2ee6b-236">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

5.  <span data-ttu-id="2ee6b-237">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-237">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="2ee6b-238">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-238">If not, then you may have incorrectly copied the device hub connection information.</span></span>

    <span data-ttu-id="2ee6b-239">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-239">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="2ee6b-240">![Terminal\_AMQP\_send\_event](images/terminal_amqp_send_event.PNG)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-240">![Terminal\_AMQP\_send\_event](images/terminal_amqp_send_event.PNG)</span></span>

    <span data-ttu-id="2ee6b-241">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-241">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="2ee6b-242">![Terminal\_HTTP\_send\_event](images/terminal_http_send_event.PNG)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-242">![Terminal\_HTTP\_send\_event](images/terminal_http_send_event.PNG)</span></span>

    <span data-ttu-id="2ee6b-243">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-243">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="2ee6b-244">![Terminal\_MQTT\_send\_event](images/terminal_mqtt_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-244">![Terminal\_MQTT\_send\_event](images/terminal_mqtt_send_event.png)</span></span>

    <span data-ttu-id="2ee6b-245">**如果将 Web Socket 与 AMQP 协议配合使用：**
    ![Terminal\_AMQP_WS\_send\_event](images/terminal_amqps_ws_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-245">**If using Web Sockets with AMQP protocol:**
![Terminal\_AMQP_WS\_send\_event](images/terminal_amqps_ws_send_event.png)</span></span>

6.  <span data-ttu-id="2ee6b-246">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-246">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="2ee6b-247">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-247">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="2ee6b-248">![DeviceExplorer\_AMQP\_message\_received](images/device_explorer_amqp_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-248">![DeviceExplorer\_AMQP\_message\_received](images/device_explorer_amqp_message_received.PNG)</span></span>

    <span data-ttu-id="2ee6b-249">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-249">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="2ee6b-250">![DeviceExplorer\_HTTP\_message\_received](images/device_explorer_http_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-250">![DeviceExplorer\_HTTP\_message\_received](images/device_explorer_http_message_received.PNG)</span></span>

    <span data-ttu-id="2ee6b-251">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-251">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="2ee6b-252">![DeviceExplorer\_MQTT\_message\_received](images/device_explorer_mqtt_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-252">![DeviceExplorer\_MQTT\_message\_received](images/device_explorer_mqtt_message_received.png)</span></span>

<a name="Step_3_2_2"></a>
### <a name="322-receive-messages-from-iot-hub"></a><span data-ttu-id="2ee6b-253">3.2.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="2ee6b-253">3.2.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="2ee6b-254">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-254">To verify that you can send messages from the IoT Hub to your device, go to the **Messages To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="2ee6b-255">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-255">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="2ee6b-256">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-256">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_message\_send](images/device_explorer_message_send.PNG)

4.  <span data-ttu-id="2ee6b-258">导航到包含接收消息示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-258">Navigate to the folder containing the executable JAR file for the receive message sample.</span></span>

        cd azure-iot-sdk-java/device/samples/handle-messages/target
     
5.  <span data-ttu-id="2ee6b-259">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-259">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="2ee6b-260">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-260">**If using AMQP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps"
    
    <span data-ttu-id="2ee6b-261">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-261">**If using HTTP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "https"

    <span data-ttu-id="2ee6b-262">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-262">**If using MQTT protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "mqtt"

    <span data-ttu-id="2ee6b-263">**如果将 Web Socket 与 AMQP 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-263">**If using Web Sockets with AMQP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps_ws"

    <span data-ttu-id="2ee6b-264">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-264">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="2ee6b-265">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="2ee6b-265">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="2ee6b-266">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="2ee6b-266">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="2ee6b-267">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="2ee6b-267">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

6.  <span data-ttu-id="2ee6b-268">应会在客户端示例的控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-268">You should be able to see the command received in the console window for the client sample.</span></span>

    <span data-ttu-id="2ee6b-269">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-269">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="2ee6b-270">![Terminal\_AMQP\_message\_received](images/terminal_amqp_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-270">![Terminal\_AMQP\_message\_received](images/terminal_amqp_message_received.PNG)</span></span>

    <span data-ttu-id="2ee6b-271">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-271">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="2ee6b-272">![Terminal\_HTTP\_message\_received](images/terminal_http_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-272">![Terminal\_HTTP\_message\_received](images/terminal_http_message_received.PNG)</span></span>

    <span data-ttu-id="2ee6b-273">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2ee6b-273">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="2ee6b-274">![Terminal\_MQTT\_message\_received](images/terminal_mqtt_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-274">![Terminal\_MQTT\_message\_received](images/terminal_mqtt_message_received.png)</span></span>

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="2ee6b-275">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="2ee6b-275">Step 4: Package and Share</span></span>

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="2ee6b-276">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="2ee6b-276">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="2ee6b-277">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="2ee6b-277">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="2ee6b-278">执行步骤 3.1.4 和 3.1.5 过程中在日志文件记录的生成日志和测试结果。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-278">Build logs and test results that were logged in the log files during steps 3.1.4 and 3.1.5.</span></span>

2.  <span data-ttu-id="2ee6b-279">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-279">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="2ee6b-280">前面“**从 IoT 中心接收消息**”部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-280">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="2ee6b-281">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-281">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="2ee6b-282">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-java.md>)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-282">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-java.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="2ee6b-283">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-283">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a><span data-ttu-id="2ee6b-284">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="2ee6b-284">4.2 Share with the Azure IoT Certification team</span></span>

1.  <span data-ttu-id="2ee6b-285">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="2ee6b-285">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="2ee6b-286">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-286">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="2ee6b-288">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-288">This will open an upload dialog.</span></span> <span data-ttu-id="2ee6b-289">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-289">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="2ee6b-291">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-291">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="2ee6b-292">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-292">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="2ee6b-293">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="2ee6b-293">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a><span data-ttu-id="2ee6b-294">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="2ee6b-294">4.3 Next steps</span></span>

<span data-ttu-id="2ee6b-295">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-295">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="2ee6b-296">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="2ee6b-296">Step 5: Troubleshooting</span></span>

<span data-ttu-id="2ee6b-297">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="2ee6b-297">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>