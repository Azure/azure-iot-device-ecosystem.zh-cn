<a name="how-to-certify-iot-devices-running-windows-with-azure-iot-sdk"></a><span data-ttu-id="18a14-101">如何使用 Azure IoT SDK 认证运行 Windows 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="18a14-101">How to certify IoT devices running Windows with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="18a14-102">目录</span><span class="sxs-lookup"><span data-stu-id="18a14-102">Table of Contents</span></span>

-   [<span data-ttu-id="18a14-103">介绍</span><span class="sxs-lookup"><span data-stu-id="18a14-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="18a14-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="18a14-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1)
-   [<span data-ttu-id="18a14-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="18a14-105">Step 2: Register Device</span></span>](#Step_2)
-   [<span data-ttu-id="18a14-106">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="18a14-106">Step 3: Build and Validate the sample using Java client libraries</span></span>](#Step_3)
    -   [<span data-ttu-id="18a14-107">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="18a14-107">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>](#Step_3_1)
    -   [<span data-ttu-id="18a14-108">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="18a14-108">3.2 Run and Validate the Samples</span></span>](#Step_3_2)
    -   [<span data-ttu-id="18a14-109">3.3 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="18a14-109">3.3 Verify Device Configuration</span></span>](#Step3_3)
-   [<span data-ttu-id="18a14-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="18a14-110">Step 4: Package and Share</span></span>](#Step_4)
    -   [<span data-ttu-id="18a14-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="18a14-111">4.1 Package build logs and sample test results</span></span>](#Step_4_1)
    -   [<span data-ttu-id="18a14-112">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="18a14-112">4.2 Share with the Azure IoT Certification team</span></span>](#Step_4_2)
    -   [<span data-ttu-id="18a14-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="18a14-113">4.3 Next steps</span></span>](#Step_4_3)
-   [<span data-ttu-id="18a14-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="18a14-114">Step 5: Troubleshooting</span></span>](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="18a14-115">介绍</span><span class="sxs-lookup"><span data-stu-id="18a14-115">Introduction</span></span>

<span data-ttu-id="18a14-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="18a14-116">**About this document**</span></span>

<span data-ttu-id="18a14-117">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT Java SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="18a14-117">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT Java SDK.</span></span> <span data-ttu-id="18a14-118">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="18a14-118">This multi-step process includes:</span></span> 
-   <span data-ttu-id="18a14-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="18a14-119">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="18a14-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="18a14-120">Registering your IoT device</span></span>
-   <span data-ttu-id="18a14-121">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="18a14-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="18a14-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="18a14-122">Packaging and sharing the logs</span></span>

<span data-ttu-id="18a14-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="18a14-123">**Prepare**</span></span>

<span data-ttu-id="18a14-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="18a14-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="18a14-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="18a14-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="18a14-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="18a14-126">Computer with GitHub installed and access to the [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub public repository.</span></span>
-   <span data-ttu-id="18a14-127">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="18a14-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="18a14-128">需要认证的硬件。</span><span class="sxs-lookup"><span data-stu-id="18a14-128">Required hardware to certify.</span></span>

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="18a14-129">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="18a14-129">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="18a14-130">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="18a14-130">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="18a14-131">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="18a14-131">As part of the sign up process, you will receive the connection string.</span></span> 

-   <span data-ttu-id="18a14-132">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="18a14-132">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="18a14-133">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="18a14-133">Step 2: Register Device</span></span>

<span data-ttu-id="18a14-134">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="18a14-134">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="18a14-135">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="18a14-135">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="18a14-136">设备管理</span><span class="sxs-lookup"><span data-stu-id="18a14-136">Device management</span></span>
    -   <span data-ttu-id="18a14-137">创建新设备</span><span class="sxs-lookup"><span data-stu-id="18a14-137">Create new devices</span></span>
    -   <span data-ttu-id="18a14-138">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="18a14-138">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="18a14-139">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="18a14-139">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="18a14-140">提供删除设备的功能</span><span class="sxs-lookup"><span data-stu-id="18a14-140">Provides ability to delete a device</span></span>
-   <span data-ttu-id="18a14-141">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="18a14-141">Monitoring events from your device</span></span>
-   <span data-ttu-id="18a14-142">将消息发送到设备</span><span class="sxs-lookup"><span data-stu-id="18a14-142">Sending messages to your device</span></span>

<span data-ttu-id="18a14-143">若要运行 DeviceExplorer 工具，请使用[步骤 1](#Step_1) 中所述的以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="18a14-143">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1):</span></span>

-   <span data-ttu-id="18a14-144">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="18a14-144">IoT Hub Connection String</span></span>
    

<span data-ttu-id="18a14-145">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="18a14-145">**Steps:**</span></span>
1.  <span data-ttu-id="18a14-146">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="18a14-146">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="18a14-147">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="18a14-147">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="18a14-148">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="18a14-148">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="18a14-149">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="18a14-149">a.</span></span> <span data-ttu-id="18a14-150">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="18a14-150">Click the **Management** tab.</span></span>

    <span data-ttu-id="18a14-151">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="18a14-151">b.</span></span> <span data-ttu-id="18a14-152">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="18a14-152">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="18a14-153">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="18a14-153">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="18a14-154">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="18a14-154">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="18a14-155">c.</span><span class="sxs-lookup"><span data-stu-id="18a14-155">c.</span></span> <span data-ttu-id="18a14-156">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="18a14-156">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="18a14-157">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="18a14-157">d.</span></span> <span data-ttu-id="18a14-158">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="18a14-158">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="18a14-159">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="18a14-159">e.</span></span> <span data-ttu-id="18a14-160">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="18a14-160">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="18a14-161">f.</span><span class="sxs-lookup"><span data-stu-id="18a14-161">f.</span></span> <span data-ttu-id="18a14-162">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="18a14-162">Save this information in Notepad.</span></span> <span data-ttu-id="18a14-163">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="18a14-163">You will need this information in later steps.</span></span>

<span data-ttu-id="18a14-164">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="18a14-164">***Not running Windows on your PC?***</span></span> <span data-ttu-id="18a14-165">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="18a14-165">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-java-client-libraries"></a><span data-ttu-id="18a14-166">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="18a14-166">Step 3: Build and Validate the sample using Java client libraries</span></span>

<span data-ttu-id="18a14-167">本部分逐步讲解如何在运行 Windows 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="18a14-167">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Windows operating system.</span></span> <span data-ttu-id="18a14-168">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="18a14-168">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="18a14-169">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="18a14-169">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1"></a>
## <a name="31-install-azure-iot-device-sdk-and-prerequisites-on-device"></a><span data-ttu-id="18a14-170">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="18a14-170">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>

-   <span data-ttu-id="18a14-171">运行 SDK 需要 Java SE 1.8。</span><span class="sxs-lookup"><span data-stu-id="18a14-171">To run the SDK you will need Java SE 1.8.</span></span>

-   <span data-ttu-id="18a14-172">在设备上使用命令行安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="18a14-172">Install the prerequisite packages using command line on the device.</span></span>

<a name="Step_3_1_1"></a>
### <a name="311--install-java-jdk-18-and-set-up-environment-variables"></a><span data-ttu-id="18a14-173">3.1.1 安装 Java JDK 1.8 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="18a14-173">3.1.1  Install Java JDK 1.8 and set up environment variables</span></span>
        
1.  <span data-ttu-id="18a14-174">有关下载项和安装说明，请访问此处：<http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></span><span class="sxs-lookup"><span data-stu-id="18a14-174">For downloads and installation instructions go here: <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></span></span>
       
2.  <span data-ttu-id="18a14-175">请确保 `PATH` 环境变量包含 jdk1.8.x\bin 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="18a14-175">Please make sure that the `PATH` environment variable includes the full path to the jdk1.8.x\bin directory.</span></span> <span data-ttu-id="18a14-176">（示例：c:\Program Files\Java\jdk1.8.0_65）</span><span class="sxs-lookup"><span data-stu-id="18a14-176">(Example: c:\Program Files\Java\jdk1.8.0_65)</span></span>
        
3.  <span data-ttu-id="18a14-177">请确保 `JAVA_HOME` 环境变量包含 jdk1.8.x 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="18a14-177">Please make sure that the `JAVA_HOME` environment variable includes the full path to the jdk1.8.x directory.</span></span> <span data-ttu-id="18a14-178">（示例：JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65)</span><span class="sxs-lookup"><span data-stu-id="18a14-178">(Example: JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65)</span></span>

4.  <span data-ttu-id="18a14-179">可以通过重新启动控制台并运行 `java -version`，来测试是否已正确设置 PATH 变量。</span><span class="sxs-lookup"><span data-stu-id="18a14-179">You can test whether your PATH variable is set correctly by restarting your console and running `java -version`.</span></span>

<a name="Step_3_1_2"></a>
### <a name="312--install-maven-and-set-up-environment-variables"></a><span data-ttu-id="18a14-180">3.1.2 安装 Maven 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="18a14-180">3.1.2  Install Maven and set up environment variables</span></span>
<span data-ttu-id="18a14-181">建议使用 Maven 3 安装用于 Java 的 Azure IoT 设备 SDK。</span><span class="sxs-lookup"><span data-stu-id="18a14-181">Using Maven 3 is the recommended way to install Azure IoT device SDK for Java.</span></span>

1.  <span data-ttu-id="18a14-182">有关 Maven 3 的下载项和安装说明，请访问此处：<https://maven.apache.org/download.cgi></span><span class="sxs-lookup"><span data-stu-id="18a14-182">For downloads and installation instructions for maven 3 go here: <https://maven.apache.org/download.cgi></span></span>

2.  <span data-ttu-id="18a14-183">请确保 PATH 环境变量包含 apache-maven-3.x.x\bin 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="18a14-183">Please make sure that the PATH environment variable includes the full path to the apache-maven-3.x.x\bin directory.</span></span> <span data-ttu-id="18a14-184">（示例：F:\Setups\apache-maven-3.3.3\bin)。</span><span class="sxs-lookup"><span data-stu-id="18a14-184">(Example: F:\Setups\apache-maven-3.3.3\bin).</span></span> <span data-ttu-id="18a14-185">Apache maven 3.x.x 目录是 Maven 3 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="18a14-185">The apache-maven-3.x.x directory is where Maven 3 is installed.</span></span>

2.  <span data-ttu-id="18a14-186">可以通过重新启动控制台并运行 `mvn --version.`，来验证是否已正确设置用于运行 Maven 3 的环境变量</span><span class="sxs-lookup"><span data-stu-id="18a14-186">You can verify that the environment variables necessary to run Maven 3 have been set correctly by restarting your console and running `mvn --version.`</span></span>
  
<a name="Step_3_1_3"></a>
### <a name="313--install-git"></a><span data-ttu-id="18a14-187">3.1.3 安装 GIT</span><span class="sxs-lookup"><span data-stu-id="18a14-187">3.1.3  Install GIT</span></span>

-   <span data-ttu-id="18a14-188">有关下载项和安装说明，请访问此处：<http://git-scm.com/book/en/v2/Getting-Started-Installing-Git></span><span class="sxs-lookup"><span data-stu-id="18a14-188">For downloads and installation instructions go here: <http://git-scm.com/book/en/v2/Getting-Started-Installing-Git></span></span>

<a name="Step_3_1_4"></a>
### <a name="314--build-qpid-jms"></a><span data-ttu-id="18a14-189">3.1.4 生成 Qpid JMS</span><span class="sxs-lookup"><span data-stu-id="18a14-189">3.1.4  Build Qpid JMS</span></span>

1.  <span data-ttu-id="18a14-190">将 Qpid JMS 的存储库克隆到本地目录。</span><span class="sxs-lookup"><span data-stu-id="18a14-190">Clone the repository for Qpid JMS to your local directory.</span></span>
    
        git clone https://github.com/avranju/qpid-jms.git

2.  <span data-ttu-id="18a14-191">按顺序执行以下命令以安装 Qpid JMS：</span><span class="sxs-lookup"><span data-stu-id="18a14-191">Install Qpid JMS by executing following commands in sequence:</span></span>

        cd qpid-jms
        mvn install
        cd ..

    <span data-ttu-id="18a14-192">\*\**注意：\*\*\*\*我们发现，如果使用最新版本的 JDK 8（编写本文档时，最新版本为 1.8.0_65）如上所示运行 `mvn install` 时，某些单元测试可能会失败。但是，在较低的版本中可以正常运行。如果发生这种情况，请使用以下命令跳过运行单元测试：*</span><span class="sxs-lookup"><span data-stu-id="18a14-192">***Note:*** *We have noticed that certain unit tests can fail when running  `mvn install` as given above with the latest version of JDK 8 (1.8.0_65 at the time this document was written). It works fine with older versions however. If this occurs please skip running unit tests using following command:*</span></span>
    
        mvn install -DskipTests

<a name="Step_3_1_5"></a>
### <a name="315-build-the-azure-iot-device-sdk-for-java"></a><span data-ttu-id="18a14-193">3.1.5 生成适用于 Java 的 Azure IoT 设备 SDK</span><span class="sxs-lookup"><span data-stu-id="18a14-193">3.1.5 Build the Azure IoT Device SDK for Java</span></span>

1.  <span data-ttu-id="18a14-194">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="18a14-194">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-java.git

2.  <span data-ttu-id="18a14-195">验证 **azure-iot-sdk-java** 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="18a14-195">Verify that you now have a copy of the source code under the directory **azure-iot-sdk-java**.</span></span>

3.  <span data-ttu-id="18a14-196">在设备上按顺序运行以下命令，生成 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="18a14-196">Run the following commands on device in sequence to build Azure IoT SDK.</span></span>

        cd azure-iot-sdk-java/device
        mvn install

4.  <span data-ttu-id="18a14-197">上述命令将生成包含所有依赖项的已编译 JAR 文件。</span><span class="sxs-lookup"><span data-stu-id="18a14-197">Above command will generate the compiled JAR files with all dependencies.</span></span> <span data-ttu-id="18a14-198">可在以下位置找到此捆绑包：</span><span class="sxs-lookup"><span data-stu-id="18a14-198">This bundle can be found at:</span></span>

        azure-iot-sdk-java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"></a>
## <a name="32-run-and-validate-the-samples"></a><span data-ttu-id="18a14-199">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="18a14-199">3.2 Run and Validate the Samples</span></span>

<span data-ttu-id="18a14-200">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="18a14-200">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="18a14-201">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="18a14-201">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="18a14-202">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="18a14-202">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="18a14-203">\*\**注意：\*\*\*\*请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="18a14-203">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2).*</span></span>

<a name="Step_3_2_1"></a>
### <a name="321-send-device-events-to-iot-hub"></a><span data-ttu-id="18a14-204">3.2.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="18a14-204">3.2.1 Send Device Events to IoT Hub:</span></span>

1.  <span data-ttu-id="18a14-205">如[步骤 2](#Step_2) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="18a14-205">Launch the DeviceExplorer as explained in [Step 2](#Step_2) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/3_3_1_01.png)

2.  <span data-ttu-id="18a14-207">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="18a14-207">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="18a14-208">导航到包含发送事件示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="18a14-208">Navigate to the folder containing the executable JAR file for send event sample.</span></span>

        cd /azure-iot-sdk-java/device/samples/send-event/target

4.  <span data-ttu-id="18a14-209">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="18a14-209">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="18a14-210">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-210">**If using AMQP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps"
    
    <span data-ttu-id="18a14-211">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-211">**If using HTTP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "https"

    <span data-ttu-id="18a14-212">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-212">**If using MQTT protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "mqtt"
    
    <span data-ttu-id="18a14-213">**如果使用 AMQP-WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-213">**If using AMQP-WebSocket protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps_ws"  

    <span data-ttu-id="18a14-214">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="18a14-214">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="18a14-215">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="18a14-215">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="18a14-216">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="18a14-216">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="18a14-217">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="18a14-217">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

5.  <span data-ttu-id="18a14-218">检查确认消息中是否显示了“OK”。</span><span class="sxs-lookup"><span data-stu-id="18a14-218">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="18a14-219">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="18a14-219">If not, then you may have incorrectly copied the device hub connection information.</span></span>

    <span data-ttu-id="18a14-220">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-220">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="18a14-221">![Terminal\_AMQP\_send\_event](images/terminal_amqp_send_event.PNG)</span><span class="sxs-lookup"><span data-stu-id="18a14-221">![Terminal\_AMQP\_send\_event](images/terminal_amqp_send_event.PNG)</span></span>

    <span data-ttu-id="18a14-222">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-222">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="18a14-223">![Terminal\_HTTP\_send\_event](images/terminal_http_send_event.PNG)</span><span class="sxs-lookup"><span data-stu-id="18a14-223">![Terminal\_HTTP\_send\_event](images/terminal_http_send_event.PNG)</span></span>

    <span data-ttu-id="18a14-224">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-224">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="18a14-225">![Terminal\_MQTT\_send\_event](images/terminal_mqtt_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="18a14-225">![Terminal\_MQTT\_send\_event](images/terminal_mqtt_send_event.png)</span></span>

    <span data-ttu-id="18a14-226">**如果使用 AMQP WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-226">**If using AMQP WebSocket protocol:**</span></span>  
    <span data-ttu-id="18a14-227">![Terminal\_AMQP_WS\_send\_event](images/terminal_amqps_ws_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="18a14-227">![Terminal\_AMQP_WS\_send\_event](images/terminal_amqps_ws_send_event.png)</span></span>

6.  <span data-ttu-id="18a14-228">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="18a14-228">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="18a14-229">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-229">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="18a14-230">![DeviceExplorer\_AMQP\_message\_received](images/device_explorer_amqp_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="18a14-230">![DeviceExplorer\_AMQP\_message\_received](images/device_explorer_amqp_message_received.PNG)</span></span>

    <span data-ttu-id="18a14-231">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-231">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="18a14-232">![DeviceExplorer\_HTTP\_message\_received](images/device_explorer_http_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="18a14-232">![DeviceExplorer\_HTTP\_message\_received](images/device_explorer_http_message_received.PNG)</span></span>

    <span data-ttu-id="18a14-233">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-233">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="18a14-234">![DeviceExplorer\_MQTT\_message\_received](images/device_explorer_mqtt_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="18a14-234">![DeviceExplorer\_MQTT\_message\_received](images/device_explorer_mqtt_message_received.png)</span></span>

    <span data-ttu-id="18a14-235">**如果使用 AMQP WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-235">**If using AMQP WebSocket protocol:**</span></span>  
    <span data-ttu-id="18a14-236">![DeviceExplorer\_AMQP_WS\_message\_received](images/device_explorer_amqp_ws_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="18a14-236">![DeviceExplorer\_AMQP_WS\_message\_received](images/device_explorer_amqp_ws_message_received.png)</span></span>

<a name="Step_3_2_2"></a>
### <a name="322-receive-messages-from-iot-hub"></a><span data-ttu-id="18a14-237">3.2.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="18a14-237">3.2.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="18a14-238">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="18a14-238">To verify that you can send messages from the IoT Hub to your device, go to the **Messages To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="18a14-239">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="18a14-239">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="18a14-240">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="18a14-240">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_message\_send](images/device_explorer_message_send.png)

4.  <span data-ttu-id="18a14-242">导航到包含接收消息示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="18a14-242">Navigate to the folder containing the executable JAR file for the receive message sample.</span></span>

        cd /azure-iot-sdk-java/device/samples/handle-messages/target
     
5.  <span data-ttu-id="18a14-243">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="18a14-243">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="18a14-244">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-244">**If using AMQP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps"
    
    <span data-ttu-id="18a14-245">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-245">**If using HTTP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "https"

    <span data-ttu-id="18a14-246">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-246">**If using MQTT protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "mqtt"

    <span data-ttu-id="18a14-247">**如果使用 AMQP-WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-247">**If using AMQP-WebSocket protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps_ws"

    <span data-ttu-id="18a14-248">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="18a14-248">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="18a14-249">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="18a14-249">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="18a14-250">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="18a14-250">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="18a14-251">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="18a14-251">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

6.  <span data-ttu-id="18a14-252">应会看到客户端示例控制台窗口中收到的命令。</span><span class="sxs-lookup"><span data-stu-id="18a14-252">You should be able to see the command received in the console window for the client sample.</span></span>

    <span data-ttu-id="18a14-253">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-253">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="18a14-254">![Terminal\_AMQP\_message\_received](images/terminal_amqp_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="18a14-254">![Terminal\_AMQP\_message\_received](images/terminal_amqp_message_received.PNG)</span></span>

    <span data-ttu-id="18a14-255">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-255">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="18a14-256">![Terminal\_HTTP\_message\_received](images/terminal_http_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="18a14-256">![Terminal\_HTTP\_message\_received](images/terminal_http_message_received.PNG)</span></span>

    <span data-ttu-id="18a14-257">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-257">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="18a14-258">![Terminal\_MQTT\_message\_received](images/terminal_mqtt_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="18a14-258">![Terminal\_MQTT\_message\_received](images/terminal_mqtt_message_received.png)</span></span>

    <span data-ttu-id="18a14-259">**如果使用 AMQP WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="18a14-259">**If using AMQP WebSocket protocol:**</span></span>  
    <span data-ttu-id="18a14-260">![Terminal\_AMQP_WS\_message\_received](images/terminal_amqp_ws_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="18a14-260">![Terminal\_AMQP_WS\_message\_received](images/terminal_amqp_ws_message_received.png)</span></span>

<a name="#Step3_3"></a>
### <a name="33-verify-device-configuration"></a><span data-ttu-id="18a14-261">3.3 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="18a14-261">3.3 Verify Device configuration</span></span>

-  <span data-ttu-id="18a14-262">在设备上以管理员身份打开 PowerShell 命令提示符，然后运行以下命令</span><span class="sxs-lookup"><span data-stu-id="18a14-262">Open PowerShell command prompt as an Administrator on your device and run the below commands</span></span>

-   <span data-ttu-id="18a14-263">首先使用以下命令检查 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="18a14-263">First check your PowerShell version by using the following command.</span></span>

        $PSversionTable

-  <span data-ttu-id="18a14-264">如果你的当前 PowerShell 版本低于 5.0，请从[此处](https://aka.ms/wmf5download)下载 PowerShell 最新版本</span><span class="sxs-lookup"><span data-stu-id="18a14-264">If your current PowerShell version is less than 5.0 then download the PowerShell latest version from [here](https://aka.ms/wmf5download)</span></span>

    <span data-ttu-id="18a14-265">安装后，请验证新安装的版本，它应为版本 5.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="18a14-265">After installation please verify the newly installed version, it should be version 5.1 or greater.</span></span> 

-   <span data-ttu-id="18a14-266">运行以下命令来获取设备配置信息。</span><span class="sxs-lookup"><span data-stu-id="18a14-266">Run the commands below to get device configuration information.</span></span>

        Get-ComputerInfo -property BiosBIOSVersion, BiosManufacturer, BiosSeralNumber, CsManufacturer, CsModel, CsName, CsNumberOfProcessors, CsProcessors, CsSystemSKUNumber, CsSystemType, OsOperatingSystemSKU | Format-List
          
        Get-NetAdapter
    
    <span data-ttu-id="18a14-267">**如果设备已与以太网连接**</span><span class="sxs-lookup"><span data-stu-id="18a14-267">**If Device connected with Ethernet**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Ethernet" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

    <span data-ttu-id="18a14-268">**如果设备已与 Wi-Fi 连接**</span><span class="sxs-lookup"><span data-stu-id="18a14-268">**If Device connected with Wi-fi**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Wi-fi" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

- <span data-ttu-id="18a14-269">请查看下面的输出屏幕截图</span><span class="sxs-lookup"><span data-stu-id="18a14-269">Please find the output screenshot below</span></span>

    ![deviceinfo\_screenshot](images/device_configuration.png)

-   <span data-ttu-id="18a14-271">请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="18a14-271">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Package).</span></span>

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="18a14-272">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="18a14-272">Step 4: Package and Share</span></span>

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="18a14-273">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="18a14-273">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="18a14-274">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="18a14-274">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="18a14-275">执行步骤 3.1.4 和 3.1.5 过程中在日志文件记录的生成日志和测试结果。</span><span class="sxs-lookup"><span data-stu-id="18a14-275">Build logs and test results that were logged in the log files during steps 3.1.4 and 3.1.5.</span></span>

2.  <span data-ttu-id="18a14-276">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="18a14-276">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="18a14-277">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="18a14-277">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="18a14-278">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="18a14-278">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="18a14-279">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-java.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="18a14-279">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-java.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="18a14-280">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="18a14-280">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a><span data-ttu-id="18a14-281">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="18a14-281">4.2 Share with the Azure IoT Certification team</span></span>

1.  <span data-ttu-id="18a14-282">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="18a14-282">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="18a14-283">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="18a14-283">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="18a14-285">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="18a14-285">This will open an upload dialog.</span></span> <span data-ttu-id="18a14-286">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="18a14-286">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="18a14-288">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="18a14-288">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="18a14-289">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="18a14-289">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="18a14-290">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="18a14-290">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a><span data-ttu-id="18a14-291">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="18a14-291">4.3 Next steps</span></span>

<span data-ttu-id="18a14-292">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="18a14-292">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="18a14-293">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="18a14-293">Step 5: Troubleshooting</span></span>

<span data-ttu-id="18a14-294">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="18a14-294">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
