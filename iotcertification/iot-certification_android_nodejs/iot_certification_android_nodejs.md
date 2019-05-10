<a name="how-to-certify-iot-devices-running-linux-with-azure-iot-sdk"></a><span data-ttu-id="c40b0-101">如何使用 Azure IoT SDK 认证运行 Linux 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="c40b0-101">How to certify IoT devices running Linux with Azure IoT SDK</span></span>
===
---


# <a name="table-of-contents"></a><span data-ttu-id="c40b0-102">目录</span><span class="sxs-lookup"><span data-stu-id="c40b0-102">Table of Contents</span></span>

-   [<span data-ttu-id="c40b0-103">介绍</span><span class="sxs-lookup"><span data-stu-id="c40b0-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="c40b0-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c40b0-104">Step 1: Configure Azure IoT Hub</span></span>](#Configure)
-   [<span data-ttu-id="c40b0-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="c40b0-105">Step 2: Register Device</span></span>](#Register)
-   [<span data-ttu-id="c40b0-106">步骤 3：使用 Node JS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-106">Step 3: Build and validate the sample using Node JS client libraries</span></span>](#Build)
    -   [<span data-ttu-id="c40b0-107">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="c40b0-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Load)
    -   [<span data-ttu-id="c40b0-108">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-108">3.2 Build the samples</span></span>](#BuildSamples)
    -   [<span data-ttu-id="c40b0-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-109">3.3 Run and Validate the Samples</span></span>](#Run)
-   [<span data-ttu-id="c40b0-110">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="c40b0-110">Step 4: Package and Share</span></span>](#PackageShare)
    -   [<span data-ttu-id="c40b0-111">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="c40b0-111">4.1 Package build logs and sample test results</span></span>](#Package)
    -   [<span data-ttu-id="c40b0-112">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="c40b0-112">4.2 Share package with Engineering Support</span></span>](#Share)
    -   [<span data-ttu-id="c40b0-113">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="c40b0-113">4.3 Next steps</span></span>](#Next)
-   [<span data-ttu-id="c40b0-114">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="c40b0-114">Step 5: Troubleshooting</span></span>](#Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="c40b0-115">介绍</span><span class="sxs-lookup"><span data-stu-id="c40b0-115">Introduction</span></span>

<span data-ttu-id="c40b0-116">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="c40b0-116">**About this document**</span></span>

<span data-ttu-id="c40b0-117">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="c40b0-117">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="c40b0-118">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="c40b0-118">This multi-step process includes:</span></span>
-   <span data-ttu-id="c40b0-119">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c40b0-119">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="c40b0-120">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="c40b0-120">Registering your IoT device</span></span>
-   <span data-ttu-id="c40b0-121">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="c40b0-121">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="c40b0-122">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="c40b0-122">Packaging and sharing the logs</span></span>


<span data-ttu-id="c40b0-123">**准备**</span><span class="sxs-lookup"><span data-stu-id="c40b0-123">**Prepare**</span></span>

<span data-ttu-id="c40b0-124">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="c40b0-124">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span> <span data-ttu-id="c40b0-125">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="c40b0-125">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="c40b0-126">用于认证的所需硬件</span><span class="sxs-lookup"><span data-stu-id="c40b0-126">Required hardware to certify</span></span>

<span data-ttu-id="c40b0-127">\*\**注意：\*\*\*\*如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://iotcert.cloudapp.net/>)请求此身份，然后遵照本文中的说明操作。*</span><span class="sxs-lookup"><span data-stu-id="c40b0-127">***Note:*** *If you haven’t contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://iotcert.cloudapp.net/>) first to request it and then follow these instructions.*</span></span>

<a name="Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="c40b0-128">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="c40b0-128">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="c40b0-129">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="c40b0-129">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="c40b0-130">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c40b0-130">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="c40b0-131">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="c40b0-131">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

          HostName=[YourIoTHubName];CredentialType=SharedAccessSignature;CredentialScope=[ContosoIotHub];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="c40b0-132">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="c40b0-132">Step 2: Register Device</span></span>

<span data-ttu-id="c40b0-133">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="c40b0-133">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="c40b0-134">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="c40b0-134">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="c40b0-135">设备管理</span><span class="sxs-lookup"><span data-stu-id="c40b0-135">Device management</span></span>
    -   <span data-ttu-id="c40b0-136">创建新设备</span><span class="sxs-lookup"><span data-stu-id="c40b0-136">Create new devices</span></span>
    -   <span data-ttu-id="c40b0-137">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="c40b0-137">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="c40b0-138">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="c40b0-138">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="c40b0-139">可删除设备</span><span class="sxs-lookup"><span data-stu-id="c40b0-139">Provides ability to delete a device</span></span>
-   <span data-ttu-id="c40b0-140">监视设备的事件。</span><span class="sxs-lookup"><span data-stu-id="c40b0-140">Monitoring events from your device.</span></span>
-   <span data-ttu-id="c40b0-141">向设备发送消息。</span><span class="sxs-lookup"><span data-stu-id="c40b0-141">Sending messages to your device.</span></span>

<span data-ttu-id="c40b0-142">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Configure) 中所述使用配置字符串：</span><span class="sxs-lookup"><span data-stu-id="c40b0-142">To run DeviceExplorer tool, follow the configuration strings as described in  [Step1](#Configure):</span></span>

-   <span data-ttu-id="c40b0-143">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="c40b0-143">IoT Hub Connection String</span></span>

<span data-ttu-id="c40b0-144">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-144">**Steps:**</span></span>

1.   <span data-ttu-id="c40b0-145">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="c40b0-145">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="c40b0-146">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="c40b0-146">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="c40b0-147">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="c40b0-147">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="c40b0-148">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="c40b0-148">a.</span></span> <span data-ttu-id="c40b0-149">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="c40b0-149">Click the **Management** tab.</span></span>

    <span data-ttu-id="c40b0-150">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="c40b0-150">b.</span></span> <span data-ttu-id="c40b0-151">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="c40b0-151">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="c40b0-152">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="c40b0-152">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="c40b0-153">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="c40b0-153">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="c40b0-154">c.</span><span class="sxs-lookup"><span data-stu-id="c40b0-154">c.</span></span> <span data-ttu-id="c40b0-155">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="c40b0-155">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="c40b0-156">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="c40b0-156">d.</span></span> <span data-ttu-id="c40b0-157">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="c40b0-157">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="c40b0-158">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="c40b0-158">e.</span></span> <span data-ttu-id="c40b0-159">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="c40b0-159">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="c40b0-160">f.</span><span class="sxs-lookup"><span data-stu-id="c40b0-160">f.</span></span> <span data-ttu-id="c40b0-161">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="c40b0-161">Save this information in Notepad.</span></span> <span data-ttu-id="c40b0-162">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="c40b0-162">You will need this information in later steps.</span></span>

<span data-ttu-id="c40b0-163">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="c40b0-163">***Not running Windows on your PC?***</span></span> <span data-ttu-id="c40b0-164">- 请遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="c40b0-164">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-node-js-client-libraries"></a><span data-ttu-id="c40b0-165">步骤 3：使用 Node JS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-165">Step 3: Build and validate the sample using Node JS client libraries</span></span>

<span data-ttu-id="c40b0-166">本部分逐步讲解如何在运行 Linux 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="c40b0-166">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Linux operating system.</span></span> <span data-ttu-id="c40b0-167">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="c40b0-167">You will install necessary prerequisites on your device.</span></span>  <span data-ttu-id="c40b0-168">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="c40b0-168">Once done,  you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="c40b0-169">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="c40b0-169">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="c40b0-170">通过 Google Playstore 或访问 URL (**[https://termux.com/](https://termux.com/)**) 安装 **Termux** 应用</span><span class="sxs-lookup"><span data-stu-id="c40b0-170">Install **Termux** app from Google Playstore or visit the URL (**[https://termux.com/](https://termux.com/)**)</span></span>

-   <span data-ttu-id="c40b0-171">打开 Termux 应用。</span><span class="sxs-lookup"><span data-stu-id="c40b0-171">Open Termux app.</span></span>
-   <span data-ttu-id="c40b0-172">运行以下命令安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="c40b0-172">Install prerequisites by running following commands:</span></span>

        apt update
        apt upgrade
        apt install -y coreutils nano openssl-tool git nodejs

-   <span data-ttu-id="c40b0-173">检查是否已成功安装 NodeJS</span><span class="sxs-lookup"><span data-stu-id="c40b0-173">Check if NodeJS is successfully installed</span></span>

        node --version

-   <span data-ttu-id="c40b0-174">在 Termux 应用中发出以下命令，将 SDK 下载到开发板</span><span class="sxs-lookup"><span data-stu-id="c40b0-174">Download the SDK to the board by issuing the following command in Termux app</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-node.git

-   <span data-ttu-id="c40b0-175">验证 ~/azure-iot-sdk-node 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="c40b0-175">Verify that you now have a copy of the source code under the directory ~/azure-iot-sdk-node.</span></span>

<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="c40b0-176">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-176">3.2 Build the samples</span></span>

-   <span data-ttu-id="c40b0-177">设置 **IOTHUB\_CONNECTION\_STRING** 环境变量。</span><span class="sxs-lookup"><span data-stu-id="c40b0-177">Set the **IOTHUB\_CONNECTION\_STRING** environment variable.</span></span>

        export IOTHUB_CONNECTION_STRING='<IoT Hub Connection String>'

<span data-ttu-id="c40b0-178">将上述占位符替换为在[步骤 2](#Register) 中注册设备时使用的“IoT 中心连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="c40b0-178">Replace the above placeholder with "IoT Hub Connection String" which you used in  [Step 2](#Register) for device registration.</span></span>

-   <span data-ttu-id="c40b0-179">运行以下命令生成开发环境</span><span class="sxs-lookup"><span data-stu-id="c40b0-179">Run the below commands to build development environment</span></span>

        cd ~/azure-iot-sdk-node
        sh build/dev-setup.sh
        sh build/build.sh | tee LogFile.txt

    <span data-ttu-id="c40b0-180">***注意：*** 应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。</span><span class="sxs-lookup"><span data-stu-id="c40b0-180">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>

-   <span data-ttu-id="c40b0-181">转到示例。</span><span class="sxs-lookup"><span data-stu-id="c40b0-181">Go to samples.</span></span>

    <span data-ttu-id="c40b0-182">cd ~/azure-iot-sdk-node/node/device/samples</span><span class="sxs-lookup"><span data-stu-id="c40b0-182">cd ~/azure-iot-sdk-node/node/device/samples</span></span>

-   <span data-ttu-id="c40b0-183">安装 npm 包以运行示例。</span><span class="sxs-lookup"><span data-stu-id="c40b0-183">Install npm package to run sample.</span></span>

    <span data-ttu-id="c40b0-184">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-184">**For AMQP Protocol:**</span></span>
    
        npm install azure-iot-device-amqp
    
    <span data-ttu-id="c40b0-185">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-185">**For HTTP Protocol:**</span></span>
    
        npm install azure-iot-device-http
    
    <span data-ttu-id="c40b0-186">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-186">**For MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt

-   <span data-ttu-id="c40b0-187">运行以下命令更新示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-187">Run the below command to update sample</span></span>

        nano simple_sample_device.js

-   <span data-ttu-id="c40b0-188">此时会启动基于控制台的文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="c40b0-188">This launches a console-based text editor.</span></span> <span data-ttu-id="c40b0-189">向下滚动到以下代码行所写入到的协议信息位置。</span><span class="sxs-lookup"><span data-stu-id="c40b0-189">Scroll down to the protocol information where following line is written.</span></span>

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
-   <span data-ttu-id="c40b0-190">如果使用的协议不是 amqp，请替换上述代码行。</span><span class="sxs-lookup"><span data-stu-id="c40b0-190">Replace the above line if using protocol other than amqp.</span></span>

    <span data-ttu-id="c40b0-191">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-191">**For HTTP Protocol:**</span></span>

        var Protocol = require('azure-iot-device-http').Http;

    <span data-ttu-id="c40b0-192">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-192">**For MQTT Protocol:**</span></span>

        var Protocol = require('azure-iot-device-mqtt').Mqtt;

-   <span data-ttu-id="c40b0-193">找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="c40b0-193">Find the following place holder for IoT connection string:</span></span>

        var connectionString = "[IoT Device Connection String]";

-   <span data-ttu-id="c40b0-194">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c40b0-194">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="c40b0-195">可根据[步骤 2](#Register) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c40b0-195">You can get this from DeviceExplorer as explained in [Step 2](#Register), that you copied into Notepad.</span></span>

-   <span data-ttu-id="c40b0-196">按 Ctrl+O 保存更改，当 nano 提示是否保存到同一文件时，按 ENTER 即可。</span><span class="sxs-lookup"><span data-stu-id="c40b0-196">Save your changes by pressing Ctrl+O and when nano prompts you to save it as the same file, just press ENTER.</span></span>

-   <span data-ttu-id="c40b0-197">按 Ctrl+X 退出 nano。</span><span class="sxs-lookup"><span data-stu-id="c40b0-197">Press Ctrl+X to exit nano.</span></span>

-   <span data-ttu-id="c40b0-198">在退出 **~/azure-iot-sdk-node/device/samples** 目录之前运行以下命令</span><span class="sxs-lookup"><span data-stu-id="c40b0-198">Run the following command before leaving the **~/azure-iot-sdk-node/device/samples** directory</span></span>

        npm link azure-iot-device

<a name="Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="c40b0-199">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="c40b0-199">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="c40b0-200">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心服务之间的通信。</span><span class="sxs-lookup"><span data-stu-id="c40b0-200">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub service.</span></span> <span data-ttu-id="c40b0-201">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="c40b0-201">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="c40b0-202">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="c40b0-202">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="c40b0-203">**注意：** 请对以下部分中执行的所有操作进行屏幕截图（如示例屏幕截图）。</span><span class="sxs-lookup"><span data-stu-id="c40b0-203">**Note:** Take screen shots of all operations, like sample screen shots, performed in below sections.</span></span> <span data-ttu-id="c40b0-204">在[步骤 4](#Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c40b0-204">These will be needed in [Step 4](#Share)</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="c40b0-205">3.3.1：向 IOT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="c40b0-205">3.3.1 Send Device Events to IOT Hub:</span></span>

1.  <span data-ttu-id="c40b0-206">如[步骤 2](#Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="c40b0-206">Launch the DeviceExplorer as explained in [Step 2](#Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs, click **Monitor** button.</span></span>

    ![DeviceExplorer_Monitor](images/3_3_1_01.png)

2.  <span data-ttu-id="c40b0-208">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="c40b0-208">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="c40b0-209">在 Termux 应用中发出以下命令运行该示例：</span><span class="sxs-lookup"><span data-stu-id="c40b0-209">Run the sample by issuing following command on Termux app:</span></span>

        node ~/azure-iot-sdk-node/device/samples/simple_sample_device.js

4.  <span data-ttu-id="c40b0-210">检查是否已成功发送和接收数据。</span><span class="sxs-lookup"><span data-stu-id="c40b0-210">Verify that data has been successfully sent and received.</span></span> <span data-ttu-id="c40b0-211">如果出现任何问题，则可能表示未正确复制设备中心连接信息。</span><span class="sxs-lookup"><span data-stu-id="c40b0-211">If any, then you may have incorrectly copied the device hub connection information.</span></span>

    <span data-ttu-id="c40b0-212">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-212">**If using AMQP protocol:**</span></span>

    ![SampleAMQP\_result\_terminal](images/3_3_1_02.png)

    <span data-ttu-id="c40b0-214">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-214">**If using HTTP protocol:**</span></span>

    ![SampleHTTP\_result\_terminal](images/3_3_1_04.png)

    <span data-ttu-id="c40b0-216">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-216">**If using MQTT protocol:**</span></span>

    ![SampleMQTT\_result\_terminal](images/3_3_1_06.png)

5.  <span data-ttu-id="c40b0-218">DeviceExplorer 应显示 IoT 中心已成功接收示例发送的数据。</span><span class="sxs-lookup"><span data-stu-id="c40b0-218">DeviceExplorer should show that IoT Hub has successfully received data sent by sample.</span></span>

    <span data-ttu-id="c40b0-219">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-219">**If using AMQP protocol:**</span></span>

     ![SampleAMQP\_result\_DeviceExplorer](images/3_3_1_03.png)

    <span data-ttu-id="c40b0-221">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-221">**If using HTTP protocol:**</span></span>
    
    ![SampleHTTP\_result\_DeviceExplorer](images/3_3_1_05.png)

    <span data-ttu-id="c40b0-223">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-223">**If using MQTT protocol:**</span></span>
    
    ![SampleMQTT\_result\_DeviceExplorer](images/3_3_1_07.png)


### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="c40b0-225">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="c40b0-225">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="c40b0-226">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="c40b0-226">To verify that you can send messages from the IoT Hub to your device, go to the **Message To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="c40b0-227">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="c40b0-227">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="c40b0-228">在“消息”字段中添加一些文本，然后单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="c40b0-228">Add some text to the Message field, then click Send button.</span></span>

    ![MessageSend_DeviceExplorer](images/3_3_2_01.png)

4.  <span data-ttu-id="c40b0-230">应会在客户端示例的控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="c40b0-230">You should be able to see the command received in the console window of the client sample.</span></span>

     <span data-ttu-id="c40b0-231">**如果使用 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-231">**If using AMQP protocol:**</span></span>

    ![MessageSend\_terminal](images/3_3_2_02.png)

    <span data-ttu-id="c40b0-233">**如果使用 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-233">**If using HTTP protocol:**</span></span>

    ![MessageSend\_terminal](images/3_3_2_03.png)

    <span data-ttu-id="c40b0-235">**如果使用 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="c40b0-235">**If using MQTT protocol:**</span></span>

    ![MessageSend\_terminal](images/3_3_2_04.png)

<a name="PackageShare"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="c40b0-237">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="c40b0-237">Step 4: Package and Share</span></span>

<a name="Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="c40b0-238">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="c40b0-238">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="c40b0-239">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="c40b0-239">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="c40b0-240">生成运行过程中在日志文件记录的生成日志和 E2E 测试结果。</span><span class="sxs-lookup"><span data-stu-id="c40b0-240">Build logs and E2E test results that were logged in the log file during build run.</span></span>

2.  <span data-ttu-id="c40b0-241">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c40b0-241">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="c40b0-242">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c40b0-242">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="c40b0-243">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="c40b0-243">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="c40b0-244">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-nodejs.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="c40b0-244">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-linux-nodejs.md>) to create your device-specific instructions.</span></span>

    <span data-ttu-id="c40b0-245">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="c40b0-245">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Share"></a>
## <a name="42-share-package-with-engineering-support"></a><span data-ttu-id="c40b0-246">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="c40b0-246">4.2 Share package with Engineering Support</span></span>

1.  <span data-ttu-id="c40b0-247">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="c40b0-247">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="c40b0-248">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="c40b0-248">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="c40b0-250">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="c40b0-250">This will open an upload dialog.</span></span> <span data-ttu-id="c40b0-251">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="c40b0-251">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="c40b0-253">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="c40b0-253">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="c40b0-254">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="c40b0-254">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="c40b0-255">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="c40b0-255">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="c40b0-256">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="c40b0-256">4.3 Next steps</span></span>

<span data-ttu-id="c40b0-257">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="c40b0-257">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="c40b0-258">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="c40b0-258">Step 5: Troubleshooting</span></span>

<span data-ttu-id="c40b0-259">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="c40b0-259">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
