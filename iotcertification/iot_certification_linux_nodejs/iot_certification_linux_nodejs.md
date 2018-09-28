<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a><span data-ttu-id="3dd7e-101">如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="3dd7e-101">How to certify IoT devices running Linux with Azure IoT SDK</span></span>
===
---


# <a name="table-of-contents"></a><span data-ttu-id="3dd7e-102">目录</span><span class="sxs-lookup"><span data-stu-id="3dd7e-102">Table of Contents</span></span>

-   [<span data-ttu-id="3dd7e-103">介绍</span><span class="sxs-lookup"><span data-stu-id="3dd7e-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="3dd7e-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="3dd7e-104">Step 1: Configure Azure IoT Hub</span></span>](#Configure)
-   [<span data-ttu-id="3dd7e-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="3dd7e-105">Step 2: Register Device</span></span>](#Register)
-   [<span data-ttu-id="3dd7e-106">步骤 3：使用 Node JS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="3dd7e-106">Step 3: Build and validate the sample using Node JS client libraries</span></span>](#Build)
    -   [<span data-ttu-id="3dd7e-107">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="3dd7e-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Load)
    -   [<span data-ttu-id="3dd7e-108">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="3dd7e-108">3.2 Build the samples</span></span>](#BuildSamples)
    -   [<span data-ttu-id="3dd7e-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="3dd7e-109">3.3 Run and Validate the Samples</span></span>](#Run)
-   [<span data-ttu-id="3dd7e-110">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="3dd7e-110">Step 4: Package and Share</span></span>](#PackageShare)
    -   [<span data-ttu-id="3dd7e-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="3dd7e-111">4.1 Package build logs and sample test results</span></span>](#Package)
    -   [<span data-ttu-id="3dd7e-112">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="3dd7e-112">4.2 Share package with Engineering Support</span></span>](#Share)
    -   [<span data-ttu-id="3dd7e-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="3dd7e-113">4.3 Next steps</span></span>](#Next)
-   [<span data-ttu-id="3dd7e-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="3dd7e-114">Step 5: Troubleshooting</span></span>](#Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="3dd7e-115">介绍</span><span class="sxs-lookup"><span data-stu-id="3dd7e-115">Introduction</span></span>

<span data-ttu-id="3dd7e-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-116">**About this document**</span></span>

<span data-ttu-id="3dd7e-117">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="3dd7e-118">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-118">This multi-step process includes:</span></span>

-   <span data-ttu-id="3dd7e-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="3dd7e-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="3dd7e-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="3dd7e-120">Registering your IoT device</span></span>
-   <span data-ttu-id="3dd7e-121">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="3dd7e-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="3dd7e-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="3dd7e-122">Packaging and sharing the logs</span></span>


<span data-ttu-id="3dd7e-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-123">**Prepare**</span></span>

<span data-ttu-id="3dd7e-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span> <span data-ttu-id="3dd7e-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="3dd7e-126">准备好一台装有 GitHub 并且可以访问 [azure-iot-sdk-node](https://github.com/Azure/azure-iot-sdk-node) GitHub 专用存储库的计算机</span><span class="sxs-lookup"><span data-stu-id="3dd7e-126">Computer with GitHub installed and access to the [azure-iot-sdk-node](https://github.com/Azure/azure-iot-sdk-node) GitHub private repository</span></span>
-   <span data-ttu-id="3dd7e-127">配置 SSH 客户端（如 [PuTTY](http://www.putty.org/)），以便能够访问命令行</span><span class="sxs-lookup"><span data-stu-id="3dd7e-127">SSH client, such as [PuTTY](http://www.putty.org/), so you can access the command line</span></span>
-   <span data-ttu-id="3dd7e-128">用于认证的所需硬件</span><span class="sxs-lookup"><span data-stu-id="3dd7e-128">Required hardware to certify</span></span>

<span data-ttu-id="3dd7e-129">\*\**注意：\*\*\*\*如果你尚未咨询 Microsoft 如何成为 Azure 认证的 IoT 合作伙伴，请先提交此[表单](<https://iotcert.cloudapp.net/>)来提出请求，然后遵照本文中的说明。*</span><span class="sxs-lookup"><span data-stu-id="3dd7e-129">***Note:*** *If you haven’t contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://iotcert.cloudapp.net/>) first to request it and then follow these instructions.*</span></span>

<a name="Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="3dd7e-130">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="3dd7e-130">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="3dd7e-131">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-131">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="3dd7e-132">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-132">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="3dd7e-133">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-133">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

          HostName=[YourIoTHubName];CredentialType=SharedAccessSignature;CredentialScope=[ContosoIotHub];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="3dd7e-134">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="3dd7e-134">Step 2: Register Device</span></span>

<span data-ttu-id="3dd7e-135">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-135">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="3dd7e-136">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-136">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="3dd7e-137">设备管理</span><span class="sxs-lookup"><span data-stu-id="3dd7e-137">Device management</span></span>
    -   <span data-ttu-id="3dd7e-138">创建新设备</span><span class="sxs-lookup"><span data-stu-id="3dd7e-138">Create new devices</span></span>
    -   <span data-ttu-id="3dd7e-139">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="3dd7e-139">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="3dd7e-140">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="3dd7e-140">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="3dd7e-141">可删除设备</span><span class="sxs-lookup"><span data-stu-id="3dd7e-141">Provides ability to delete a device</span></span>
-   <span data-ttu-id="3dd7e-142">监视设备的事件。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-142">Monitoring events from your device.</span></span>
-   <span data-ttu-id="3dd7e-143">向设备发送消息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-143">Sending messages to your device.</span></span>

<span data-ttu-id="3dd7e-144">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Configure) 中所述使用配置字符串：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-144">To run DeviceExplorer tool, follow the configuration strings as described in  [Step1](#Configure):</span></span>

-   <span data-ttu-id="3dd7e-145">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="3dd7e-145">IoT Hub Connection String</span></span>

<span data-ttu-id="3dd7e-146">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-146">**Steps:**</span></span>
1.   <span data-ttu-id="3dd7e-147">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-147">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="3dd7e-148">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-148">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="3dd7e-149">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-149">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="3dd7e-150">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-150">a.</span></span> <span data-ttu-id="3dd7e-151">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-151">Click the **Management** tab.</span></span>

    <span data-ttu-id="3dd7e-152">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-152">b.</span></span> <span data-ttu-id="3dd7e-153">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-153">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="3dd7e-154">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-154">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="3dd7e-155">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-155">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="3dd7e-156">c.</span><span class="sxs-lookup"><span data-stu-id="3dd7e-156">c.</span></span> <span data-ttu-id="3dd7e-157">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-157">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="3dd7e-158">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-158">d.</span></span> <span data-ttu-id="3dd7e-159">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-159">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="3dd7e-160">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-160">e.</span></span> <span data-ttu-id="3dd7e-161">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-161">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="3dd7e-162">f.</span><span class="sxs-lookup"><span data-stu-id="3dd7e-162">f.</span></span> <span data-ttu-id="3dd7e-163">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-163">Save this information in Notepad.</span></span> <span data-ttu-id="3dd7e-164">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-164">You will need this information in later steps.</span></span>

<span data-ttu-id="3dd7e-165">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="3dd7e-165">***Not running Windows on your PC?***</span></span> <span data-ttu-id="3dd7e-166">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-166">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-node-js-client-libraries"></a><span data-ttu-id="3dd7e-167">步骤 3：使用 Node JS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="3dd7e-167">Step 3: Build and validate the sample using Node JS client libraries</span></span>

<span data-ttu-id="3dd7e-168">本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-168">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Linux operating system.</span></span> <span data-ttu-id="3dd7e-169">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-169">You will install necessary prerequisites on your device.</span></span>  <span data-ttu-id="3dd7e-170">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-170">Once done,  you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="3dd7e-171">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="3dd7e-171">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="3dd7e-172">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-172">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="3dd7e-173">在后续步骤中根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-173">Choose your commands in next steps based on the OS running on your device.</span></span>

-   <span data-ttu-id="3dd7e-174">运行以下命令检查是否已安装 NodeJS</span><span class="sxs-lookup"><span data-stu-id="3dd7e-174">Run following command to check if NodeJS is already installed</span></span>

        node --version

    <span data-ttu-id="3dd7e-175">如果版本为 **0.12.x 或更高**，可跳过有关安装必备组件包的后续步骤。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-175">If version is **0.12.x or greater**, then skip next step of installing prerequisite packages.</span></span> <span data-ttu-id="3dd7e-176">否则，请在设备上的命令行中发出以下命令来卸载该版本。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-176">Else uninstall it by issuing following command from command line on the device.</span></span>

    <span data-ttu-id="3dd7e-177">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-177">**Debian or Ubuntu**</span></span>

        sudo apt-get remove nodejs

    <span data-ttu-id="3dd7e-178">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-178">**Fedora**</span></span>

        sudo dnf remove nodejs

    <span data-ttu-id="3dd7e-179">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-179">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

-   <span data-ttu-id="3dd7e-180">在设备上的命令行中发出以下命令，安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-180">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span> <span data-ttu-id="3dd7e-181">根据设备上运行的 OS 选择命令。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-181">Choose your commands based on the OS running on your device.</span></span>

    <span data-ttu-id="3dd7e-182">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-182">**Debian or Ubuntu**</span></span>

        curl -sL https://deb.nodesource.com/setup_4.x | sudo bash -

        sudo apt-get install -y nodejs

    <span data-ttu-id="3dd7e-183">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-183">**Fedora**</span></span>

        wget http://nodejs.org/dist/v4.2.1/node-v4.2.1-linux-x64.tar.gz

        tar xvf node-v4.2.1-linux-x64.tar.gz

        sudo mv node-v4.2.1-linux-x64 /opt

        echo "export PATH=\$PATH:/opt/node-v4.2.1-linux-x64/bin" >> ~/.bashrc

        source ~/.bashrc

    <span data-ttu-id="3dd7e-184">**其他任何 Linux OS**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-184">**Any Other Linux OS**</span></span>

        Use equivalent commands on the target OS

    <span data-ttu-id="3dd7e-185">**注意：** 若要测试 Node JS 是否成功安装，请尝试运行以下命令获取其版本信息：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-185">**Note:** To test successful installation of Node JS, try to fetch its version information by running following command:</span></span>

        node --version

-   <span data-ttu-id="3dd7e-186">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-186">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone --recursive https://github.com/Azure/azure-iot-sdk-node.git

-   <span data-ttu-id="3dd7e-187">验证 ~/azure-iot-sdk-node 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-187">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-node.</span></span>

<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="3dd7e-188">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="3dd7e-188">3.2 Build the samples</span></span>

-   <span data-ttu-id="3dd7e-189">若要验证源代码，请在设备上运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-189">To validate the source code run the following commands on the device.</span></span>

        export IOTHUB_CONNECTION_STRING='<iothub_connection_string>'

    <span data-ttu-id="3dd7e-190">将 `<iothub_connection_string>` 占位符替换为在[步骤 1](#Configure) 中获取的 IoT 中心连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-190">Replace the `<iothub_connection_string>` placeholder with IoTHub Connection String you got in [Step 1](#Configure).</span></span>    

-   <span data-ttu-id="3dd7e-191">运行以下命令</span><span class="sxs-lookup"><span data-stu-id="3dd7e-191">Run the following commands</span></span> 

        cd ~/azure-iot-sdk-node
        build/dev-setup.sh
        build/build.sh | tee LogFile.txt

    <span data-ttu-id="3dd7e-192">\*\**注意：\*\*\*\*应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。*</span><span class="sxs-lookup"><span data-stu-id="3dd7e-192">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>

-   <span data-ttu-id="3dd7e-193">安装 npm 包以运行示例。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-193">Install npm package to run sample.</span></span>

        cd ~/azure-iot-sdk-node/device/samples

    <span data-ttu-id="3dd7e-194">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-194">**For AMQP Protocol:**</span></span>
    
        npm install azure-iot-device-amqp
    
    <span data-ttu-id="3dd7e-195">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-195">**For HTTP Protocol:**</span></span>
    
        npm install azure-iot-device-http
    
    <span data-ttu-id="3dd7e-196">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-196">**For MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt   

    <span data-ttu-id="3dd7e-197">**对于将 Web Socket 与 AMQP 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-197">**For Web Sockets with AMQP Protocol:**</span></span>

        npm install azure-iot-device-amqp

    <span data-ttu-id="3dd7e-198">**对于将 Web Socket 与 MQTT 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-198">**For Web Sockets with MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt

-   <span data-ttu-id="3dd7e-199">若要更新示例，请在设备上运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-199">To update sample, run the following command on device.</span></span>

        cd ~/azure-iot-sdk-node/device/samples
        nano simple_sample_device.js

-   <span data-ttu-id="3dd7e-200">此时会启动基于控制台的文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-200">This launches a console-based text editor.</span></span> <span data-ttu-id="3dd7e-201">向下滚动到协议信息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-201">Scroll down to the protocol information.</span></span>
    
-   <span data-ttu-id="3dd7e-202">找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-202">Find the below code:</span></span>

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    <span data-ttu-id="3dd7e-203">使用的默认协议为 AMQP。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-203">The default protocol used is AMQP.</span></span> <span data-ttu-id="3dd7e-204">脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-204">Code for other protocols(HTTP/MQTT) are mentioned just below the above line in the script.</span></span>
    <span data-ttu-id="3dd7e-205">请根据想要使用的协议取消注释相应的代码行。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-205">Uncomment the line as per the protocol you want to use.</span></span>


-   <span data-ttu-id="3dd7e-206">向下滚动到连接信息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-206">Scroll down to the connection information.</span></span>
    <span data-ttu-id="3dd7e-207">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-207">Find the following place holder for IoT connection string:</span></span>

        var connectionString = "[IoT Device Connection String]";

-   <span data-ttu-id="3dd7e-208">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-208">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="3dd7e-209">可根据[步骤 2](#Register) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-209">You can get this from DeviceExplorer as explained in [Step 2](#Register), that you copied into Notepad.</span></span>

-   <span data-ttu-id="3dd7e-210">按 Ctrl+O 保存更改，当 nano 提示是否保存到同一文件时，按 ENTER 即可。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-210">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

-   <span data-ttu-id="3dd7e-211">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-211">Press Ctrl+X to exit nano.</span></span>

-   <span data-ttu-id="3dd7e-212">在退出 **~/azure-iot-sdk-node/device/samples** 目录之前运行以下命令</span><span class="sxs-lookup"><span data-stu-id="3dd7e-212">Run the following command before leaving the **~/azure-iot-sdk-node/device/samples** directory</span></span>

        npm link azure-iot-device

<a name="Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="3dd7e-213">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="3dd7e-213">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="3dd7e-214">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心服务之间的通信。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-214">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub service.</span></span> <span data-ttu-id="3dd7e-215">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-215">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="3dd7e-216">此外，还要监视从 Azure IoT 中心发送到客户端的所有消息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-216">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="3dd7e-217">**注意：** 请针对以下部分中执行的所有操作创建屏幕截图，如示例屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-217">**Note:** Take screen shots of all operations, like sample screen shots, performed in below sections.</span></span> <span data-ttu-id="3dd7e-218">[步骤 4](#Share) 中需要用到这些屏幕截图</span><span class="sxs-lookup"><span data-stu-id="3dd7e-218">These will be needed in [Step 4](#Share)</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="3dd7e-219">3.3.1：向 IOT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-219">3.3.1 Send Device Events to IOT Hub:</span></span>

1.  <span data-ttu-id="3dd7e-220">如[步骤 2](#Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-220">Launch the DeviceExplorer as explained in [Step 2](#Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs, click **Monitor** button.</span></span>

    ![DeviceExplorer_Monitor](images/3_3_1_01.png)

2.  <span data-ttu-id="3dd7e-222">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-222">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="3dd7e-223">发出以下命令运行该示例：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-223">Run the sample by issuing following command:</span></span>

        node ~/azure-iot-sdk-node/device/samples/simple_sample_device.js

4. <span data-ttu-id="3dd7e-224">检查是否已成功发送和接收数据。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-224">Verify that data has been successfully sent and received.</span></span> <span data-ttu-id="3dd7e-225">如果出现任何问题，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-225">If any, then you may have incorrectly copied the device hub connection information.</span></span>

   ![Simple_Sample_result_terminal](images/3_3_1_02.png)

5.  <span data-ttu-id="3dd7e-227">DeviceExplorer 应显示 IoT 中心已成功接收示例测试发送的数据。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-227">DeviceExplorer should show that IoT Hub has successfully received data sent by sample test.</span></span>

    ![Simple_Sample_result_DeviceExplorer](images/3_3_1_03.png)


### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="3dd7e-229">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="3dd7e-229">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="3dd7e-230">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-230">To verify that you can send messages from the IoT Hub to your device, go to the **Message To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="3dd7e-231">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-231">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="3dd7e-232">在“消息”字段中添加一些文本，然后单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-232">Add some text to the Message field, then click Send button.</span></span>

    ![MessageSend_DeviceExplorer](images/3_3_2_01.png)

4.  <span data-ttu-id="3dd7e-234">应会在客户端示例的控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-234">You should be able to see the command received in the console window of the client sample.</span></span>

    ![MessageSend_terminal](images/3_3_2_02.png)

### <a name="333-verify-device-configuration"></a><span data-ttu-id="3dd7e-236">3.3.3 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="3dd7e-236">3.3.3 Verify Device configuration</span></span>

-   <span data-ttu-id="3dd7e-237">请通过执行以下命令安装 python。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-237">Please install python by following below command.</span></span>

    <span data-ttu-id="3dd7e-238">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-238">**Debian or Ubuntu**</span></span>

        sudo apt-get install python

    <span data-ttu-id="3dd7e-239">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-239">**Fedora**</span></span>

        sudo dnf install python

-    <span data-ttu-id="3dd7e-240">*此库还需要 Python 版本 2.7.x。* 可使用以下命令来验证环境中当前安装的版本：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-240">*This library also requires Python version 2.7.x. You can verify the current version installed in your environment using the following command:*</span></span>
    
          python --version

-   <span data-ttu-id="3dd7e-241">在运行 `platform_data.py` 之前，请安装以下模块</span><span class="sxs-lookup"><span data-stu-id="3dd7e-241">Please install the below modules before you run the `platform_data.py`</span></span>

    <span data-ttu-id="3dd7e-242">**Debian 或 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-242">**Debian or Ubuntu**</span></span> 

        sudo apt-get install python-requests
        sudo apt-get install python-netifaces

    <span data-ttu-id="3dd7e-243">**Fedora**</span><span class="sxs-lookup"><span data-stu-id="3dd7e-243">**Fedora**</span></span>

        sudo dnf install python-requests
        sudo dnf install python-netifaces

-   <span data-ttu-id="3dd7e-244">发出以下命令下载 SDK：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-244">Download the SDK by issuing following command:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-python.git

-   <span data-ttu-id="3dd7e-245">通过执行以下命令导航到 tools 文件夹：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-245">Navigate to tools folder by executing following command:</span></span>

        cd azure-iot-sdk-python/Tools

-   <span data-ttu-id="3dd7e-246">在设备上运行以下命令</span><span class="sxs-lookup"><span data-stu-id="3dd7e-246">Run the following command on the device</span></span>
        
        python platform_data.py

    ![deviceinfo\_screenshot](images/python_modified_output.PNG)

-   <span data-ttu-id="3dd7e-248">请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-248">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Package).</span></span>

<a name="PackageShare"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="3dd7e-249">步骤 4：打包和共享</span><span class="sxs-lookup"><span data-stu-id="3dd7e-249">Step 4: Package and Share</span></span>

<a name="Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="3dd7e-250">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="3dd7e-250">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="3dd7e-251">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="3dd7e-251">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="3dd7e-252">生成运行过程中在日志文件记录的生成日志和 E2E 测试结果。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-252">Build logs and E2E test results that were logged in the log file during build run.</span></span>

2.  <span data-ttu-id="3dd7e-253">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-253">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="3dd7e-254">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-254">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="3dd7e-255">前面“设备配置”部分中的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-255">All the screenshots that are above in "**Device Configuration**" section.</span></span>

5.  <span data-ttu-id="3dd7e-256">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-256">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="3dd7e-257">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-nodejs.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-257">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-nodejs.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="3dd7e-258">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-258">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Share"></a>
## <a name="42-share-package-with-engineering-support"></a><span data-ttu-id="3dd7e-259">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="3dd7e-259">4.2 Share package with Engineering Support</span></span>

1.  <span data-ttu-id="3dd7e-260">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-260">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="3dd7e-261">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-261">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="3dd7e-263">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-263">This will open an upload dialog.</span></span> <span data-ttu-id="3dd7e-264">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-264">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="3dd7e-266">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-266">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="3dd7e-267">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-267">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="3dd7e-268">***注意：*** 提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-268">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="3dd7e-269">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="3dd7e-269">4.3 Next steps</span></span>

<span data-ttu-id="3dd7e-270">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-270">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="3dd7e-271">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="3dd7e-271">Step 5: Troubleshooting</span></span>

<span data-ttu-id="3dd7e-272">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="3dd7e-272">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
