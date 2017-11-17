<a name="how-to-certify-iot-devices-running-windows-with-azure-iot-sdk"></a><span data-ttu-id="728b4-101">如何使用 Azure IoT SDK 认证运行 Windows 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="728b4-101">How to certify IoT devices running Windows with Azure IoT SDK</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="728b4-102">目录</span><span class="sxs-lookup"><span data-stu-id="728b4-102">Table of Contents</span></span>

-   [<span data-ttu-id="728b4-103">介绍</span><span class="sxs-lookup"><span data-stu-id="728b4-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="728b4-104">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="728b4-104">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1)
-   [<span data-ttu-id="728b4-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="728b4-105">Step 2: Register Device</span></span>](#Step_2)
-   [<span data-ttu-id="728b4-106">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="728b4-106">Step 3: Build and Validate the sample using Java client libraries</span></span>](#Step_3)
    -   [<span data-ttu-id="728b4-107">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="728b4-107">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>](#Step_3_1)
    -   [<span data-ttu-id="728b4-108">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="728b4-108">3.2 Run and Validate the Samples</span></span>](#Step_3_2)
-   [<span data-ttu-id="728b4-109">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="728b4-109">Step 4: Package and Share</span></span>](#Step_4)
    -   [<span data-ttu-id="728b4-110">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="728b4-110">4.1 Package build logs and sample test results</span></span>](#Step_4_1)
    -   [<span data-ttu-id="728b4-111">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="728b4-111">4.2 Share with the Azure IoT Certification team</span></span>](#Step_4_2)
    -   [<span data-ttu-id="728b4-112">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="728b4-112">4.3 Next steps</span></span>](#Step_4_3)
-   [<span data-ttu-id="728b4-113">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="728b4-113">Step 5: Troubleshooting</span></span>](#Step_5)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="728b4-114">介绍</span><span class="sxs-lookup"><span data-stu-id="728b4-114">Introduction</span></span>

<span data-ttu-id="728b4-115">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="728b4-115">**About this document**</span></span>

<span data-ttu-id="728b4-116">本文档向 IoT 硬件发布人员提供有关如何使用 Azure IoT Java SDK 认证已启用 IoT 的硬件的分步指南。</span><span class="sxs-lookup"><span data-stu-id="728b4-116">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT Java SDK.</span></span> <span data-ttu-id="728b4-117">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="728b4-117">This multi-step process includes:</span></span> 
-   <span data-ttu-id="728b4-118">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="728b4-118">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="728b4-119">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="728b4-119">Registering your IoT device</span></span>
-   <span data-ttu-id="728b4-120">在设备上生成并部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="728b4-120">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="728b4-121">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="728b4-121">Packaging and sharing the logs</span></span>

<span data-ttu-id="728b4-122">**准备**</span><span class="sxs-lookup"><span data-stu-id="728b4-122">**Prepare**</span></span>

<span data-ttu-id="728b4-123">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="728b4-123">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="728b4-124">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="728b4-124">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="728b4-125">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="728b4-125">Computer with GitHub installed and access to the [azure-iot-sdk-java](https://github.com/Azure/azure-iot-sdk-java) GitHub public repository.</span></span>
-   <span data-ttu-id="728b4-126">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行。</span><span class="sxs-lookup"><span data-stu-id="728b4-126">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line.</span></span>
-   <span data-ttu-id="728b4-127">用于认证的所需硬件。</span><span class="sxs-lookup"><span data-stu-id="728b4-127">Required hardware to certify.</span></span>

<a name="Step_1"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="728b4-128">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="728b4-128">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="728b4-129">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)所述的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="728b4-129">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="728b4-130">在注册过程中，你将收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="728b4-130">As part of the sign up process, you will receive the connection string.</span></span> 

-   <span data-ttu-id="728b4-131">**IoT 中心连接字符串**：IoT 中心的连接字符串示例如下：</span><span class="sxs-lookup"><span data-stu-id="728b4-131">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

         HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="728b4-132">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="728b4-132">Step 2: Register Device</span></span>

<span data-ttu-id="728b4-133">在本部分，将要使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="728b4-133">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="728b4-134">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="728b4-134">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="728b4-135">设备管理</span><span class="sxs-lookup"><span data-stu-id="728b4-135">Device management</span></span>
    -   <span data-ttu-id="728b4-136">创建新设备</span><span class="sxs-lookup"><span data-stu-id="728b4-136">Create new devices</span></span>
    -   <span data-ttu-id="728b4-137">列出现有设备，公开设备中心内存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="728b4-137">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="728b4-138">可更新设备密钥</span><span class="sxs-lookup"><span data-stu-id="728b4-138">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="728b4-139">可删除设备</span><span class="sxs-lookup"><span data-stu-id="728b4-139">Provides ability to delete a device</span></span>
-   <span data-ttu-id="728b4-140">监视设备的事件</span><span class="sxs-lookup"><span data-stu-id="728b4-140">Monitoring events from your device</span></span>
-   <span data-ttu-id="728b4-141">向设备发送消息</span><span class="sxs-lookup"><span data-stu-id="728b4-141">Sending messages to your device</span></span>

<span data-ttu-id="728b4-142">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Step_1) 中所述使用以下配置字符串：</span><span class="sxs-lookup"><span data-stu-id="728b4-142">To run DeviceExplorer tool, use following configuration string as described in [Step1](#Step_1):</span></span>

-   <span data-ttu-id="728b4-143">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="728b4-143">IoT Hub Connection String</span></span>
    

<span data-ttu-id="728b4-144">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="728b4-144">**Steps:**</span></span>
1.  <span data-ttu-id="728b4-145">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="728b4-145">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="728b4-146">添加“配置”选项卡下面的连接信息，然后单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="728b4-146">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="728b4-147">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="728b4-147">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="728b4-148">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="728b4-148">a.</span></span> <span data-ttu-id="728b4-149">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="728b4-149">Click the **Management** tab.</span></span>

    <span data-ttu-id="728b4-150">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="728b4-150">b.</span></span> <span data-ttu-id="728b4-151">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="728b4-151">Your registered devices will be displayed in the list.</span></span> <span data-ttu-id="728b4-152">如果你的设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="728b4-152">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="728b4-153">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="728b4-153">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="728b4-154">c.</span><span class="sxs-lookup"><span data-stu-id="728b4-154">c.</span></span> <span data-ttu-id="728b4-155">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="728b4-155">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="728b4-156">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="728b4-156">d.</span></span> <span data-ttu-id="728b4-157">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="728b4-157">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="728b4-158">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="728b4-158">e.</span></span> <span data-ttu-id="728b4-159">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="728b4-159">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="728b4-160">f.</span><span class="sxs-lookup"><span data-stu-id="728b4-160">f.</span></span> <span data-ttu-id="728b4-161">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="728b4-161">Save this information in Notepad.</span></span> <span data-ttu-id="728b4-162">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="728b4-162">You will need this information in later steps.</span></span>

<span data-ttu-id="728b4-163">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="728b4-163">***Not running Windows on your PC?***</span></span> <span data-ttu-id="728b4-164">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="728b4-164">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Step_3"></a>
# <a name="step-3-build-and-validate-the-sample-using-java-client-libraries"></a><span data-ttu-id="728b4-165">步骤 3：使用 Java 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="728b4-165">Step 3: Build and Validate the sample using Java client libraries</span></span>

<span data-ttu-id="728b4-166">本部分逐步讲解如何在运行 Windows 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="728b4-166">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Windows operating system.</span></span> <span data-ttu-id="728b4-167">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="728b4-167">You will install the necessary prerequisites on your device.</span></span> <span data-ttu-id="728b4-168">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="728b4-168">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1"></a>
## <a name="31-install-azure-iot-device-sdk-and-prerequisites-on-device"></a><span data-ttu-id="728b4-169">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="728b4-169">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>

-   <span data-ttu-id="728b4-170">运行 SDK 需要 Java SE 1.8。</span><span class="sxs-lookup"><span data-stu-id="728b4-170">To run the SDK you will need Java SE 1.8.</span></span>

-   <span data-ttu-id="728b4-171">在设备上使用命令行安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="728b4-171">Install the prerequisite packages using command line on the device.</span></span>

<a name="Step_3_1_1"></a>
### <a name="311--install-java-jdk-18-and-set-up-environment-variables"></a><span data-ttu-id="728b4-172">3.1.1 安装 Java JDK 1.8 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="728b4-172">3.1.1  Install Java JDK 1.8 and set up environment variables</span></span>
        
1.  <span data-ttu-id="728b4-173">有关下载和安装说明，请访问：<http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></span><span class="sxs-lookup"><span data-stu-id="728b4-173">For downloads and installation instructions go here: <http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html></span></span>
       
2.  <span data-ttu-id="728b4-174">请确保 `PATH` 环境变量包含 jdk1.8.x\bin 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="728b4-174">Please make sure that the `PATH` environment variable includes the full path to the jdk1.8.x\bin directory.</span></span> <span data-ttu-id="728b4-175">（示例：c:\Program Files\Java\jdk1.8.0_65）</span><span class="sxs-lookup"><span data-stu-id="728b4-175">(Example: c:\Program Files\Java\jdk1.8.0_65)</span></span>
        
3.  <span data-ttu-id="728b4-176">请确保 `JAVA_HOME` 环境变量包含 jdk1.8.x 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="728b4-176">Please make sure that the `JAVA_HOME` environment variable includes the full path to the jdk1.8.x directory.</span></span> <span data-ttu-id="728b4-177">（示例：JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65）</span><span class="sxs-lookup"><span data-stu-id="728b4-177">(Example: JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65)</span></span>

4.  <span data-ttu-id="728b4-178">可以通过重新启动控制台并运行 `java -version`，来测试是否已正确设置 PATH 变量。</span><span class="sxs-lookup"><span data-stu-id="728b4-178">You can test whether your PATH variable is set correctly by restarting your console and running `java -version`.</span></span>

<a name="Step_3_1_2"></a>
### <a name="312--install-maven-and-set-up-environment-variables"></a><span data-ttu-id="728b4-179">3.1.2 安装 Maven 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="728b4-179">3.1.2  Install Maven and set up environment variables</span></span>
<span data-ttu-id="728b4-180">建议使用 Maven 3 安装用于 Java 的 Azure IoT 设备 SDK。</span><span class="sxs-lookup"><span data-stu-id="728b4-180">Using Maven 3 is the recommended way to install Azure IoT device SDK for Java.</span></span>

1.  <span data-ttu-id="728b4-181">有关 Maven 3 的下载和安装说明，请访问：<https://maven.apache.org/download.cgi></span><span class="sxs-lookup"><span data-stu-id="728b4-181">For downloads and installation instructions for maven 3 go here: <https://maven.apache.org/download.cgi></span></span>

2.  <span data-ttu-id="728b4-182">请确保 PATH 环境变量包含 apache-maven-3.x.x\bin 目录的完整路径。</span><span class="sxs-lookup"><span data-stu-id="728b4-182">Please make sure that the PATH environment variable includes the full path to the apache-maven-3.x.x\bin directory.</span></span> <span data-ttu-id="728b4-183">（示例：F:\Setups\apache-maven-3.3.3\bin）。</span><span class="sxs-lookup"><span data-stu-id="728b4-183">(Example: F:\Setups\apache-maven-3.3.3\bin).</span></span> <span data-ttu-id="728b4-184">Apache maven 3.x.x 目录是 Maven 3 的安装位置。</span><span class="sxs-lookup"><span data-stu-id="728b4-184">The apache-maven-3.x.x directory is where Maven 3 is installed.</span></span>

2.  <span data-ttu-id="728b4-185">可以通过重新启动控制台并运行 `mvn --version.`，来验证是否已正确设置用于运行 Maven 3 的环境变量</span><span class="sxs-lookup"><span data-stu-id="728b4-185">You can verify that the environment variables necessary to run Maven 3 have been set correctly by restarting your console and running `mvn --version.`</span></span>
  
<a name="Step_3_1_3"></a>
### <a name="313--install-git"></a><span data-ttu-id="728b4-186">3.1.3 安装 GIT</span><span class="sxs-lookup"><span data-stu-id="728b4-186">3.1.3  Install GIT</span></span>

-   <span data-ttu-id="728b4-187">有关下载和安装说明，请访问：<http://git-scm.com/book/en/v2/Getting-Started-Installing-Git></span><span class="sxs-lookup"><span data-stu-id="728b4-187">For downloads and installation instructions go here: <http://git-scm.com/book/en/v2/Getting-Started-Installing-Git></span></span>

<a name="Step_3_1_4"></a>
### <a name="314--build-qpid-jms"></a><span data-ttu-id="728b4-188">3.1.4 生成 Qpid JMS</span><span class="sxs-lookup"><span data-stu-id="728b4-188">3.1.4  Build Qpid JMS</span></span>

1.  <span data-ttu-id="728b4-189">将 Qpid JMS 的存储库克隆到本地目录。</span><span class="sxs-lookup"><span data-stu-id="728b4-189">Clone the repository for Qpid JMS to your local directory.</span></span>
    
        git clone https://github.com/avranju/qpid-jms.git

2.  <span data-ttu-id="728b4-190">按顺序执行以下命令以安装 Qpid JMS：</span><span class="sxs-lookup"><span data-stu-id="728b4-190">Install Qpid JMS by executing following commands in sequence:</span></span>

        cd qpid-jms
        mvn install
        cd ..

    <span data-ttu-id="728b4-191">***注意：****我们发现，如果使用最新版本的 JDK 8（编写本文档时，最新版本为 1.8.0_65），在运行上述 `mvn install` 时，某些单元测试可能会失败。但是，在较低的版本中可以正常运行。如果发生这种情况，请使用以下命令跳过运行单元测试：*</span><span class="sxs-lookup"><span data-stu-id="728b4-191">***Note:*** *We have noticed that certain unit tests can fail when running  `mvn install` as given above with the latest version of JDK 8 (1.8.0_65 at the time this document was written). It works fine with older versions however. If this occurs please skip running unit tests using following command:*</span></span>
    
        mvn install -DskipTests

<a name="Step_3_1_5"></a>
### <a name="315-build-the-azure-iot-device-sdk-for-java"></a><span data-ttu-id="728b4-192">3.1.5 生成适用于 Java 的 Azure IoT 设备 SDK</span><span class="sxs-lookup"><span data-stu-id="728b4-192">3.1.5 Build the Azure IoT Device SDK for Java</span></span>

1.  <span data-ttu-id="728b4-193">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="728b4-193">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-java.git

2.  <span data-ttu-id="728b4-194">验证 **azure-iot-sdk-java** 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="728b4-194">Verify that you now have a copy of the source code under the directory **azure-iot-sdk-java**.</span></span>

3.  <span data-ttu-id="728b4-195">在设备上按顺序运行以下命令，生成 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="728b4-195">Run the following commands on device in sequence to build Azure IoT SDK.</span></span>

        cd azure-iot-sdk-java/device
        mvn install

4.  <span data-ttu-id="728b4-196">上述命令将生成包含所有依赖项的已编译 JAR 文件。</span><span class="sxs-lookup"><span data-stu-id="728b4-196">Above command will generate the compiled JAR files with all dependencies.</span></span> <span data-ttu-id="728b4-197">可在以下位置找到此捆绑包：</span><span class="sxs-lookup"><span data-stu-id="728b4-197">This bundle can be found at:</span></span>

        azure-iot-sdk-java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"></a>
## <a name="32-run-and-validate-the-samples"></a><span data-ttu-id="728b4-198">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="728b4-198">3.2 Run and Validate the Samples</span></span>

<span data-ttu-id="728b4-199">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="728b4-199">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="728b4-200">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="728b4-200">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="728b4-201">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="728b4-201">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="728b4-202">***注意：****请为本部分中执行的所有操作创建屏幕截图。[步骤 4](#Step_4_2) 中需要用到这些屏幕截图。*</span><span class="sxs-lookup"><span data-stu-id="728b4-202">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2).*</span></span>

<a name="Step_3_2_1"></a>
### <a name="321-send-device-events-to-iot-hub"></a><span data-ttu-id="728b4-203">3.2.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="728b4-203">3.2.1 Send Device Events to IoT Hub:</span></span>

1.  <span data-ttu-id="728b4-204">如[步骤 2](#Step_2) 中所述启动 DeviceExplorer，然后导航到“数据”选项卡。</span><span class="sxs-lookup"><span data-stu-id="728b4-204">Launch the DeviceExplorer as explained in [Step 2](#Step_2) and navigate to **Data** tab.</span></span> <span data-ttu-id="728b4-205">从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="728b4-205">Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_Monitor](images/3_3_1_01.png)

2.  <span data-ttu-id="728b4-207">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="728b4-207">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="728b4-208">导航到包含发送事件示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="728b4-208">Navigate to the folder containing the executable JAR file for send event sample.</span></span>

        cd /azure-iot-sdk-java/device/samples/send-event/target

4.  <span data-ttu-id="728b4-209">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="728b4-209">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="728b4-210">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-210">**If using AMQP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps"
    
    <span data-ttu-id="728b4-211">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-211">**If using HTTP protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "https"

    <span data-ttu-id="728b4-212">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-212">**If using MQTT protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "mqtt"
    
    <span data-ttu-id="728b4-213">**如果使用 AMQP-WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-213">**If using AMQP-WebSocket protocol:**</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps_ws"    

    <span data-ttu-id="728b4-214">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="728b4-214">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="728b4-215">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="728b4-215">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="728b4-216">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="728b4-216">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="728b4-217">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="728b4-217">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

5.  <span data-ttu-id="728b4-218">检查确认消息中是否显示“正常”。</span><span class="sxs-lookup"><span data-stu-id="728b4-218">Verify that the confirmation messages show an OK.</span></span> <span data-ttu-id="728b4-219">如果没有，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="728b4-219">If not, then you may have incorrectly copied the device hub connection information.</span></span>

    <span data-ttu-id="728b4-220">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-220">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="728b4-221">![Terminal\_AMQP\_send\_event](images/terminal_amqp_send_event.PNG)</span><span class="sxs-lookup"><span data-stu-id="728b4-221">![Terminal\_AMQP\_send\_event](images/terminal_amqp_send_event.PNG)</span></span>

    <span data-ttu-id="728b4-222">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-222">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="728b4-223">![Terminal\_HTTP\_send\_event](images/terminal_http_send_event.PNG)</span><span class="sxs-lookup"><span data-stu-id="728b4-223">![Terminal\_HTTP\_send\_event](images/terminal_http_send_event.PNG)</span></span>

    <span data-ttu-id="728b4-224">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-224">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="728b4-225">![Terminal\_MQTT\_send\_event](images/terminal_mqtt_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="728b4-225">![Terminal\_MQTT\_send\_event](images/terminal_mqtt_send_event.png)</span></span>

    <span data-ttu-id="728b4-226">**如果使用 AMQP WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-226">**If using AMQP WebSocket protocol:**</span></span>  
    <span data-ttu-id="728b4-227">![Terminal\_AMQP_WS\_send\_event](images/terminal_amqps_ws_send_event.png)</span><span class="sxs-lookup"><span data-stu-id="728b4-227">![Terminal\_AMQP_WS\_send\_event](images/terminal_amqps_ws_send_event.png)</span></span>

6.  <span data-ttu-id="728b4-228">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="728b4-228">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    <span data-ttu-id="728b4-229">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-229">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="728b4-230">![DeviceExplorer\_AMQP\_message\_received](images/device_explorer_amqp_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="728b4-230">![DeviceExplorer\_AMQP\_message\_received](images/device_explorer_amqp_message_received.PNG)</span></span>

    <span data-ttu-id="728b4-231">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-231">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="728b4-232">![DeviceExplorer\_HTTP\_message\_received](images/device_explorer_http_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="728b4-232">![DeviceExplorer\_HTTP\_message\_received](images/device_explorer_http_message_received.PNG)</span></span>

    <span data-ttu-id="728b4-233">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-233">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="728b4-234">![DeviceExplorer\_MQTT\_message\_received](images/device_explorer_mqtt_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="728b4-234">![DeviceExplorer\_MQTT\_message\_received](images/device_explorer_mqtt_message_received.png)</span></span>

    <span data-ttu-id="728b4-235">**如果使用 AMQP WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-235">**If using AMQP WebSocket protocol:**</span></span>  
    <span data-ttu-id="728b4-236">![DeviceExplorer\_AMQP_WS\_message\_received](images/device_explorer_amqp_ws_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="728b4-236">![DeviceExplorer\_AMQP_WS\_message\_received](images/device_explorer_amqp_ws_message_received.png)</span></span>

<a name="Step_3_2_2"></a>
### <a name="322-receive-messages-from-iot-hub"></a><span data-ttu-id="728b4-237">3.2.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="728b4-237">3.2.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="728b4-238">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="728b4-238">To verify that you can send messages from the IoT Hub to your device, go to the **Messages To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="728b4-239">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="728b4-239">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="728b4-240">在“消息”字段中添加一些文本，然后单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="728b4-240">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_message\_send](images/device_explorer_message_send.png)

4.  <span data-ttu-id="728b4-242">导航到包含接收消息示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="728b4-242">Navigate to the folder containing the executable JAR file for the receive message sample.</span></span>

        cd /azure-iot-sdk-java/device/samples/handle-messages/target
     
5.  <span data-ttu-id="728b4-243">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="728b4-243">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="728b4-244">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-244">**If using AMQP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps"
    
    <span data-ttu-id="728b4-245">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-245">**If using HTTP protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "https"

    <span data-ttu-id="728b4-246">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-246">**If using MQTT protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "mqtt"

    <span data-ttu-id="728b4-247">**如果使用 AMQP-WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-247">**If using AMQP-WebSocket protocol:**</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps_ws"

    <span data-ttu-id="728b4-248">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="728b4-248">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="728b4-249">`{version}`：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="728b4-249">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="728b4-250">`{connection string}`：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="728b4-250">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="728b4-251">`{number of requests to send}`：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="728b4-251">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

6.  <span data-ttu-id="728b4-252">应会在客户端示例的控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="728b4-252">You should be able to see the command received in the console window for the client sample.</span></span>

    <span data-ttu-id="728b4-253">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-253">**If using AMQP protocol:**</span></span>  
    <span data-ttu-id="728b4-254">![Terminal\_AMQP\_message\_received](images/terminal_amqp_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="728b4-254">![Terminal\_AMQP\_message\_received](images/terminal_amqp_message_received.PNG)</span></span>

    <span data-ttu-id="728b4-255">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-255">**If using HTTP protocol:**</span></span>  
    <span data-ttu-id="728b4-256">![Terminal\_HTTP\_message\_received](images/terminal_http_message_received.PNG)</span><span class="sxs-lookup"><span data-stu-id="728b4-256">![Terminal\_HTTP\_message\_received](images/terminal_http_message_received.PNG)</span></span>

    <span data-ttu-id="728b4-257">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-257">**If using MQTT protocol:**</span></span>  
    <span data-ttu-id="728b4-258">![Terminal\_MQTT\_message\_received](images/terminal_mqtt_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="728b4-258">![Terminal\_MQTT\_message\_received](images/terminal_mqtt_message_received.png)</span></span>

    <span data-ttu-id="728b4-259">**如果使用 AMQP WebSocket 协议：**</span><span class="sxs-lookup"><span data-stu-id="728b4-259">**If using AMQP WebSocket protocol:**</span></span>  
    <span data-ttu-id="728b4-260">![Terminal\_AMQP_WS\_message\_received](images/terminal_amqp_ws_message_received.png)</span><span class="sxs-lookup"><span data-stu-id="728b4-260">![Terminal\_AMQP_WS\_message\_received](images/terminal_amqp_ws_message_received.png)</span></span>

<a name="Step_4"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="728b4-261">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="728b4-261">Step 4: Package and Share</span></span>

<a name="Step_4_1"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="728b4-262">4.1 打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="728b4-262">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="728b4-263">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="728b4-263">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="728b4-264">执行步骤 3.1.4 和 3.1.5 过程中在日志文件记录的生成日志和测试结果。</span><span class="sxs-lookup"><span data-stu-id="728b4-264">Build logs and test results that were logged in the log files during steps 3.1.4 and 3.1.5.</span></span>

2.  <span data-ttu-id="728b4-265">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="728b4-265">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="728b4-266">前面“**从 IoT 中心接收消息**”部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="728b4-266">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="728b4-267">向我们发送明确的说明，告知如何在硬件上运行此示例（具体强调客户所要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="728b4-267">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="728b4-268">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-java.md>)提供的模板创建特定于设备的说明。</span><span class="sxs-lookup"><span data-stu-id="728b4-268">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-java.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="728b4-269">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="728b4-269">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2"></a>
## <a name="42-share-with-the-azure-iot-certification-team"></a><span data-ttu-id="728b4-270">4.2 与 Azure IoT 认证团队共享</span><span class="sxs-lookup"><span data-stu-id="728b4-270">4.2 Share with the Azure IoT Certification team</span></span>

1.  <span data-ttu-id="728b4-271">转到“合作伙伴仪表板”。[](<https://catalog.azureiotsuite.com/devices>)</span><span class="sxs-lookup"><span data-stu-id="728b4-271">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="728b4-272">单击设备右上角的“上载”图标。</span><span class="sxs-lookup"><span data-stu-id="728b4-272">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="728b4-274">此时将打开上载对话框。</span><span class="sxs-lookup"><span data-stu-id="728b4-274">This will open an upload dialog.</span></span> <span data-ttu-id="728b4-275">单击“上载”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="728b4-275">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="728b4-277">可以上载同一个设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="728b4-277">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="728b4-278">上载所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="728b4-278">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="728b4-279">***注意：****提交文件供审查后，若要更改/删除文件，请与 iotcert 团队联系。*</span><span class="sxs-lookup"><span data-stu-id="728b4-279">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3"></a>
## <a name="43-next-steps"></a><span data-ttu-id="728b4-280">4.3 后续步骤</span><span class="sxs-lookup"><span data-stu-id="728b4-280">4.3 Next steps</span></span>

<span data-ttu-id="728b4-281">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="728b4-281">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="728b4-282">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="728b4-282">Step 5: Troubleshooting</span></span>

<span data-ttu-id="728b4-283">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="728b4-283">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
