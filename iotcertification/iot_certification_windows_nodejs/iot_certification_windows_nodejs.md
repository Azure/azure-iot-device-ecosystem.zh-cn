<a name="how-to-certify-iot-devices-running-windows-10-with-azure-iot-sdk"></a><span data-ttu-id="2abfc-101">如何使用 Azure IoT SDK 认证运行 Windows 10 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="2abfc-101">How to certify IoT devices running Windows 10 with Azure IoT SDK</span></span>
===
---


# <a name="table-of-contents"></a><span data-ttu-id="2abfc-102">目录</span><span class="sxs-lookup"><span data-stu-id="2abfc-102">Table of Contents</span></span>

-   [<span data-ttu-id="2abfc-103">介绍</span><span class="sxs-lookup"><span data-stu-id="2abfc-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="2abfc-104">步骤 1：配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2abfc-104">Step 1: Configure Azure IoT Hub</span></span>](#Configure)
-   [<span data-ttu-id="2abfc-105">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="2abfc-105">Step 2: Register Device</span></span>](#Register)
-   [<span data-ttu-id="2abfc-106">步骤 3：使用 Node JS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-106">Step 3: Build and validate the sample using Node JS client libraries</span></span>](#Build)
    -   [<span data-ttu-id="2abfc-107">3.1：在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="2abfc-107">3.1 Load the Azure IoT bits and prerequisites on device</span></span>](#Load)
    -   [<span data-ttu-id="2abfc-108">3.2：生成示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-108">3.2 Build the samples</span></span>](#BuildSamples)
    -   [<span data-ttu-id="2abfc-109">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-109">3.3 Run and Validate the Samples</span></span>](#Run)
    -   [<span data-ttu-id="2abfc-110">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="2abfc-110">3.4 Verify Device Configuration</span></span>](#Step3_4)
-   [<span data-ttu-id="2abfc-111">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="2abfc-111">Step 4: Package and Share</span></span>](#PackageShare)
    -   [<span data-ttu-id="2abfc-112">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="2abfc-112">4.1 Package build logs and sample test results</span></span>](#Package)
    -   [<span data-ttu-id="2abfc-113">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="2abfc-113">4.2 Share package with Engineering Support</span></span>](#Share)
    -   [<span data-ttu-id="2abfc-114">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="2abfc-114">4.3 Next steps</span></span>](#Next)
-   [<span data-ttu-id="2abfc-115">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="2abfc-115">Step 5: Troubleshooting</span></span>](#Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="2abfc-116">介绍</span><span class="sxs-lookup"><span data-stu-id="2abfc-116">Introduction</span></span>

<span data-ttu-id="2abfc-117">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="2abfc-117">**About this document**</span></span>

<span data-ttu-id="2abfc-118">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="2abfc-118">This document provides step-by-step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="2abfc-119">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="2abfc-119">This multi-step process includes:</span></span>

-   <span data-ttu-id="2abfc-120">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2abfc-120">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="2abfc-121">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="2abfc-121">Registering your IoT device</span></span>
-   <span data-ttu-id="2abfc-122">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="2abfc-122">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="2abfc-123">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="2abfc-123">Packaging and sharing the logs</span></span>

<span data-ttu-id="2abfc-124">**准备**</span><span class="sxs-lookup"><span data-stu-id="2abfc-124">**Prepare**</span></span>

<span data-ttu-id="2abfc-125">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="2abfc-125">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="2abfc-126">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="2abfc-126">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="2abfc-127">用于认证的所需硬件。</span><span class="sxs-lookup"><span data-stu-id="2abfc-127">Required hardware to certify.</span></span>
-   <span data-ttu-id="2abfc-128">在 **C:\OpenSSL** 位置安装 OpenSSL 并执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2abfc-128">Install OpenSSL at **C:\OpenSSL** location and perform following actions:</span></span>
    -   <span data-ttu-id="2abfc-129">将 `C:\OpenSSL\` 添加到 **PATH** 环境变量</span><span class="sxs-lookup"><span data-stu-id="2abfc-129">Add `C:\OpenSSL\` to the **PATH** environment variable</span></span>
    -   <span data-ttu-id="2abfc-130">在 OpenSSL 目录中搜索“openssl.cnf”文件的位置。</span><span class="sxs-lookup"><span data-stu-id="2abfc-130">Search for the location of file 'openssl.cnf' inside the OpenSSL directory.</span></span>
    -   <span data-ttu-id="2abfc-131">创建新环境变量 **OPENSSL_CONF** 并将其值设置为 `openssl.cnf` 文件的绝对路径。</span><span class="sxs-lookup"><span data-stu-id="2abfc-131">Create a new environment variable **OPENSSL_CONF** and set its value as absolute path of the file `openssl.cnf`.</span></span>

-   <span data-ttu-id="2abfc-132">安装 [NodeJS](https://nodejs.org/)。</span><span class="sxs-lookup"><span data-stu-id="2abfc-132">Install [NodeJS](https://nodejs.org/).</span></span> <span data-ttu-id="2abfc-133">确保 NodeJS 的版本高于 4.0。</span><span class="sxs-lookup"><span data-stu-id="2abfc-133">Make sure that version of NodeJS is greater than 4.0.</span></span>
-   <span data-ttu-id="2abfc-134">安装 [GIT](https://git-scm.com/download/win)。</span><span class="sxs-lookup"><span data-stu-id="2abfc-134">Install [GIT](https://git-scm.com/download/win).</span></span>

<span data-ttu-id="2abfc-135">\*\**注意：\*\*\*\*如果尚未联系 Microsoft 来申请成为“Azure IoT 认证”合作伙伴，请先提交此[表单](<https://iotcert.cloudapp.net/>)请求此身份，然后遵照本文中的说明操作。*</span><span class="sxs-lookup"><span data-stu-id="2abfc-135">***Note:*** *If you haven’t contacted Microsoft about being an Azure Certified for IoT partner, please submit this [form](<https://iotcert.cloudapp.net/>) first to request it and then follow these instructions.*</span></span>

<a name="Configure"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="2abfc-136">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="2abfc-136">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="2abfc-137">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="2abfc-137">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="2abfc-138">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2abfc-138">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="2abfc-139">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="2abfc-139">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

          HostName=[YourIoTHubName];CredentialType=SharedAccessSignature;CredentialScope=[ContosoIotHub];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="2abfc-140">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="2abfc-140">Step 2: Register Device</span></span>

<span data-ttu-id="2abfc-141">在本部分，我们将使用 DeviceExplorer 注册设备。</span><span class="sxs-lookup"><span data-stu-id="2abfc-141">In this section, you will register your device using DeviceExplorer.</span></span> <span data-ttu-id="2abfc-142">DeviceExplorer 是与 Azure IoT 中心对接的 Windows 应用程序，可执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="2abfc-142">The DeviceExplorer is a Windows application that interfaces with Azure IoT Hub and can perform the following operations:</span></span>

-   <span data-ttu-id="2abfc-143">设备管理</span><span class="sxs-lookup"><span data-stu-id="2abfc-143">Device management</span></span>
    -   <span data-ttu-id="2abfc-144">创建新设备</span><span class="sxs-lookup"><span data-stu-id="2abfc-144">Create new devices</span></span>
    -   <span data-ttu-id="2abfc-145">列出现有设备并公开设备中心存储的设备属性</span><span class="sxs-lookup"><span data-stu-id="2abfc-145">List existing devices and expose device properties stored on Device Hub</span></span>
    -   <span data-ttu-id="2abfc-146">提供更新设备密钥的功能</span><span class="sxs-lookup"><span data-stu-id="2abfc-146">Provides ability to update device keys</span></span>
    -   <span data-ttu-id="2abfc-147">可删除设备</span><span class="sxs-lookup"><span data-stu-id="2abfc-147">Provides ability to delete a device</span></span>
-   <span data-ttu-id="2abfc-148">监视设备的事件。</span><span class="sxs-lookup"><span data-stu-id="2abfc-148">Monitoring events from your device.</span></span>
-   <span data-ttu-id="2abfc-149">向设备发送消息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-149">Sending messages to your device.</span></span>

<span data-ttu-id="2abfc-150">若要运行 DeviceExplorer 工具，请根据[步骤 1](#Configure) 中所述使用配置字符串：</span><span class="sxs-lookup"><span data-stu-id="2abfc-150">To run DeviceExplorer tool, follow the configuration strings as described in  [Step1](#Configure):</span></span>

-   <span data-ttu-id="2abfc-151">IoT 中心连接字符串</span><span class="sxs-lookup"><span data-stu-id="2abfc-151">IoT Hub Connection String</span></span>

<span data-ttu-id="2abfc-152">**步骤：**</span><span class="sxs-lookup"><span data-stu-id="2abfc-152">**Steps:**</span></span>

1.   <span data-ttu-id="2abfc-153">单击[此处](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>)下载并安装 DeviceExplorer。</span><span class="sxs-lookup"><span data-stu-id="2abfc-153">Click [here](<https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md>) to download and install DeviceExplorer.</span></span>

2.  <span data-ttu-id="2abfc-154">在“配置”选项卡下添加连接信息，并单击“更新”按钮。</span><span class="sxs-lookup"><span data-stu-id="2abfc-154">Add connection information under the Configuration tab and click the **Update** button.</span></span>

3.  <span data-ttu-id="2abfc-155">根据以下说明创建设备并将其注册到 IoT 中心。</span><span class="sxs-lookup"><span data-stu-id="2abfc-155">Create and register the device with your IoT Hub using instructions as below.</span></span>

    <span data-ttu-id="2abfc-156">a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，然后单击“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="2abfc-156">a.</span></span> <span data-ttu-id="2abfc-157">单击“管理”选项卡。</span><span class="sxs-lookup"><span data-stu-id="2abfc-157">Click the **Management** tab.</span></span>

    <span data-ttu-id="2abfc-158">b.保留“数据库类型”设置，即设置为“共享”。</span><span class="sxs-lookup"><span data-stu-id="2abfc-158">b.</span></span> <span data-ttu-id="2abfc-159">注册的设备将显示在列表中。</span><span class="sxs-lookup"><span data-stu-id="2abfc-159">Your registered devices will be visible in the list.</span></span> <span data-ttu-id="2abfc-160">如果该设备未显示在列表中，请单击“刷新”按钮。</span><span class="sxs-lookup"><span data-stu-id="2abfc-160">In case your device is not there in the list, click **Refresh** button.</span></span> <span data-ttu-id="2abfc-161">如果这是第一次注册设备，请不要检索任何信息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-161">If this is your first time, then you shouldn't retrieve anything.</span></span>

    <span data-ttu-id="2abfc-162">c.</span><span class="sxs-lookup"><span data-stu-id="2abfc-162">c.</span></span> <span data-ttu-id="2abfc-163">单击“创建”按钮创建设备 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="2abfc-163">Click **Create** button to create a device ID and key.</span></span>

    <span data-ttu-id="2abfc-164">d.单击“下一步”。</span><span class="sxs-lookup"><span data-stu-id="2abfc-164">d.</span></span> <span data-ttu-id="2abfc-165">成功创建设备后，该设备将列在 DeviceExplorer 中。</span><span class="sxs-lookup"><span data-stu-id="2abfc-165">Once created successfully, device will be listed in DeviceExplorer.</span></span>

    <span data-ttu-id="2abfc-166">e.在“新建 MySQL 数据库”边栏选项卡中，接受法律条款，然后单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="2abfc-166">e.</span></span> <span data-ttu-id="2abfc-167">右键单击该设备，然后从上下文菜单中选择“复制所选设备的连接字符串”。</span><span class="sxs-lookup"><span data-stu-id="2abfc-167">Right click the device and from context menu select "**Copy connection string for selected device**".</span></span>

    <span data-ttu-id="2abfc-168">f.</span><span class="sxs-lookup"><span data-stu-id="2abfc-168">f.</span></span> <span data-ttu-id="2abfc-169">在记事本中保存此信息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-169">Save this information in Notepad.</span></span> <span data-ttu-id="2abfc-170">后面的步骤需要用到此信息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-170">You will need this information in later steps.</span></span>

<span data-ttu-id="2abfc-171">***不是在电脑上运行 Windows？***</span><span class="sxs-lookup"><span data-stu-id="2abfc-171">***Not running Windows on your PC?***</span></span> <span data-ttu-id="2abfc-172">- 请遵照[此处](<https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/manage_iot_hub.md>)的说明预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="2abfc-172">- Please follow the instructions [here](<https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/manage_iot_hub.md>) to provision your device and get its credentials.</span></span>

<a name="Build"></a>
# <a name="step-3-build-and-validate-the-sample-using-node-js-client-libraries"></a><span data-ttu-id="2abfc-173">步骤 3：使用 Node JS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-173">Step 3: Build and validate the sample using Node JS client libraries</span></span>

<span data-ttu-id="2abfc-174">本部分逐步讲解如何在运行 Windows 操作系统的设备上生成、部署和验证 IoT 客户端 SDK。</span><span class="sxs-lookup"><span data-stu-id="2abfc-174">This section walks you through building, deploying and validating the IoT Client SDK on your device running a Windows operating system.</span></span> <span data-ttu-id="2abfc-175">我们将在设备上安装必备组件。</span><span class="sxs-lookup"><span data-stu-id="2abfc-175">You will install necessary prerequisites on your device.</span></span>  <span data-ttu-id="2abfc-176">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="2abfc-176">Once done,  you will build and deploy the IoT Client SDK and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Load"></a>
## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a><span data-ttu-id="2abfc-177">3.1 在设备上加载 Azure IoT 代码和必备组件</span><span class="sxs-lookup"><span data-stu-id="2abfc-177">3.1 Load the Azure IoT bits and prerequisites on device</span></span>

-   <span data-ttu-id="2abfc-178">创建环境变量 `IOTHUB_CONNECTION_STRING`，并将其值设置为在[步骤 1](#Configure) 中获取的 **IoT 中心连接字符串**。</span><span class="sxs-lookup"><span data-stu-id="2abfc-178">Create environment variable `IOTHUB_CONNECTION_STRING` and set its value as your **IoTHub connection string** which you got in [Step 1](#Configure).</span></span>

-   <span data-ttu-id="2abfc-179">打开 Node.js 命令提示符并运行以下命令</span><span class="sxs-lookup"><span data-stu-id="2abfc-179">Open the Node.js command prompt and run the following commands</span></span>

        node -v

    <span data-ttu-id="2abfc-180">确保 Node 版本高于 4.0。</span><span class="sxs-lookup"><span data-stu-id="2abfc-180">Make sure node version is greater than 4.0.</span></span>
        
-   <span data-ttu-id="2abfc-181">检查是否已正确设置所有环境变量。</span><span class="sxs-lookup"><span data-stu-id="2abfc-181">Check all environment variables are properly set.</span></span>

        echo %PATH%
        echo %OPENSSL_CONF%
        echo %IOTHUB_CONNECTION_STRING%
    
-   <span data-ttu-id="2abfc-182">下载该 SDK</span><span class="sxs-lookup"><span data-stu-id="2abfc-182">Download the SDK</span></span> 

        git clone --recursive https://github.com/Azure/azure-iot-sdk-node.git

<a name="BuildSamples"></a>
## <a name="32-build-the-samples"></a><span data-ttu-id="2abfc-183">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-183">3.2 Build the samples</span></span>

-   <span data-ttu-id="2abfc-184">若要验证源代码，请在设备上的 Node.js 命令提示符下运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="2abfc-184">To validate the source code run the following commands on Node.js command prompt on Device.</span></span>

        cd azure-iot-sdk-node
        build\dev-setup.cmd
        build\build.cmd > LogFile.txt

    <span data-ttu-id="2abfc-185">***注意：*** 应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。</span><span class="sxs-lookup"><span data-stu-id="2abfc-185">***Note:*** *LogFile.txt in above command should be replaced with a file name where build output will be written.*</span></span>

-   <span data-ttu-id="2abfc-186">安装 npm 包以运行示例。</span><span class="sxs-lookup"><span data-stu-id="2abfc-186">Install npm package to run sample.</span></span>

        cd \azure-iot-sdk-node\device\samples

    <span data-ttu-id="2abfc-187">**对于 AMQP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2abfc-187">**For AMQP Protocol:**</span></span>
    
        npm install azure-iot-device-amqp
    
    <span data-ttu-id="2abfc-188">**对于 HTTP 协议：**</span><span class="sxs-lookup"><span data-stu-id="2abfc-188">**For HTTP Protocol:**</span></span>
    
        npm install azure-iot-device-http
    
    <span data-ttu-id="2abfc-189">**对于 MQTT 协议：**</span><span class="sxs-lookup"><span data-stu-id="2abfc-189">**For MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt   

    <span data-ttu-id="2abfc-190">**对于将 Web Socket 与 AMQP 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="2abfc-190">**For Web Sockets with AMQP Protocol:**</span></span>

        npm install azure-iot-device-amqp

    <span data-ttu-id="2abfc-191">**对于将 Web Socket 与 MQTT 协议配合使用：**</span><span class="sxs-lookup"><span data-stu-id="2abfc-191">**For Web Sockets with MQTT Protocol:**</span></span>

        npm install azure-iot-device-mqtt

-   <span data-ttu-id="2abfc-192">更新示例以设置协议。</span><span class="sxs-lookup"><span data-stu-id="2abfc-192">Update the sample to set the protocol.</span></span>

        cd azure-iot-sdk-node\device\samples
        notepad simple_sample_device.js

-   <span data-ttu-id="2abfc-193">这会启动文本编辑器。</span><span class="sxs-lookup"><span data-stu-id="2abfc-193">This launches a text editor.</span></span> <span data-ttu-id="2abfc-194">向下滚动到协议信息，找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="2abfc-194">Scroll down to the protocol information and find the below code:</span></span>

        var Protocol = require('azure-iot-device-amqp').Amqp;
    
    <span data-ttu-id="2abfc-195">使用的默认协议为 AMQP。</span><span class="sxs-lookup"><span data-stu-id="2abfc-195">The default protocol used is AMQP.</span></span> <span data-ttu-id="2abfc-196">脚本中紧接在上述代码行的下面会提到其他协议 (HTTP/MQTT) 的代码。</span><span class="sxs-lookup"><span data-stu-id="2abfc-196">Code for other protocols(HTTP/MQTT) are mentioned just below the above line in the script.</span></span> 
    <span data-ttu-id="2abfc-197">请根据想要使用的协议取消注释相应的代码行。</span><span class="sxs-lookup"><span data-stu-id="2abfc-197">Uncomment the line as per the protocol you want to use.</span></span>

-   <span data-ttu-id="2abfc-198">向下滚动到连接信息，找到 IoT 连接字符串的以下占位符：</span><span class="sxs-lookup"><span data-stu-id="2abfc-198">Scroll down to the connection information and find following placeholder for IoT connection string:</span></span>

        var connectionString = "[IoT Device Connection String]";

    <span data-ttu-id="2abfc-199">将上述占位符替换为设备连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2abfc-199">Replace the above placeholder with device connection string.</span></span> <span data-ttu-id="2abfc-200">可根据[步骤 2](#Register) 中所述，从 DeviceExplorer 获取这个已复制到记事本的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="2abfc-200">You can get this from DeviceExplorer as explained in [Step 2](#Register), that you copied into Notepad.</span></span>

-   <span data-ttu-id="2abfc-201">保存更改并关闭记事本。</span><span class="sxs-lookup"><span data-stu-id="2abfc-201">Save your changes and close the notepad.</span></span>

-   <span data-ttu-id="2abfc-202">退出 **azure-iot-sdk-node\device\samples** 目录之前，在 Node.js 命令提示符下运行以下命令</span><span class="sxs-lookup"><span data-stu-id="2abfc-202">Run the following command on Node.js command prompt before leaving the **azure-iot-sdk-node\device\samples** directory</span></span>

        npm link azure-iot-device

<a name="Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="2abfc-203">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-203">3.3 Run and Validate the Samples</span></span>

<span data-ttu-id="2abfc-204">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心服务之间的通信。</span><span class="sxs-lookup"><span data-stu-id="2abfc-204">In this section you will run the Azure IoT client SDK samples to validate communication between your device and Azure IoT Hub service.</span></span> <span data-ttu-id="2abfc-205">我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="2abfc-205">You will send messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="2abfc-206">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-206">You will also monitor any messages send from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="2abfc-207">**注意：** 请对以下部分中执行的所有操作进行屏幕截图（如示例屏幕截图）。</span><span class="sxs-lookup"><span data-stu-id="2abfc-207">**Note:** Take screen shots of all operations, like sample screen shots, performed in below sections.</span></span> <span data-ttu-id="2abfc-208">在[步骤 4](#Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2abfc-208">These will be needed in [Step 4](#Share)</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="2abfc-209">3.3.1：向 IOT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="2abfc-209">3.3.1 Send Device Events to IOT Hub:</span></span>

1.  <span data-ttu-id="2abfc-210">如[步骤 2](#Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，然后单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="2abfc-210">Launch the DeviceExplorer as explained in [Step 2](#Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs, click **Monitor** button.</span></span>

    ![DeviceExplorer_Monitor](images/3_3_1_01.png)

2.  <span data-ttu-id="2abfc-212">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="2abfc-212">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>

3.  <span data-ttu-id="2abfc-213">在 Node.js 命令提示符下发出以下命令来运行示例</span><span class="sxs-lookup"><span data-stu-id="2abfc-213">Run the sample by issuing following command on Node.js command prompt</span></span>

        node azure-iot-sdk-node\device\samples\simple_sample_device.js
    
4.  <span data-ttu-id="2abfc-214">检查是否已成功发送数据。</span><span class="sxs-lookup"><span data-stu-id="2abfc-214">Verify that data has been successfully sent.</span></span> <span data-ttu-id="2abfc-215">如果没有，则可能表示未正确复制设备连接信息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-215">If not, then you may have incorrectly copied the device connection information.</span></span>

    ![SampleAMQP\_result\_terminal](images/3_3_1_02.png)

5.  <span data-ttu-id="2abfc-217">DeviceExplorer 应显示 IoT 中心已成功接收示例发送的数据。</span><span class="sxs-lookup"><span data-stu-id="2abfc-217">DeviceExplorer should show that IoT Hub has successfully received data sent by sample.</span></span>

     ![SampleAMQP\_result\_DeviceExplorer](images/3_3_1_03.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="2abfc-219">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="2abfc-219">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="2abfc-220">若要验证是否可从 IoT 中心向设备发送消息，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="2abfc-220">To verify that you can send messages from the IoT Hub to your device, go to the **Message To Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="2abfc-221">使用设备 ID 下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="2abfc-221">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="2abfc-222">在“消息”字段中添加一些文本，然后单击“发送”按钮。</span><span class="sxs-lookup"><span data-stu-id="2abfc-222">Add some text to the Message field, then click Send button.</span></span>

    ![MessageSend_DeviceExplorer](images/3_3_2_01.png)

4.  <span data-ttu-id="2abfc-224">应会在控制台窗口中看到收到的命令。</span><span class="sxs-lookup"><span data-stu-id="2abfc-224">You should be able to see the command received in the console window.</span></span>

    ![MessageSend\_terminal](images/3_3_2_02.png)

<a name="#Step3_4"></a>
### <a name="34-verify-device-configuration"></a><span data-ttu-id="2abfc-226">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="2abfc-226">3.4 Verify Device configuration</span></span>

-  <span data-ttu-id="2abfc-227">在设备上以管理员身份打开 PowerShell 命令提示符，然后运行以下命令</span><span class="sxs-lookup"><span data-stu-id="2abfc-227">Open PowerShell command prompt as an Administrator on your device and run the below commands</span></span>

-   <span data-ttu-id="2abfc-228">首先使用以下命令检查 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="2abfc-228">First check your PowerShell version by using the following command.</span></span>

        $PSversionTable

-  <span data-ttu-id="2abfc-229">如果你的当前 PowerShell 版本低于 5.0，请从[此处](https://aka.ms/wmf5download)下载 PowerShell 最新版本</span><span class="sxs-lookup"><span data-stu-id="2abfc-229">If your current PowerShell version is less than 5.0 then download the PowerShell latest version from [here](https://aka.ms/wmf5download)</span></span>

    <span data-ttu-id="2abfc-230">安装后，请验证新安装的版本，它应为版本 5.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="2abfc-230">After installation please verify the newly installed version, it should be version 5.1 or greater.</span></span> 

-   <span data-ttu-id="2abfc-231">运行以下命令来获取设备配置信息。</span><span class="sxs-lookup"><span data-stu-id="2abfc-231">Run the commands below to get device configuration information.</span></span>

        Get-ComputerInfo -property BiosBIOSVersion, BiosManufacturer, BiosSeralNumber, CsManufacturer, CsModel, CsName, CsNumberOfProcessors, CsProcessors, CsSystemSKUNumber, CsSystemType, OsOperatingSystemSKU | Format-List
          
        Get-NetAdapter
    
    <span data-ttu-id="2abfc-232">**如果设备已与以太网连接**</span><span class="sxs-lookup"><span data-stu-id="2abfc-232">**If Device connected with Ethernet**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Ethernet" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

    <span data-ttu-id="2abfc-233">**如果设备已与 Wi-Fi 连接**</span><span class="sxs-lookup"><span data-stu-id="2abfc-233">**If Device connected with Wi-fi**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Wi-fi" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

- <span data-ttu-id="2abfc-234">请查看下面的输出屏幕截图</span><span class="sxs-lookup"><span data-stu-id="2abfc-234">Please find the output screenshot below</span></span>

    ![deviceinfo\_screenshot](images/device_configuration.png)

-   <span data-ttu-id="2abfc-236">请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2abfc-236">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Package).</span></span>

<a name="PackageShare"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="2abfc-237">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="2abfc-237">Step 4: Package and Share</span></span>

<a name="Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="2abfc-238">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="2abfc-238">4.1 Package build logs and sample test results</span></span>

<span data-ttu-id="2abfc-239">从设备打包以下项目：</span><span class="sxs-lookup"><span data-stu-id="2abfc-239">Package following artifacts from your device:</span></span>

1.  <span data-ttu-id="2abfc-240">生成运行过程中在日志文件记录的生成日志和 E2E 测试结果。</span><span class="sxs-lookup"><span data-stu-id="2abfc-240">Build logs and E2E test results that were logged in the log file during build run.</span></span>

2.  <span data-ttu-id="2abfc-241">前面“**向 IoT 中心发送设备事件**”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2abfc-241">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>

3.  <span data-ttu-id="2abfc-242">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="2abfc-242">All the screenshots that are above in "**Receive messages from IoT Hub**" section.</span></span>

4.  <span data-ttu-id="2abfc-243">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="2abfc-243">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="2abfc-244">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-nodejs.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="2abfc-244">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-nodejs.md>) to create your device-specific instructions.</span></span>

    <span data-ttu-id="2abfc-245">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="2abfc-245">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Share"></a>
## <a name="42-share-package-with-engineering-support"></a><span data-ttu-id="2abfc-246">4.2 与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="2abfc-246">4.2 Share package with Engineering Support</span></span>

1.  <span data-ttu-id="2abfc-247">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="2abfc-247">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="2abfc-248">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="2abfc-248">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="2abfc-250">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="2abfc-250">This will open an upload dialog.</span></span> <span data-ttu-id="2abfc-251">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="2abfc-251">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="2abfc-253">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="2abfc-253">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="2abfc-254">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="2abfc-254">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="2abfc-255">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="2abfc-255">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="2abfc-256">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="2abfc-256">4.3 Next steps</span></span>

<span data-ttu-id="2abfc-257">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="2abfc-257">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="2abfc-258">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="2abfc-258">Step 5: Troubleshooting</span></span>

<span data-ttu-id="2abfc-259">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="2abfc-259">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
