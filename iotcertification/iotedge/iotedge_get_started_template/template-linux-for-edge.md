---
platform:
  enter the OS name running on edge device: 
device:
  enter your device name here: 
language:
  enter the language used to you edge device: 
ms.openlocfilehash: f683bf1198e4e49d4852c2bfd0f84ffa5de7aa78
ms.sourcegitcommit: a5f004161e77a795c776465344fd6f78f565a0bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2018
ms.locfileid: "52891447"
---
<span data-ttu-id="b2303-101">*强烈建议使此文档保持最新，如果文档包含损坏的 URL 链接、不正确的信息等等，请记住，Microsoft 预留了从 Azure IoT 设备目录中删除设备和文档的权利。*</span><span class="sxs-lookup"><span data-stu-id="b2303-101">*We highly recommend keeping this document current, and Microsoft reserves a right to remove devices and documents from the Azure IoT Device Catalog if document contains broken URL links, incorrect information etc.*</span></span>

<a name="run-a-simple-enter-the-language-used-to-you-edge-device-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-edge-device-specify-distribution-or-windows-sku-information-ex-ubuntu-sever-1604-windows-10-iot-core-only-tier-1-oshttpsdocsmicrosoftcomen-usazureiot-edgesupport-is-allowed"></a><span data-ttu-id="b2303-102">在运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 {输入用于 Edge 设备的语言} 示例。</span><span class="sxs-lookup"><span data-stu-id="b2303-102">Run a simple {enter the language used to you edge device} sample on {enter your device name here} device running {enter the OS name running on edge device.</span></span> <span data-ttu-id="b2303-103">指定发行版或 Windows SKU 信息。</span><span class="sxs-lookup"><span data-stu-id="b2303-103">Specify distribution or Windows SKU information.</span></span> <span data-ttu-id="b2303-104">例如：Ubuntu Sever 16.04、Windows 10 IoT 核心版。</span><span class="sxs-lookup"><span data-stu-id="b2303-104">Ex: Ubuntu Sever 16.04, Windows 10 IoT Core.</span></span> <span data-ttu-id="b2303-105">仅允许[第 1 层 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support)。</span><span class="sxs-lookup"><span data-stu-id="b2303-105">Only [Tier 1 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support) is allowed}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="b2303-106">目录</span><span class="sxs-lookup"><span data-stu-id="b2303-106">Table of Contents</span></span>

-   [<span data-ttu-id="b2303-107">介绍</span><span class="sxs-lookup"><span data-stu-id="b2303-107">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="b2303-108">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="b2303-108">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="b2303-109">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="b2303-109">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="b2303-110">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="b2303-110">Step 3: Manual Test for Azure IoT Edge on device</span></span>](#Manual)
-   [<span data-ttu-id="b2303-111">步骤 4：后续步骤</span><span class="sxs-lookup"><span data-stu-id="b2303-111">Step 4: Next Steps</span></span>](#NextSteps)
-   [<span data-ttu-id="b2303-112">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="b2303-112">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="b2303-113">有关使用此模板的说明</span><span class="sxs-lookup"><span data-stu-id="b2303-113">Instructions for using this template</span></span>

-   <span data-ttu-id="b2303-114">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="b2303-114">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="b2303-115">遵照 {{enclosed}} 行之间的说明后，删除这些行。</span><span class="sxs-lookup"><span data-stu-id="b2303-115">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="b2303-116">建议尽量使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="b2303-116">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="b2303-117">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="b2303-117">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="b2303-118">介绍</span><span class="sxs-lookup"><span data-stu-id="b2303-118">Introduction</span></span>

<span data-ttu-id="b2303-119">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="b2303-119">**About this document**</span></span>

<span data-ttu-id="b2303-120">本文档介绍了如何使用预先安装的 Azure IoT Edge 运行时和“设备管理”来连接运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="b2303-120">This document describes how to connect {enter your device name here} device running {enter the OS name running on edge device} with Azure IoT Edge Runtime pre-installed and Device Management.</span></span> <span data-ttu-id="b2303-121">此过程由多个步骤构成，具体包括：</span><span class="sxs-lookup"><span data-stu-id="b2303-121">This multi-step process includes:</span></span>

-   <span data-ttu-id="b2303-122">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="b2303-122">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="b2303-123">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="b2303-123">Registering your IoT device</span></span>
-   <span data-ttu-id="b2303-124">构建并部署客户端组件来测试设备管理功能</span><span class="sxs-lookup"><span data-stu-id="b2303-124">Build and Deploy client component to test device management capability</span></span> 

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="b2303-125">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="b2303-125">Step 1: Prerequisites</span></span>

<span data-ttu-id="b2303-126">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="b2303-126">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="b2303-127">[准备开发环境][setup-devbox-linux]</span><span class="sxs-lookup"><span data-stu-id="b2303-127">[Prepare your development environment][setup-devbox-linux]</span></span>
-   [<span data-ttu-id="b2303-128">设置 IoT 中心</span><span class="sxs-lookup"><span data-stu-id="b2303-128">Setup your IoT hub</span></span>](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   <span data-ttu-id="b2303-129">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="b2303-129">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   [<span data-ttu-id="b2303-130">注册到 IOT 中心</span><span class="sxs-lookup"><span data-stu-id="b2303-130">Sign up to IOT Hub</span></span>](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   [<span data-ttu-id="b2303-131">添加 Edge 设备</span><span class="sxs-lookup"><span data-stu-id="b2303-131">Add the Edge Device</span></span>](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux)
-   [<span data-ttu-id="b2303-132">添加 Edge 模块</span><span class="sxs-lookup"><span data-stu-id="b2303-132">Add the Edge Modules</span></span>](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#deploy-a-module)
-   <span data-ttu-id="b2303-133">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="b2303-133">{enter your device name here} device.</span></span>
-   <span data-ttu-id="b2303-134">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="b2303-134">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="b2303-135">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="b2303-135">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="b2303-136">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="b2303-136">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="b2303-137">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="b2303-137">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a><span data-ttu-id="b2303-138">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="b2303-138">Step 3: Manual Test for Azure IoT Edge on device</span></span>

<span data-ttu-id="b2303-139">本部分将引导你在运行 Linux 操作系统的 Edge 设备上执行测试，使该设备符合 Azure IoT Edge 认证的要求。</span><span class="sxs-lookup"><span data-stu-id="b2303-139">This section walks you through the test to be performed on the Edge devices running the Linux operating system such that it can qualify for Azure IoT Edge certification.</span></span>

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a><span data-ttu-id="b2303-140">3.1：Edge RuntimeEnabled（必需）</span><span class="sxs-lookup"><span data-stu-id="b2303-140">3.1 Edge RuntimeEnabled (Mandatory)</span></span>

<span data-ttu-id="b2303-141">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="b2303-141">**Details of the requirement:**</span></span>

<span data-ttu-id="b2303-142">预装以下组件，或者由分销点在设备上为客户安装这些组件：</span><span class="sxs-lookup"><span data-stu-id="b2303-142">The following components come pre-installed or at the point of distribution on the device to customer(s):</span></span>

-   <span data-ttu-id="b2303-143">Azure IoT Edge 安全守护程序</span><span class="sxs-lookup"><span data-stu-id="b2303-143">Azure IoT Edge Security Daemon</span></span>
-   <span data-ttu-id="b2303-144">守护程序配置文件</span><span class="sxs-lookup"><span data-stu-id="b2303-144">Daemon configuration file</span></span>
-   <span data-ttu-id="b2303-145">Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="b2303-145">Moby container management system</span></span>
-   <span data-ttu-id="b2303-146">版本 `hsmlib`</span><span class="sxs-lookup"><span data-stu-id="b2303-146">A version of `hsmlib`</span></span> 

<span data-ttu-id="b2303-147">启用 Edge 运行时：</span><span class="sxs-lookup"><span data-stu-id="b2303-147">*Edge Runtime Enabled:*</span></span>

<span data-ttu-id="b2303-148">**检查 iotedge 守护程序命令：**</span><span class="sxs-lookup"><span data-stu-id="b2303-148">**Check the iotedge daemon command:**</span></span> 

<span data-ttu-id="b2303-149">在 IoT Edge 设备上打开命令提示符，确认 Azure IoT Edge 守护程序处于“正在运行”状态</span><span class="sxs-lookup"><span data-stu-id="b2303-149">Open the command prompt on your IoT Edge device , confirm that the Azure IoT edge Daemon is under running state</span></span>

    systemctl status iotedge

 ![](./images/Capture.png)

<span data-ttu-id="b2303-150">在 IoT Edge 设备上打开命令提示符，确认从云中部署的模块正在 IoT Edge 设备上运行</span><span class="sxs-lookup"><span data-stu-id="b2303-150">Open the command prompt on your IoT Edge device, confirm that the module deployed from the cloud is running on your IoT Edge device</span></span>

    sudo iotedge list

 ![](./images/iotedgedaemon.png) 

<span data-ttu-id="b2303-151">在 Azure 的设备详细信息页面上，应当会看到运行时模块（edgeAgent、edgeHub 和 tempSensor 模块）处于“正在运行”状态</span><span class="sxs-lookup"><span data-stu-id="b2303-151">On the device details page of the Azure, you should see the runtime modules - edgeAgent, edgeHub and tempSensor modueles are under running status</span></span>

 ![](./images/tempSensor.png)

<a name="Step-3-2-DeviceManagement"></a>
## <a name="32-device-management-mandatory"></a><span data-ttu-id="b2303-152">3.2：设备管理（必需）</span><span class="sxs-lookup"><span data-stu-id="b2303-152">3.2 Device Management (Mandatory)</span></span>

<span data-ttu-id="b2303-153">**先决条件：** 设备连接。</span><span class="sxs-lookup"><span data-stu-id="b2303-153">**Pre-requisites:** Device Connectivity.</span></span>

<span data-ttu-id="b2303-154">**说明：** 可以执行由 IoT 中心发出的消息触发的基本设备管理操作（重启和固件更新）的设备。</span><span class="sxs-lookup"><span data-stu-id="b2303-154">**Description:** A device that can perform basic device management operations (Reboot and Firmware update) triggered by messages from IoT Hub.</span></span>

## <a name="321-firmware-update-using-microsoft-sdk-samples"></a><span data-ttu-id="b2303-155">3.2.1 固件更新（使用 Microsoft SDK 示例）：</span><span class="sxs-lookup"><span data-stu-id="b2303-155">3.2.1 Firmware Update (Using Microsoft SDK Samples):</span></span>

<span data-ttu-id="b2303-156">指定安装了 firmwareupdate 客户端组件的路径 {{输入路径}}。</span><span class="sxs-lookup"><span data-stu-id="b2303-156">Specify the path {{enter the path}} where the firmwareupdate client components are installed.</span></span>

<span data-ttu-id="b2303-157">若要运行模拟设备应用程序，请打开 shell 或命令提示符窗口，并导航到下载的 Node.js 项目中的 **iot-hub/Tutorials/FirmwareUpdate** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="b2303-157">To run the simulated device application, open a shell or command prompt window and navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="b2303-158">然后运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b2303-158">Then run the following commands:</span></span>

    npm install
    node SimulatedDevice.js "{your device connection string}"

<span data-ttu-id="b2303-159">若要运行后端应用程序，请打开另一个 shell 或命令提示符窗口。</span><span class="sxs-lookup"><span data-stu-id="b2303-159">To run the back-end application, open another shell or command prompt window.</span></span> <span data-ttu-id="b2303-160">导航到下载的 Node.js 项目中的 **iot-hub/Tutorials/FirmwareUpdate** 文件夹。</span><span class="sxs-lookup"><span data-stu-id="b2303-160">Then navigate to the **iot-hub/Tutorials/FirmwareUpdate** folder in the Node.js project you downloaded.</span></span> <span data-ttu-id="b2303-161">然后运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b2303-161">Then run the following commands:</span></span>

    npm install
    node ServiceClient.js "{your service connection string}"

<span data-ttu-id="b2303-162">IoT 设备客户端将得到消息并将状态报告给设备孪生。</span><span class="sxs-lookup"><span data-stu-id="b2303-162">IoT device client will get the message and report the status to the device twin.</span></span>

 ![](./images/devicetwin.png)

<span data-ttu-id="b2303-163">**更新固件**</span><span class="sxs-lookup"><span data-stu-id="b2303-163">**Update firmware**</span></span>

<span data-ttu-id="b2303-164">确认 IoT 中心、设备 ID、方法名称和方法有效负载，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2303-164">Confirm the IoT hub, Device ID, method name and method payload as below:</span></span>

-   <span data-ttu-id="b2303-165">按下“调用方法”按钮</span><span class="sxs-lookup"><span data-stu-id="b2303-165">Press “call Method” button</span></span>
-   <span data-ttu-id="b2303-166">检查返回状态，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2303-166">Check the returning status as below:</span></span>

 ![](./images/firmware.png)


## <a name="322-reboot-using-microsoft-sdk-samples"></a><span data-ttu-id="b2303-167">3.2.2 重启（使用 Microsoft SDK 示例）：</span><span class="sxs-lookup"><span data-stu-id="b2303-167">3.2.2 Reboot (Using Microsoft SDK Samples):</span></span>

<span data-ttu-id="b2303-168">指定安装了组件的路径 {{输入路径}}</span><span class="sxs-lookup"><span data-stu-id="b2303-168">Specify the path {{enter the path}} where the components are installed</span></span> 

<span data-ttu-id="b2303-169">确认 IoT 中心、设备 ID、方法名称，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2303-169">Confirm the IoT hub, Device ID, method name as below:</span></span>

-   <span data-ttu-id="b2303-170">按下“调用方法”按钮</span><span class="sxs-lookup"><span data-stu-id="b2303-170">Press “call Method” button</span></span>
-   <span data-ttu-id="b2303-171">检查返回状态，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2303-171">Check the returning status as below:</span></span>

 ![](./images/reboot.png)


<span data-ttu-id="b2303-172">IoT 设备客户端将得到消息并将状态报告给设备孪生。</span><span class="sxs-lookup"><span data-stu-id="b2303-172">IoT device client will get the message and report the status to the device twin.</span></span>

 ![](./images/devicetwinmessage.png)
  
## <a name="333-firmware-update-modified-sdk-samplescustom-made-application"></a><span data-ttu-id="b2303-173">3.3.3 固件更新（修改的 SDK 示例/定制的应用程序）：</span><span class="sxs-lookup"><span data-stu-id="b2303-173">3.3.3 Firmware Update (Modified SDK samples/Custom made application):</span></span>

<span data-ttu-id="b2303-174">如果客户端组件是定制的，请通过“设备孪生”添加步骤来执行固件更新。</span><span class="sxs-lookup"><span data-stu-id="b2303-174">If the Client components are custom made please add the steps to execute the Firmware Update through Device Twin.</span></span>

<span data-ttu-id="b2303-175">**注意**：设备必须附带客户端组件</span><span class="sxs-lookup"><span data-stu-id="b2303-175">**Note**: Client Components must be shipped with the device</span></span> 

## <a name="334-reboot-modified-sdk-samplescustom-made-application"></a><span data-ttu-id="b2303-176">3.3.4 重启（修改的 SDK 示例/定制的应用程序）：</span><span class="sxs-lookup"><span data-stu-id="b2303-176">3.3.4 Reboot (Modified SDK samples/Custom made application):</span></span>

<span data-ttu-id="b2303-177">如果客户端组件是定制的，请通过“直接方法”添加步骤来执行设备重启。</span><span class="sxs-lookup"><span data-stu-id="b2303-177">If the Client components are custom made please add the steps to execute the Device Reboot through Direct Methods</span></span>

<span data-ttu-id="b2303-178">**注意**：设备必须附带客户端组件</span><span class="sxs-lookup"><span data-stu-id="b2303-178">**Note**: Client Components must be shipped with the device</span></span> 

<a name="NextSteps"></a>
# <a name="step-4-next-steps"></a><span data-ttu-id="b2303-179">步骤 4：后续步骤</span><span class="sxs-lookup"><span data-stu-id="b2303-179">Step 4: Next steps</span></span>

<span data-ttu-id="b2303-180">与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。</span><span class="sxs-lookup"><span data-stu-id="b2303-180">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="b2303-181">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="b2303-181">Step 5: Troubleshooting</span></span>

<span data-ttu-id="b2303-182">如需故障排除的帮助，请通过 **<mailto:iotcert@microsoft.com>** 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="b2303-182">Please contact engineering support on **<mailto:iotcert@microsoft.com>** for help with troubleshooting.</span></span>
  
[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md
