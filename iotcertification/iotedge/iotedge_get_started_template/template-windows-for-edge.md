---
platform:
  enter the OS name running on edge device: 
device:
  enter your device name here: 
language:
  enter the language used to you edge device: 
ms.openlocfilehash: 22db77d2bf8b8194d07257118d3ba47a39768ea0
ms.sourcegitcommit: 27194ccdf98e5e8864505485c8a169cc747cd30c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68862369"
---
<span data-ttu-id="799a7-101">*强烈建议使此文档保持最新，如果文档包含损坏的 URL 链接、不正确的信息等等，请记住，Microsoft 预留了从 Azure IoT 设备目录中删除设备和文档的权利。*</span><span class="sxs-lookup"><span data-stu-id="799a7-101">*We highly recommend keeping this document current, and Microsoft reserves a right to remove devices and documents from the Azure IoT Device Catalog if document contains broken URL links, incorrect information etc.*</span></span>

<a name="run-a-simple-enter-the-language-used-to-you-edge-device-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-edge-device-specify-distribution-or-windows-sku-information-ex-ubuntu-sever-1604-windows-10-iot-core-only-tier-1-oshttpsdocsmicrosoftcomen-usazureiot-edgesupport-is-allowed"></a><span data-ttu-id="799a7-102">在运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 {输入用于 Edge 设备的语言} 示例。</span><span class="sxs-lookup"><span data-stu-id="799a7-102">Run a simple {enter the language used to you edge device} sample on {enter your device name here} device running {enter the OS name running on edge device.</span></span> <span data-ttu-id="799a7-103">指定发行版或 Windows SKU 信息。</span><span class="sxs-lookup"><span data-stu-id="799a7-103">Specify distribution or Windows SKU information.</span></span> <span data-ttu-id="799a7-104">例如：Ubuntu Sever 16.04、Windows 10 IoT 核心版。</span><span class="sxs-lookup"><span data-stu-id="799a7-104">Ex: Ubuntu Sever 16.04, Windows 10 IoT Core.</span></span> <span data-ttu-id="799a7-105">仅允许[第 1 层 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support)。</span><span class="sxs-lookup"><span data-stu-id="799a7-105">Only [Tier 1 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support) is allowed}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="799a7-106">目录</span><span class="sxs-lookup"><span data-stu-id="799a7-106">Table of Contents</span></span>

-   [<span data-ttu-id="799a7-107">介绍</span><span class="sxs-lookup"><span data-stu-id="799a7-107">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="799a7-108">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="799a7-108">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="799a7-109">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="799a7-109">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="799a7-110">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="799a7-110">Step 3: Manual Test for Azure IoT Edge on device</span></span>](#Manual)
-   [<span data-ttu-id="799a7-111">步骤 4：后续步骤</span><span class="sxs-lookup"><span data-stu-id="799a7-111">Step 4: Next Steps</span></span>](#NextSteps)
-   [<span data-ttu-id="799a7-112">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="799a7-112">Step 5: Troubleshooting</span></span>](#Step-5-Troubleshooting)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="799a7-113">此模板的用法说明</span><span class="sxs-lookup"><span data-stu-id="799a7-113">Instructions for using this template</span></span>

-   <span data-ttu-id="799a7-114">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="799a7-114">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="799a7-115">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="799a7-115">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="799a7-116">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="799a7-116">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="799a7-117">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="799a7-117">Remove this section from final document.</span></span>

<a name="Introduction"></a>
# <a name="introduction"></a><span data-ttu-id="799a7-118">介绍</span><span class="sxs-lookup"><span data-stu-id="799a7-118">Introduction</span></span>

<span data-ttu-id="799a7-119">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="799a7-119">**About this document**</span></span>

<span data-ttu-id="799a7-120">本文档介绍了如何使用预先安装的 Azure IoT Edge 运行时和“设备管理”来连接运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="799a7-120">This document describes how to connect {enter your device name here} device running {enter the OS name running on edge device} with Azure IoT Edge Runtime pre-installed and Device Management.</span></span> <span data-ttu-id="799a7-121">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="799a7-121">This multi-step process includes:</span></span>

-   <span data-ttu-id="799a7-122">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="799a7-122">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="799a7-123">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="799a7-123">Registering your IoT device</span></span>
-   <span data-ttu-id="799a7-124">构建并部署客户端组件来测试设备管理功能</span><span class="sxs-lookup"><span data-stu-id="799a7-124">Build and Deploy client component to test device management capability</span></span> 

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="799a7-125">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="799a7-125">Step 1: Prerequisites</span></span>

<span data-ttu-id="799a7-126">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="799a7-126">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="799a7-127">[准备开发环境][setup-devbox-windows]</span><span class="sxs-lookup"><span data-stu-id="799a7-127">[Prepare your development environment][setup-devbox-windows]</span></span>
-   [<span data-ttu-id="799a7-128">设置 IoT 中心</span><span class="sxs-lookup"><span data-stu-id="799a7-128">Setup your IoT hub</span></span>](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   <span data-ttu-id="799a7-129">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="799a7-129">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   [<span data-ttu-id="799a7-130">注册到 IOT 中心</span><span class="sxs-lookup"><span data-stu-id="799a7-130">Sign up to IOT Hub</span></span>](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   [<span data-ttu-id="799a7-131">添加 Edge 设备</span><span class="sxs-lookup"><span data-stu-id="799a7-131">Add the Edge Device</span></span>](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart)
-   [<span data-ttu-id="799a7-132">添加 Edge 模块</span><span class="sxs-lookup"><span data-stu-id="799a7-132">Add the Edge Modules</span></span>](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart#deploy-a-module)
-   <span data-ttu-id="799a7-133">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="799a7-133">{enter your device name here} device.</span></span>
-   <span data-ttu-id="799a7-134">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="799a7-134">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="799a7-135">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="799a7-135">Step 2: Prepare your Device</span></span>

-   <span data-ttu-id="799a7-136">{{记下安装、配置和连接设备时需要遵循的说明。</span><span class="sxs-lookup"><span data-stu-id="799a7-136">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="799a7-137">请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}</span><span class="sxs-lookup"><span data-stu-id="799a7-137">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a><span data-ttu-id="799a7-138">步骤 3：在设备上对 Azure IoT Edge 进行手动测试</span><span class="sxs-lookup"><span data-stu-id="799a7-138">Step 3: Manual Test for Azure IoT Edge on device</span></span>

<span data-ttu-id="799a7-139">本部分将引导你在运行 Windows 操作系统的 Edge 设备上执行测试，从而使该设备符合 Azure IoT Edge 认证的要求。</span><span class="sxs-lookup"><span data-stu-id="799a7-139">This section walks you through the test to be performed on the Edge devices running the Windows operating system such that it can qualify for Azure IoT Edge certification.</span></span>

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a><span data-ttu-id="799a7-140">3.1：Edge RuntimeEnabled（必需）</span><span class="sxs-lookup"><span data-stu-id="799a7-140">3.1 Edge RuntimeEnabled (Mandatory)</span></span>

<span data-ttu-id="799a7-141">**要求详细信息：**</span><span class="sxs-lookup"><span data-stu-id="799a7-141">**Details of the requirement:**</span></span>

<span data-ttu-id="799a7-142">预装以下组件，或者由分销点在设备上为客户安装这些组件：</span><span class="sxs-lookup"><span data-stu-id="799a7-142">The following components come pre-installed or at the point of distribution on the device to customer(s):</span></span>

-   <span data-ttu-id="799a7-143">Azure IoT Edge 安全守护程序</span><span class="sxs-lookup"><span data-stu-id="799a7-143">Azure IoT Edge Security Daemon</span></span>
-   <span data-ttu-id="799a7-144">守护程序配置文件</span><span class="sxs-lookup"><span data-stu-id="799a7-144">Daemon configuration file</span></span>
-   <span data-ttu-id="799a7-145">Moby 容器管理系统</span><span class="sxs-lookup"><span data-stu-id="799a7-145">Moby container management system</span></span>
-   <span data-ttu-id="799a7-146">版本 `hsmlib`</span><span class="sxs-lookup"><span data-stu-id="799a7-146">A version of `hsmlib`</span></span> 

<span data-ttu-id="799a7-147">启用 Edge 运行时： </span><span class="sxs-lookup"><span data-stu-id="799a7-147">*Edge Runtime Enabled:*</span></span>

<span data-ttu-id="799a7-148">在 IoT Edge 设备上打开 Powershell，确认 IoT Edge 服务的状态。</span><span class="sxs-lookup"><span data-stu-id="799a7-148">Open the powershell on your IoT Edge device , confirm the status of the IoT Edge service.</span></span>

    Get-Service iotedge

<span data-ttu-id="799a7-149">检查过去 5 分钟的服务日志。</span><span class="sxs-lookup"><span data-stu-id="799a7-149">Examine service logs from the last 5 minutes.</span></span> <span data-ttu-id="799a7-150">如果刚完成了 IoT Edge 运行时的安装，则可能会在运行 **Deploy-IoTEdge** 和**Initialize-IoTEdge** 之间看到一系列的错误。</span><span class="sxs-lookup"><span data-stu-id="799a7-150">If you just finished installing the IoT Edge runtime, you may see a list of errors from the time between running **Deploy-IoTEdge** and **Initialize-IoTEdge**.</span></span> <span data-ttu-id="799a7-151">这些错误是预期的错误，因为服务在配置前尝试启动。</span><span class="sxs-lookup"><span data-stu-id="799a7-151">These errors are expected, as the service is trying to start before being configured.</span></span> 

    . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; Get-IoTEdgeLog

<span data-ttu-id="799a7-152">列出正在运行的模块。</span><span class="sxs-lookup"><span data-stu-id="799a7-152">List running modules.</span></span> <span data-ttu-id="799a7-153">在全新安装之后，应该看到运行的唯一模块是 **edgeAgent**。</span><span class="sxs-lookup"><span data-stu-id="799a7-153">After a new installation, the only module you should see running is **edgeAgent**.</span></span> <span data-ttu-id="799a7-154">[部署 IoT Edge 模块](how-to-deploy-modules-portal.md)后，你将看到其他模块。</span><span class="sxs-lookup"><span data-stu-id="799a7-154">After you [deploy IoT Edge modules](how-to-deploy-modules-portal.md), you will see others.</span></span> 

    iotedge list

![](images/edgemodule_status.PNG)

<span data-ttu-id="799a7-155">查看从你创建的模块发送到云的消息。</span><span class="sxs-lookup"><span data-stu-id="799a7-155">View the messages being sent from the module you created to the cloud.</span></span>

    iotedge logs {module name}

![](images/edgemodule_logs.PNG)

<a name="NextSteps"></a>
# <a name="step-4-next-steps"></a><span data-ttu-id="799a7-156">步骤 4：后续步骤</span><span class="sxs-lookup"><span data-stu-id="799a7-156">Step 4: Next steps</span></span>

<span data-ttu-id="799a7-157">与我们共享文档后，我们将在 48 到 72 个小时（营业时间）内与你取得联系，到时会告知后续步骤。</span><span class="sxs-lookup"><span data-stu-id="799a7-157">Once you shared the documents with us, we will contact you in the following 48 to 72 business hours with next steps.</span></span>

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a><span data-ttu-id="799a7-158">步骤 5：故障排除</span><span class="sxs-lookup"><span data-stu-id="799a7-158">Step 5: Troubleshooting</span></span>

<span data-ttu-id="799a7-159">如需故障排除的帮助，请通过 **<mailto:iotcert@microsoft.com>** 联系工程支持部门。</span><span class="sxs-lookup"><span data-stu-id="799a7-159">Please contact engineering support on **<mailto:iotcert@microsoft.com>** for help with troubleshooting.</span></span>
  
[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md
