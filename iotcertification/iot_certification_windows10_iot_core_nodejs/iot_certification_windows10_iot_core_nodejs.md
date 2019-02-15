<a name="how-to-certify-iot-devices-running-windows-10-iot-core-os-with-azure-iot-sdk"></a><span data-ttu-id="bd71e-101">如何使用 Azure IoT SDK 认证运行 Windows 10 IoT core OS 的 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="bd71e-101">How to Certify IoT devices running Windows 10 IoT core OS with Azure IoT SDK</span></span> 
===
---


<span data-ttu-id="bd71e-102">**注意：\*\*\*\*\*我们不支持将 Windows 10 IoT 核心版与 NodeJS 配合使用。请联系 <iotcert@microsoft.com> 以进行进一步查询。**\*</span><span class="sxs-lookup"><span data-stu-id="bd71e-102">**Note:** ***We are not supporting Windows 10 IoT Core with NodeJS. Please contact <iotcert@microsoft.com> for futher queries.***</span></span>
# <a name="table-of-contents"></a><span data-ttu-id="bd71e-103">目录</span><span class="sxs-lookup"><span data-stu-id="bd71e-103">Table of Contents</span></span>

-   [<span data-ttu-id="bd71e-104">介绍</span><span class="sxs-lookup"><span data-stu-id="bd71e-104">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="bd71e-105">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bd71e-105">Step 1: Sign Up To Azure IoT Hub</span></span>](#Step_1:_Sign_Up)
-   [<span data-ttu-id="bd71e-106">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="bd71e-106">Step 2: Register Device</span></span>](#Step_2:_Register)
-   [<span data-ttu-id="bd71e-107">步骤 3：使用 NodeJS 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="bd71e-107">Step 3: Build and Validate the Sample using NodeJS Client Libraries</span></span>](#Step_3:_Build_and_Validate)
    -   [<span data-ttu-id="bd71e-108">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="bd71e-108">3.1 Connect the Device</span></span>](#Step_3_1:_Connect)
    -   [<span data-ttu-id="bd71e-109">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="bd71e-109">3.2 Build the Samples</span></span>](#Step_3_2:_Build)
    -   [<span data-ttu-id="bd71e-110">3.3：运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="bd71e-110">3.3 Run and Validate the Samples</span></span>](#Step_3_3:_Run)
    -   [<span data-ttu-id="bd71e-111">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="bd71e-111">3.4 Verify Device Configuration</span></span>](#Step3_4)
-   [<span data-ttu-id="bd71e-112">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="bd71e-112">Step 4: Package and Share</span></span>](#Step_4:_Package_Share)
    -   [<span data-ttu-id="bd71e-113">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="bd71e-113">4.1 Package build logs and sample test results</span></span>](#Step_4_1:_Package)
    -   [<span data-ttu-id="bd71e-114">4.2：与工程支持人员共享包</span><span class="sxs-lookup"><span data-stu-id="bd71e-114">4.2 Share package with Engineering Support</span></span>](#Step_4_2:_Share)
    -   [<span data-ttu-id="bd71e-115">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="bd71e-115">4.3 Next steps</span></span>](#Step_4_3:_Next)
-   [<span data-ttu-id="bd71e-116">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="bd71e-116">Step 5: Troubleshooting</span></span>](#Step_5:_Troubleshooting)

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="bd71e-117">介绍</span><span class="sxs-lookup"><span data-stu-id="bd71e-117">Introduction</span></span>

<span data-ttu-id="bd71e-118">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="bd71e-118">**About this document**</span></span>

<span data-ttu-id="bd71e-119">本文档向 IoT 硬件发行商逐步说明如何使用 Azure IoT SDK 来认证支持 IoT 的硬件。</span><span class="sxs-lookup"><span data-stu-id="bd71e-119">This document provides step by step guidance to IoT hardware publishers on how to certify an IoT enabled hardware with Azure IoT SDK.</span></span> <span data-ttu-id="bd71e-120">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="bd71e-120">This multi-step process includes:</span></span>
-   <span data-ttu-id="bd71e-121">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bd71e-121">Configuring Azure IoT Hub</span></span> 
-   <span data-ttu-id="bd71e-122">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="bd71e-122">Registering your IoT device</span></span>
-   <span data-ttu-id="bd71e-123">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="bd71e-123">Build and deploy Azure IoT SDK on device</span></span>
-   <span data-ttu-id="bd71e-124">打包并共享日志</span><span class="sxs-lookup"><span data-stu-id="bd71e-124">Packaging and sharing the logs</span></span>  

<span data-ttu-id="bd71e-125">**准备**</span><span class="sxs-lookup"><span data-stu-id="bd71e-125">**Prepare**</span></span>

<span data-ttu-id="bd71e-126">在执行以下任一步骤之前，请仔细阅读每个过程的每个步骤，确保全盘了解整个过程。</span><span class="sxs-lookup"><span data-stu-id="bd71e-126">Before executing any of the steps below, read through each process, step by step to ensure end to end understanding.</span></span>

<span data-ttu-id="bd71e-127">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="bd71e-127">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="bd71e-128">准备好一台装有 Git 客户端、运行 **Windows 10** 并且可以访问 [azure-iot-sdk-node](https://github.com/Azure/azure-iot-sdk-node) GitHub 公共存储库的计算机。</span><span class="sxs-lookup"><span data-stu-id="bd71e-128">Computer with **Windows 10** having Git client installed and access to the [azure-iot-sdk-node](https://github.com/Azure/azure-iot-sdk-node) GitHub public repository.</span></span>
-   <span data-ttu-id="bd71e-129">安装 Visual Studio 2015 和工具。</span><span class="sxs-lookup"><span data-stu-id="bd71e-129">Install Visual Studio 2015 and Tools.</span></span> <span data-ttu-id="bd71e-130">可以安装任意版本的 Visual Studio，包括免费的 Community 版。</span><span class="sxs-lookup"><span data-stu-id="bd71e-130">You can install any edition of Visual Studio, including the free Community edition.</span></span>

    <span data-ttu-id="bd71e-131">请务必选择“通用 Windows 应用开发工具”，这是编写 Windows 10 应用时必须使用的组件：</span><span class="sxs-lookup"><span data-stu-id="bd71e-131">Make sure to select the "Universal Windows App Development Tools", the component required for writing apps Windows 10:</span></span>
    
    ![安装\_所需的\_工具](images/vs_install_tools_for_windows10.png)
- <span data-ttu-id="bd71e-133">从[此处](<https://www.visualstudio.com/features/node-js-vs>)安装最新的用于 Visual Studio 的 Node.js 工具</span><span class="sxs-lookup"><span data-stu-id="bd71e-133">Install the latest Node.js Tools for Visual Studio from [here](<https://www.visualstudio.com/features/node-js-vs>)</span></span> 
-   <span data-ttu-id="bd71e-134">从[此处](<https://github.com/ms-iot/ntvsiot/releases/tag/v1.5.1>)安装最新的用于 Windows IoT 的 Node.js 工具</span><span class="sxs-lookup"><span data-stu-id="bd71e-134">Install the latest Node.js Tools for Windows IoT from [here](<https://github.com/ms-iot/ntvsiot/releases/tag/v1.5.1>)</span></span> 

-   <span data-ttu-id="bd71e-135">用于认证的、运行 Windows 10 IoT Core 的所需硬件。</span><span class="sxs-lookup"><span data-stu-id="bd71e-135">Required hardware running Windows 10 IoT Core to certify.</span></span>

     <span data-ttu-id="bd71e-136">\*\**注意：\*\*\*\*如果在安装 Windows 10 IoT 核心板时需要帮助，请访问 <https://www.windowsondevices.com> 或者通过 <iotcert@microsoft.com> 联系我们*</span><span class="sxs-lookup"><span data-stu-id="bd71e-136">***Note:*** *If you need assistance installing Windows 10 IoT Core , please visit <https://www.windowsondevices.com> or contact us at <iotcert@microsoft.com>*</span></span>

<a name="Step_1:_Sign_Up"></a>
# <a name="step-1-sign-up-to-azure-iot-hub"></a><span data-ttu-id="bd71e-137">步骤 1：注册 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="bd71e-137">Step 1: Sign Up To Azure IoT Hub</span></span>

<span data-ttu-id="bd71e-138">遵照[此处](https://account.windowsazure.com/signup?offer=ms-azr-0044p)的说明了解如何注册 Azure IoT 中心服务。</span><span class="sxs-lookup"><span data-stu-id="bd71e-138">Follow the instructions [here](https://account.windowsazure.com/signup?offer=ms-azr-0044p) on how to sign up to the Azure IoT Hub service.</span></span>

<span data-ttu-id="bd71e-139">在注册过程中，将会收到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bd71e-139">As part of the sign up process, you will receive the connection string.</span></span>

-   <span data-ttu-id="bd71e-140">**IoT 中心连接字符串**：下面显示了 IoT 中心连接字符串的示例：</span><span class="sxs-lookup"><span data-stu-id="bd71e-140">**IoT Hub Connection String**: An example of IoT Hub Connection String is as below:</span></span>

        HostName=[YourIoTHubName];SharedAccessKeyName=[YourAccessKeyName];SharedAccessKey=[YourAccessKey]

<a name="Step_2:_Register"></a>
# <a name="step-2-register-device"></a><span data-ttu-id="bd71e-141">步骤 2：注册设备</span><span class="sxs-lookup"><span data-stu-id="bd71e-141">Step 2: Register Device</span></span>

-   <span data-ttu-id="bd71e-142">遵照[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>)所述的说明，了解如何预配设备并获取其凭据。</span><span class="sxs-lookup"><span data-stu-id="bd71e-142">Follow the instructions [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/manage_iot_hub.md>) on how to provision your device and get its credentials.</span></span>

<a name="Step_3:_Build_and_Validate"></a>
# <a name="step-3-build-and-validate-the-sample-using-nodejs-client-libraries"></a><span data-ttu-id="bd71e-143">步骤 3：使用 Node.js 客户端库生成并验证示例</span><span class="sxs-lookup"><span data-stu-id="bd71e-143">Step 3: Build and Validate the Sample using Node.js Client Libraries</span></span> 

<span data-ttu-id="bd71e-144">本部分逐步讲解如何使用 Visual Studio 基于现有的 Node.js 客户端 SDK 创建 UWP Node.js 包装器。</span><span class="sxs-lookup"><span data-stu-id="bd71e-144">This section walks you through the steps to create a UWP Node.js wrapper over existing Node.js client SDK using Visual Studio.</span></span> <span data-ttu-id="bd71e-145">完成后，将生成并部署 IoT 客户端 SDK，然后验证使用 Azure IoT SDK 进行 IoT 认证所需的示例测试。</span><span class="sxs-lookup"><span data-stu-id="bd71e-145">Once done, you will build and deploy the IoT Client SDK, and validate the sample tests required for IoT certification with the Azure IoT SDK.</span></span>

<a name="Step_3_1:_Connect"></a>
## <a name="31-connect-the-device"></a><span data-ttu-id="bd71e-146">3.1 连接设备</span><span class="sxs-lookup"><span data-stu-id="bd71e-146">3.1 Connect the Device</span></span>

1.  <span data-ttu-id="bd71e-147">使用以太网电缆将开发板连接到网络。</span><span class="sxs-lookup"><span data-stu-id="bd71e-147">Connect the board to your network using an Ethernet cable.</span></span> <span data-ttu-id="bd71e-148">由于示例依赖于 Internet 访问，因此必须执行此步骤。</span><span class="sxs-lookup"><span data-stu-id="bd71e-148">This step is required, as the sample depends on internet access.</span></span>

2.  <span data-ttu-id="bd71e-149">使用 micro-USB 电缆或电源适配器为开发板供电。</span><span class="sxs-lookup"><span data-stu-id="bd71e-149">Power the board using a micro-USB cable or power adapter.</span></span>

<a name="Step_3_2:_Build"></a>
## <a name="32--build-the-samples"></a><span data-ttu-id="bd71e-150">3.2 生成示例</span><span class="sxs-lookup"><span data-stu-id="bd71e-150">3.2  Build the Samples</span></span>


1.  <span data-ttu-id="bd71e-151">启动 Visual Studio 2015 的新实例。</span><span class="sxs-lookup"><span data-stu-id="bd71e-151">Start a new instance of Visual Studio 2015.</span></span>

2. <span data-ttu-id="bd71e-152">创建新项目（“文件”|“新建项目...”）。</span><span class="sxs-lookup"><span data-stu-id="bd71e-152">Create a new project (**File | New Project…**).</span></span> <span data-ttu-id="bd71e-153">在“新建项目”对话框中导航到 Node.js，如下所示（在对话框的左窗格中，选择“模板”|“JavaScript”|“Node.js”）。</span><span class="sxs-lookup"><span data-stu-id="bd71e-153">In the New Project dialog, navigate to Node.js as shown below (in the left pane in the dialog: Templates | JavaScript | Node.js).</span></span> <span data-ttu-id="bd71e-154">选择“基本 Node.js Johnny-Five 应用程序(通用 Windows)模板”（如下所示）。</span><span class="sxs-lookup"><span data-stu-id="bd71e-154">Select the **Basic Node.js Johnny-Five Application (Universal Windows) template** (shown below).</span></span> <span data-ttu-id="bd71e-155">输入项目的名称，例如 **NodeJsUWPSample**。</span><span class="sxs-lookup"><span data-stu-id="bd71e-155">Enter a name for your project, for example **NodeJsUWPSample**.</span></span> 

    ![VisualStudio\_project\_Template](images/vs_project_template_for_nodejs_uwp.png)

3. <span data-ttu-id="bd71e-157">在解决方案资源管理器中选择 app.js 和 package.json 文件，然后单击右键并选择“删除”。</span><span class="sxs-lookup"><span data-stu-id="bd71e-157">Select app.js and package.json file in Solution Explorer, Right click and select **Delete**.</span></span>

      ![VisualStudio\_delete\_oldfiles](images/Delete_old_files.png)
          
4. <span data-ttu-id="bd71e-159">将 [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-node.git) 存储库克隆到 Windows 10 计算机。</span><span class="sxs-lookup"><span data-stu-id="bd71e-159">Clone [Azure IoT SDK](https://github.com/Azure/azure-iot-sdk-node.git) repository to your Windows 10 machine.</span></span> 

5. <span data-ttu-id="bd71e-160">在文件资源管理器中，复制计算机上存储库 Node.js 示例下面的 **package.json** 和 **simple_sample_device.js** 文件。</span><span class="sxs-lookup"><span data-stu-id="bd71e-160">In File explorer, Copy **package.json** and **simple_sample_device.js** files available under Node.js sample of the repository on your machine.</span></span> <span data-ttu-id="bd71e-161">例如，如果已将 **azure-iot-sdk-node** 存储库克隆到 C:\IOT 目录下，请转到 **(C:\azure-iot-sdk-node\device\samples\)**</span><span class="sxs-lookup"><span data-stu-id="bd71e-161">For example if you cloned the **azure-iot-sdk-node** repository under C:\IOT directory, Go to **(C:\azure-iot-sdk-node\device\samples\)**</span></span>

    ![FileExplorere\_copy\_files](images/copy_files.png)
          
6. <span data-ttu-id="bd71e-163">返回 Visual Studio，在解决方案资源管理器中右键单击项目，然后单击“在文件资源管理器中打开文件夹”。</span><span class="sxs-lookup"><span data-stu-id="bd71e-163">Go back to Visual Studio, Right click your project in Solution Explorer and click **Open Folder in File Explorer**.</span></span>

   ![VisualStudio\_project\_Template](images/open_project_in_file_explorer.png)
    
7. <span data-ttu-id="bd71e-165">将前面复制的文件粘贴到此文件夹中。</span><span class="sxs-lookup"><span data-stu-id="bd71e-165">Paste the files you copied earlier in this folder.</span></span>

    ![FileExplorer\_paste\Files](images/project_file_explorer.png)
    
8. <span data-ttu-id="bd71e-167">返回 Visual Studio，在解决方案资源管理器的顶部上下文菜单中单击“显示所有文件”。</span><span class="sxs-lookup"><span data-stu-id="bd71e-167">Go back to Visual Studio, in Solution Explorer on the top context menu, click **Show All Files**.</span></span>

    ![VisualStudio\show\AllFiles](images/show_all_files.PNG)
    
9. <span data-ttu-id="bd71e-169">右键单击“package.json”和“simple_sample_device.js”文件并选择“包括在项目中”选项。</span><span class="sxs-lookup"><span data-stu-id="bd71e-169">Right click both **package.json** and **simple_sample_device.js** files and choose **Include in project** option.</span></span>

      ![VisualStudio\IncudeIn\Project](images/Include_In_Project.PNG)
        
10. <span data-ttu-id="bd71e-171">右键单击“npm”节点，然后单击“安装缺少的 npm 包”安装解决方案所需的包。</span><span class="sxs-lookup"><span data-stu-id="bd71e-171">Right click the **npm** node and click **Install Missing npm Packages** to install the required packages for the solution.</span></span>

    ![VisualStudio\Install\MissingNpmPackages](images/install-missing-npm-packages.PNG)
    
11. <span data-ttu-id="bd71e-173">在解决方案资源管理器中展开“npm”节点，右键单击显示的但未列在该包中的所有包，然后单击“卸载 npm 程序包”。</span><span class="sxs-lookup"><span data-stu-id="bd71e-173">Expand the npm node in Solution Explorer and right click all package(s) that shows not listed in package and click **Uninstall npm Package(s)**.</span></span>

    ![VisualStudio\_Properties\_Debug](images/Remove_extra_package.PNG)

12.  <span data-ttu-id="bd71e-175">选择 **simple_sample_device.js** 文件，然后在 **simple_sample_device.js** 文件中找到以下代码：</span><span class="sxs-lookup"><span data-stu-id="bd71e-175">Select **simple_sample_device.js** file and locate the following code in the **simple_sample_device.js** file:</span></span>

        <span data-ttu-id="bd71e-176">var connectionString = '[IoT device connection string]';</span><span class="sxs-lookup"><span data-stu-id="bd71e-176">var connectionString = '[IoT device connection string]';</span></span>

13.  <span data-ttu-id="bd71e-177">将 `[IoT device connection string]` 替换为设备的连接字符串，然后**保存**更改。</span><span class="sxs-lookup"><span data-stu-id="bd71e-177">Replace `[IoT device connection string]` with the connection string for your device and **Save** the changes.</span></span> <span data-ttu-id="bd71e-178">如[步骤 2](#Step_2:_Register) 中所述，可从 DeviceExplorer 获取连接字符串。</span><span class="sxs-lookup"><span data-stu-id="bd71e-178">You can get the connection string from DeviceExplorer as explained in [Step 2](#Step_2:_Register).</span></span>

14. <span data-ttu-id="bd71e-179">右键单击“simple_sample_device.js”文件，然后从上下文菜单中选择“设为 Node.JS 启动文件”。</span><span class="sxs-lookup"><span data-stu-id="bd71e-179">Right click the **simple_sample_device.js** file and from context menu choose "Set as Node.JS Startup File".</span></span>

15.  <span data-ttu-id="bd71e-180">选择适当的体系结构（x86 或 ARM，具体取决于设备），将调试方法设置为“远程计算机”：</span><span class="sxs-lookup"><span data-stu-id="bd71e-180">Choose the right architecture (x86 or ARM, depending on your device) and set the debugging method to "Remote Machine":</span></span>

     ![VisualStudio\_Select\_Architecture](images/vs_select_arch.png)
    
16.  <span data-ttu-id="bd71e-182">若要在设备上部署二进制文件，请在“解决方案资源管理器”中右键单击 NodeJsUWPSample 项目，选择“属性”，然后导航到“常规”选项卡：</span><span class="sxs-lookup"><span data-stu-id="bd71e-182">To deploy the binaries on your device, right-click on the NodeJsUWPSample project in the **Solution Explorer**, select **Properties** and navigate to the **General** tab:</span></span>

     ![VisualStudio\_Properties\_Debug](images/vs_properties_debug.png)

   <span data-ttu-id="bd71e-184">键入设备的名称或 IP。</span><span class="sxs-lookup"><span data-stu-id="bd71e-184">Type in the name or IP of your device.</span></span>

17.  <span data-ttu-id="bd71e-185">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="bd71e-185">Build the solution.</span></span>


<a name="Step_3_3:_Run"></a>
## <a name="33-run-and-validate-the-samples"></a><span data-ttu-id="bd71e-186">3.3 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="bd71e-186">3.3 Run and Validate the Samples</span></span>
    
<span data-ttu-id="bd71e-187">在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。</span><span class="sxs-lookup"><span data-stu-id="bd71e-187">In this section you will run the Azure IoT client SDK samples to validate the communication between your device and Azure IoT Hub.</span></span> <span data-ttu-id="bd71e-188">我们要向 Azure IoT 中心服务发送消息，并验证 IoT 中心是否已成功接收数据。</span><span class="sxs-lookup"><span data-stu-id="bd71e-188">You will send the messages to the Azure IoT Hub service and validate that IoT Hub has successfully receive the data.</span></span> <span data-ttu-id="bd71e-189">此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。</span><span class="sxs-lookup"><span data-stu-id="bd71e-189">You will also monitor any messages sent from the Azure IoT Hub to client.</span></span>

<span data-ttu-id="bd71e-190">\*\**注意：\*\*\*\*请对本部分中执行的所有操作进行屏幕截图。* 在[步骤 4](#Step_4_2:_Share) 中需要使用这些屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bd71e-190">***Note:*** *Take screenshots of all the operations you will perform in this section. These will be needed in [Step 4](#Step_4_2:_Share).*</span></span>

### <a name="331-send-device-events-to-iot-hub"></a><span data-ttu-id="bd71e-191">3.3.1：向 IoT 中心发送设备事件</span><span class="sxs-lookup"><span data-stu-id="bd71e-191">3.3.1 Send Device Events to IoT Hub</span></span>

1.  <span data-ttu-id="bd71e-192">如[步骤 2](#Step_2:_Register) 中所述启动 DeviceExplorer，并导航到“数据”选项卡。从设备 ID 下拉列表中选择创建的设备名称，并单击“监视”按钮。</span><span class="sxs-lookup"><span data-stu-id="bd71e-192">Launch the DeviceExplorer as explained in [Step 2](#Step_2:_Register) and navigate to **Data** tab. Select the device name you created from the drop-down list of device IDs and click **Monitor** button.</span></span>

    ![DeviceExplorer\_监视](images/device_explorer_monitor.png)

2.  <span data-ttu-id="bd71e-194">现在，DeviceExplorer 正在监视从选定设备发送到 IoT 中心的数据。</span><span class="sxs-lookup"><span data-stu-id="bd71e-194">DeviceExplorer is now monitoring data sent from the selected device to the IoT Hub.</span></span>
     

3.  <span data-ttu-id="bd71e-195">在 Visual Studio 的“解决方案资源管理器”中右键单击“NodeJsUWPSample”项目，然后单击“调试”&minus;&gt;“启动新实例”生成并运行示例。</span><span class="sxs-lookup"><span data-stu-id="bd71e-195">In Visual Studio, from **Solution Explorer**, right-click the **NodeJsUWPSample** project, click **Debug &minus;&gt; Start new instance** to build and run the sample.</span></span> 

       
4. <span data-ttu-id="bd71e-196">DeviceExplorer 的数据选项卡中应会显示收到的事件。</span><span class="sxs-lookup"><span data-stu-id="bd71e-196">You should be able to see the events received in the DeviceExplorer's data tab.</span></span>

      ![DeviceExplorer\_Events\_Received](images/device_explorer_message_received.png)

### <a name="332-receive-messages-from-iot-hub"></a><span data-ttu-id="bd71e-198">3.3.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="bd71e-198">3.3.2 Receive messages from IoT Hub</span></span>

1.  <span data-ttu-id="bd71e-199">若要验证是否可将消息从 IoT 中心发送到设备，请转到 DeviceExplorer 中的“发送到设备的消息”选项卡。</span><span class="sxs-lookup"><span data-stu-id="bd71e-199">To verify that you can send messages from the IoT Hub to your device, go to the **Messages to Device** tab in DeviceExplorer.</span></span>

2.  <span data-ttu-id="bd71e-200">使用“设备 ID”下拉列表选择创建的设备。</span><span class="sxs-lookup"><span data-stu-id="bd71e-200">Select the device you created using Device ID drop down.</span></span>

3.  <span data-ttu-id="bd71e-201">在“消息”字段中添加一些文本，并单击“发送”。</span><span class="sxs-lookup"><span data-stu-id="bd71e-201">Add some text to the Message field, then click Send.</span></span>

    ![DeviceExplorer\_Notification\_Send](images/device_explorer_notification_send.png)

4.  <span data-ttu-id="bd71e-203">Visual Studio 的“输出”窗口中应会显示收到的消息。</span><span class="sxs-lookup"><span data-stu-id="bd71e-203">You should be able to see the message received in the Visual Studio Output window.</span></span>
    
<a name="#Step3_4"></a>
### <a name="34-verify-device-configuration"></a><span data-ttu-id="bd71e-204">3.4 验证设备配置</span><span class="sxs-lookup"><span data-stu-id="bd71e-204">3.4 Verify Device configuration</span></span>

-  <span data-ttu-id="bd71e-205">在设备上以管理员身份打开 PowerShell 命令提示符，然后运行以下命令</span><span class="sxs-lookup"><span data-stu-id="bd71e-205">Open PowerShell command prompt as an Administrator on your device and run the below commands</span></span>

-   <span data-ttu-id="bd71e-206">首先使用以下命令检查 PowerShell 版本。</span><span class="sxs-lookup"><span data-stu-id="bd71e-206">First check your PowerShell version by using the following command.</span></span>

        $PSversionTable

-  <span data-ttu-id="bd71e-207">如果你的当前 PowerShell 版本低于 5.0，请从[此处](https://aka.ms/wmf5download)下载 PowerShell 最新版本</span><span class="sxs-lookup"><span data-stu-id="bd71e-207">If your current PowerShell version is less than 5.0 then download the PowerShell latest version from [here](https://aka.ms/wmf5download)</span></span>

    <span data-ttu-id="bd71e-208">安装后，请验证新安装的版本，它应为版本 5.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="bd71e-208">After installation please verify the newly installed version, it should be version 5.1 or greater.</span></span> 

-   <span data-ttu-id="bd71e-209">运行以下命令来获取设备配置信息。</span><span class="sxs-lookup"><span data-stu-id="bd71e-209">Run the commands below to get device configuration information.</span></span>

        Get-ComputerInfo -property BiosBIOSVersion, BiosManufacturer, BiosSeralNumber, CsManufacturer, CsModel, CsName, CsNumberOfProcessors, CsProcessors, CsSystemSKUNumber, CsSystemType, OsOperatingSystemSKU | Format-List
          
        Get-NetAdapter
    
    <span data-ttu-id="bd71e-210">**如果设备已与以太网连接**</span><span class="sxs-lookup"><span data-stu-id="bd71e-210">**If Device connected with Ethernet**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Ethernet" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

    <span data-ttu-id="bd71e-211">**如果设备已与 Wi-Fi 连接**</span><span class="sxs-lookup"><span data-stu-id="bd71e-211">**If Device connected with Wi-fi**</span></span>

        $uri = 'http://macvendors.co/api/{0}' -f (Get-NetAdapter | Where-Object -Property Name -eq -Value "Wi-fi" | Select-Object -property macaddress | foreach { $_.MacAddress })

        (Invoke-WebRequest -uri $uri).content | ConvertFrom-Json | Select-Object -Expand result

- <span data-ttu-id="bd71e-212">请查看下面的输出屏幕截图</span><span class="sxs-lookup"><span data-stu-id="bd71e-212">Please find the output screenshot below</span></span>

    ![deviceinfo\_screenshot](images/device_configuration.png)

-   <span data-ttu-id="bd71e-214">请保存设备配置屏幕截图，然后按[步骤 4](#Package) 所述上传该屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bd71e-214">Please save the device configuration screenshot and upload it as mentioned in [Step 4](#Package).</span></span>    
    
<a name="Step_4:_Package_Share"></a>
# <a name="step-4-package-and-share"></a><span data-ttu-id="bd71e-215">步骤 4：打包并共享</span><span class="sxs-lookup"><span data-stu-id="bd71e-215">Step 4: Package and Share</span></span>

<a name="Step_4_1:_Package"></a>
## <a name="41-package-build-logs-and-sample-test-results"></a><span data-ttu-id="bd71e-216">4.1：打包生成日志和示例测试结果</span><span class="sxs-lookup"><span data-stu-id="bd71e-216">4.1 Package build logs and sample test results</span></span>
  
<span data-ttu-id="bd71e-217">打包设备中的以下项目：</span><span class="sxs-lookup"><span data-stu-id="bd71e-217">Package the following artifacts from your device:</span></span>

1.  <span data-ttu-id="bd71e-218">第 3.2 部分所述的生成日志。</span><span class="sxs-lookup"><span data-stu-id="bd71e-218">Build logs from section 3.2.</span></span>
2.  <span data-ttu-id="bd71e-219">前面“向 IoT 中心发送设备事件”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bd71e-219">All the screenshots that are shown above in "**Send Device Events to IoT Hub**" section.</span></span>
3.  <span data-ttu-id="bd71e-220">前面“从 IoT 中心接收消息”部分中显示的所有屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="bd71e-220">All the screenshots that are shown above in "**Receive messages from IoT Hub**" section.</span></span>
4.  <span data-ttu-id="bd71e-221">请向我们发送明确的说明，描述如何使用你的硬件运行此示例（明确强调客户要执行的新步骤）。</span><span class="sxs-lookup"><span data-stu-id="bd71e-221">Send us clear instructions of how to run this sample with your hardware (explicitly highlighting the new steps for customers).</span></span> <span data-ttu-id="bd71e-222">请使用[此处](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-iotcore-nodejs.md>)提供的模板创建设备特定的说明。</span><span class="sxs-lookup"><span data-stu-id="bd71e-222">Please use the template available [here](<https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/templates/template-windows-iotcore-nodejs.md>) to create your device-specific instructions.</span></span>
    
    <span data-ttu-id="bd71e-223">有关说明形式的指导，请参考[此处](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>) GitHub 存储库中发布的示例。</span><span class="sxs-lookup"><span data-stu-id="bd71e-223">As a guideline on how the instructions should look please refer the examples published on GitHub repository [here](<https://github.com/Azure/azure-iot-device-ecosystem/tree/master/get_started>).</span></span>

<a name="Step_4_2:_Share"></a>
## <a name="42-share-package-with-the-azure-iot-certification-team"></a><span data-ttu-id="bd71e-224">4.2 与 Azure IoT 认证团队共享包</span><span class="sxs-lookup"><span data-stu-id="bd71e-224">4.2 Share package with the Azure IoT Certification Team</span></span>

1.  <span data-ttu-id="bd71e-225">转到[合作伙伴仪表板](<https://catalog.azureiotsuite.com/devices>)。</span><span class="sxs-lookup"><span data-stu-id="bd71e-225">Go to [Partner Dashboard](<https://catalog.azureiotsuite.com/devices>).</span></span>
2.  <span data-ttu-id="bd71e-226">单击设备右上角的“上传”图标。</span><span class="sxs-lookup"><span data-stu-id="bd71e-226">Click on Upload icon at top-right corner of your device.</span></span>

    ![Share\_Results\_upload\_icon](images/4_2_01.png)

3.  <span data-ttu-id="bd71e-228">此时会打开上传对话框。</span><span class="sxs-lookup"><span data-stu-id="bd71e-228">This will open an upload dialog.</span></span> <span data-ttu-id="bd71e-229">单击“上传”按钮浏览文件。</span><span class="sxs-lookup"><span data-stu-id="bd71e-229">Browse your file(s) by clicking **Upload** button.</span></span>

    ![Share\_Results\_upload\_dialog](images/4_2_02.png)

    <span data-ttu-id="bd71e-231">可以上传同一设备的多个文件。</span><span class="sxs-lookup"><span data-stu-id="bd71e-231">You can upload multiple files for same device.</span></span>

4.  <span data-ttu-id="bd71e-232">上传所有文件后，单击“提交审查”按钮。</span><span class="sxs-lookup"><span data-stu-id="bd71e-232">Once you have uploaded all the files, click on **Submit for Review** button.</span></span>

    <span data-ttu-id="bd71e-233">\*\**注意：\*\*\*\*提交文件供审查后，若要更改/删除文件，请联系 iotcert 团队。*</span><span class="sxs-lookup"><span data-stu-id="bd71e-233">***Note:*** *Please contact iotcert team to change/remove the files once you submit them for review.*</span></span>
 

<a name="Step_4_3:_Next"></a>
## <a name="43-next-steps"></a><span data-ttu-id="bd71e-234">4.3：后续步骤</span><span class="sxs-lookup"><span data-stu-id="bd71e-234">4.3 Next steps</span></span>

<span data-ttu-id="bd71e-235">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="bd71e-235">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step_5:_Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="bd71e-236">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="bd71e-236">Step 5: Troubleshooting</span></span>

<span data-ttu-id="bd71e-237">如需故障排除的帮助，请通过 <iotcert@microsoft.com> 联系工程支持人员。</span><span class="sxs-lookup"><span data-stu-id="bd71e-237">Please contact engineering support on <iotcert@microsoft.com> for help with troubleshooting.</span></span>
