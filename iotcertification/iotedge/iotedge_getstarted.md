# <a name="introduction"></a><span data-ttu-id="08710-101">介绍</span><span class="sxs-lookup"><span data-stu-id="08710-101">Introduction</span></span>

<span data-ttu-id="08710-102">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="08710-102">**About this document**</span></span>

<span data-ttu-id="08710-103">感谢你对认证 Microsoft Azure IoT 设备的关注。</span><span class="sxs-lookup"><span data-stu-id="08710-103">Thank you for your interest in certifying your Microsoft Azure IoT Edge device.</span></span> <span data-ttu-id="08710-104">本文档提供 **Microsoft Azure IoT Edge 设备**认证（Azure IoT 认证计划的一部分）的概述。</span><span class="sxs-lookup"><span data-stu-id="08710-104">This document provides an overview of **Microsoft Azure IoT Edge device** certification, which is part of the Azure Certified for IoT program.</span></span>

<span data-ttu-id="08710-105">Azure IoT 认证计划持续为 [IoT 设备](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/iotcertification)和[初学者工具包](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/kits/iotcertification/iot_certification_kit.md)的现有认证要求提供支持。</span><span class="sxs-lookup"><span data-stu-id="08710-105">Azure Certified for IoT program continues to support the existing certification requirements for [IoT devices](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/iotcertification) and [Starter kits](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/kits/iotcertification/iot_certification_kit.md).</span></span> <span data-ttu-id="08710-106">该计划正在不断扩展，支持名为 **Azure IoT Edge** 设备的新设备类型；与其他 IoT 设备和初学者工具包相比，此类设备可提供更高的质量标准。</span><span class="sxs-lookup"><span data-stu-id="08710-106">The program is extending to support a new device type named **Azure IoT Edge** device which provides higher quality standards than the other IoT devices and Starter kits.</span></span>

# <a name="device-prerequisites"></a><span data-ttu-id="08710-107">设备先决条件</span><span class="sxs-lookup"><span data-stu-id="08710-107">Device Prerequisites</span></span>

<span data-ttu-id="08710-108">IoT Edge 设备上需要预装 [Azure IoT Edge](https://github.com/Azure/iot-edge/blob/master/README.md) 运行时，这样才能将它认证为 Azure IoT Edge 设备。</span><span class="sxs-lookup"><span data-stu-id="08710-108">Your IoT Edge device is required to pre-install [Azure IoT Edge](https://github.com/Azure/iot-edge/blob/master/README.md) runtime to be certified as Azure IoT Edge device.</span></span>  <span data-ttu-id="08710-109">可以在价值链中的多个阶段在设备上预装 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="08710-109">Pre-installing IoT Edge runtime in your device can occur at multiple stages in value chain.</span></span>

-   <span data-ttu-id="08710-110">在 OEM 或 ODM 生产地预装 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="08710-110">Pre-install IoT Edge runtime at the OEM or ODM manufacturing facility.</span></span>
-   <span data-ttu-id="08710-111">在分销点预装 OEM 提供的 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="08710-111">Pre-install IoT Edge runtime that is supplied by OEM at the point of distribution.</span></span> <span data-ttu-id="08710-112">例如，分销商、增值经销商等任何渠道都可以安装 OEM 提供的 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="08710-112">This is the scenario where any channels such as distributor(s), value-added reseller(s) etc. installs OEM supplied IoT Edge runtime.</span></span>
-   <span data-ttu-id="08710-113">如果渠道在 OEM Edge 设备上安装特定于该渠道的 IoT Edge 运行时，则认证计划将接受提交内容，但会将它视为不同的提交实体。</span><span class="sxs-lookup"><span data-stu-id="08710-113">If the channel takes OEM Edge device, and installs the channel specific IoT Edge runtime, the program accepts the submission as a different submission entity.</span></span> <span data-ttu-id="08710-114">在这种情况下，渠道和 OEM 需要议定[设备目录](https://catalog.azureiotsolutions.com/)中所述的有关品牌和设备名称等的细节。</span><span class="sxs-lookup"><span data-stu-id="08710-114">In this case, the channel and OEM needs to agree on specifics on branding, device names etc that are shown in [device catalog](https://catalog.azureiotsolutions.com/).</span></span>

<span data-ttu-id="08710-115">Raspberry Pi3 等 IoT 设备可以继续运行 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="08710-115">IoT devices like Raspberry Pi3 etc can continue to run IoT Edge runtime.</span></span> <span data-ttu-id="08710-116">Azure IoT 认证计划将会针对 OEM 或渠道控制的设备中预装的、用于在 IoT Edge 设备上提供最佳开箱即用体验的 Edge 运行时进行认证。</span><span class="sxs-lookup"><span data-stu-id="08710-116">Azure Certified for IoT program is certifying against the pre-installed Edge runtime in the device controlled by either OEMs or channels to provide the best out-of-the-box experience on IoT Edge devices.</span></span>

# <a name="iot-edge-device-certification-program-overview"></a><span data-ttu-id="08710-117">IoT Edge 设备认证计划概述</span><span class="sxs-lookup"><span data-stu-id="08710-117">IoT Edge Device certification program overview</span></span>

<span data-ttu-id="08710-118">IoT Edge 认证计划实行基于功能的认证概念。</span><span class="sxs-lookup"><span data-stu-id="08710-118">IoT Edge certification program has the capability-based certification concept.</span></span> <span data-ttu-id="08710-119">每个功能具有自身的级别，提供设备客户寻求的 IoT Edge 设备粒度级，并允许 Azure IoT 认证计划在将来得到发展。</span><span class="sxs-lookup"><span data-stu-id="08710-119">Each capability has its own level to provide granularity of the IoT Edge device that device seekers are looking for, and allows the Azure Certified for IoT program to evolve in the future.</span></span>

<span data-ttu-id="08710-120">每个功能包含自身的级别，“级别 1”是最低级别。</span><span class="sxs-lookup"><span data-stu-id="08710-120">Each capability contains its own leveling with **Level 1** being the lowest.</span></span> 

<span data-ttu-id="08710-121">设备需要通过所有强制要求才能认证为 IoT Edge 设备：</span><span class="sxs-lookup"><span data-stu-id="08710-121">For the device to be certified as IoT Edge device, the device needs to pass all mandatory requirements:</span></span>

-   <span data-ttu-id="08710-122">[强制] Edge 运行时（仅限级别 1）</span><span class="sxs-lookup"><span data-stu-id="08710-122">[Mandatory] Edge runtime (Level 1 only)</span></span>
-   <span data-ttu-id="08710-123">[可选] 设备管理（仅限级别 1）</span><span class="sxs-lookup"><span data-stu-id="08710-123">[Optional] Device management (Level 1 only)</span></span>

# <a name="certification-criteria-description-of-capabilities-and-levels"></a><span data-ttu-id="08710-124">认证条件：功能和级别的说明</span><span class="sxs-lookup"><span data-stu-id="08710-124">Certification Criteria: Description of capabilities and levels</span></span>

<span data-ttu-id="08710-125">下面描述了每个级别的 IoT Edge 设备认证条件和关联的功能：</span><span class="sxs-lookup"><span data-stu-id="08710-125">Below describes the IoT Edge device certification criteria and associated capabilities for each level:</span></span>

<span data-ttu-id="08710-126">**注意：** 目前我们仅针对 [T1 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support) 进行认证</span><span class="sxs-lookup"><span data-stu-id="08710-126">**Note:** Currently we only certify against [T1 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support)</span></span>

-   <span data-ttu-id="08710-127">Azure IoT Edge 运行时：设备应该能够运行 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="08710-127">Azure IoT Edge Runtime:  Device should be capable of running IoT Edge Runtime.</span></span>

-   <span data-ttu-id="08710-128">设备管理：IoT 中心发出的消息触发的基本设备管理操作（重启、FW/OS 升级）。</span><span class="sxs-lookup"><span data-stu-id="08710-128">Device management: Basic device management operations (reboot, FW/OS upgrades) triggered by messages from IoT Hub.</span></span>

<span data-ttu-id="08710-129">请单击[此处](https://github.com/Azure/azure-iotedge/blob/master/LICENSE)以查看 IoT Edge 运行时的 MICROSOFT 软件许可条款</span><span class="sxs-lookup"><span data-stu-id="08710-129">Please click [here](https://github.com/Azure/azure-iotedge/blob/master/LICENSE) for MICROSOFT SOFTWARE LICENSE TERMS for IoT Edge runtime</span></span>

# <a name="next-steps"></a><span data-ttu-id="08710-130">后续步骤</span><span class="sxs-lookup"><span data-stu-id="08710-130">Next steps</span></span>

<span data-ttu-id="08710-131">现在，你已了解正在扩展为支持 Azure IoT Edge 设备的 Azure IoT 认证计划的概述。</span><span class="sxs-lookup"><span data-stu-id="08710-131">You have now learned about the overview of Azure Certified for IoT program extending to support Azure IoT Edge devices.</span></span>

<span data-ttu-id="08710-132">接下来请详细了解认证为 Azure IoT Edge 设备所要满足的具体要求以及验证过程。</span><span class="sxs-lookup"><span data-stu-id="08710-132">Read more details about specific requirements and validation process to be certified as Azure IoT Edge devices.</span></span> 

<span data-ttu-id="08710-133">如有任何疑问，请通过 [iotcert@microsoft.com](mailto:iotcert@microsoft.com) 联系 Azure IoT 认证部门。</span><span class="sxs-lookup"><span data-stu-id="08710-133">If you have any questions, please contact Azure Certified for IoT [iotcert@microsoft.com](mailto:iotcert@microsoft.com).</span></span>
