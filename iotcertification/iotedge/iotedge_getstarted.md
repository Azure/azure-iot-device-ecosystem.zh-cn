# <a name="introduction"></a><span data-ttu-id="ed067-101">介绍</span><span class="sxs-lookup"><span data-stu-id="ed067-101">Introduction</span></span>

<span data-ttu-id="ed067-102">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="ed067-102">**About this document**</span></span>

<span data-ttu-id="ed067-103">感谢你对认证 Microsoft Azure IoT 设备的关注。</span><span class="sxs-lookup"><span data-stu-id="ed067-103">Thank you for your interest in certifying your Microsoft Azure IoT Edge device.</span></span> <span data-ttu-id="ed067-104">本文档提供 **Microsoft Azure IoT Edge 设备**认证（Azure IoT 认证计划的一部分）的概述。</span><span class="sxs-lookup"><span data-stu-id="ed067-104">This document provides an overview of **Microsoft Azure IoT Edge device** certification, which is part of the Azure Certified for IoT program.</span></span>

<span data-ttu-id="ed067-105">Azure IoT 认证计划持续为 [IoT 设备](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/iotcertification)和[初学者工具包](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/kits/iotcertification/iot_certification_kit.md)的现有认证要求提供支持。</span><span class="sxs-lookup"><span data-stu-id="ed067-105">Azure Certified for IoT program continues to support the existing certification requirements for [IoT devices](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/iotcertification) and [Starter kits](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/kits/iotcertification/iot_certification_kit.md).</span></span> <span data-ttu-id="ed067-106">该计划正在不断扩展，支持名为 **Azure IoT Edge** 设备的新设备类型；与其他 IoT 设备和初学者工具包相比，此类设备可提供更高的质量标准。</span><span class="sxs-lookup"><span data-stu-id="ed067-106">The program is extending to support a new device type named **Azure IoT Edge** device which provides higher quality standards than the other IoT devices and Starter kits.</span></span>

# <a name="device-prerequisites"></a><span data-ttu-id="ed067-107">设备先决条件</span><span class="sxs-lookup"><span data-stu-id="ed067-107">Device Prerequisites</span></span>

<span data-ttu-id="ed067-108">IoT Edge 设备上需要预装 [Azure IoT Edge](https://github.com/Azure/iot-edge/blob/master/README.md) 运行时，这样才能将它认证为 Azure IoT Edge 设备。</span><span class="sxs-lookup"><span data-stu-id="ed067-108">Your IoT Edge device is required to pre-install [Azure IoT Edge](https://github.com/Azure/iot-edge/blob/master/README.md) runtime to be certified as Azure IoT Edge device.</span></span>  <span data-ttu-id="ed067-109">可以在价值链中的多个阶段在设备上预装 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="ed067-109">Pre-installing IoT Edge runtime in your device can occur at multiple stages in value chain.</span></span>

-   <span data-ttu-id="ed067-110">在 OEM 或 ODM 生产地预装 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="ed067-110">Pre-install IoT Edge runtime at the OEM or ODM manufacturing facility.</span></span>
-   <span data-ttu-id="ed067-111">在分销点预装 OEM 提供的 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="ed067-111">Pre-install IoT Edge runtime that is supplied by OEM at the point of distribution.</span></span> <span data-ttu-id="ed067-112">例如，分销商、增值经销商等任何渠道都可以安装 OEM 提供的 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="ed067-112">This is the scenario where any channels such as distributor(s), value-added reseller(s) etc. installs OEM supplied IoT Edge runtime.</span></span>
-   <span data-ttu-id="ed067-113">如果渠道在 OEM Edge 设备上安装特定于该渠道的 IoT Edge 运行时，则认证计划将接受提交内容，但会将它视为不同的提交实体。</span><span class="sxs-lookup"><span data-stu-id="ed067-113">If the channel takes OEM Edge device, and installs the channel specific IoT Edge runtime, the program accepts the submission as a different submission entity.</span></span> <span data-ttu-id="ed067-114">在这种情况下，渠道和 OEM 需要议定[设备目录](https://catalog.azureiotsolutions.com/)中所述的有关品牌和设备名称等的细节。</span><span class="sxs-lookup"><span data-stu-id="ed067-114">In this case, the channel and OEM needs to agree on specifics on branding, device names etc that are shown in [device catalog](https://catalog.azureiotsolutions.com/).</span></span>

<span data-ttu-id="ed067-115">Raspberry Pi3 等 IoT 设备可以继续运行 IoT Edge 运行时。</span><span class="sxs-lookup"><span data-stu-id="ed067-115">IoT devices like Raspberry Pi3 etc can continue to run IoT Edge runtime.</span></span> <span data-ttu-id="ed067-116">Azure IoT 认证计划将会针对 OEM 或渠道控制的设备中预装的、用于在 IoT Edge 设备上提供最佳开箱即用体验的 Edge 运行时进行认证。</span><span class="sxs-lookup"><span data-stu-id="ed067-116">Azure Certified for IoT program is certifying against the pre-installed Edge runtime in the device controlled by either OEMs or channels to provide the best out-of-the-box experience on IoT Edge devices.</span></span>

# <a name="iot-edge-device-certification-program-overview"></a><span data-ttu-id="ed067-117">IoT Edge 设备认证计划概述</span><span class="sxs-lookup"><span data-stu-id="ed067-117">IoT Edge Device certification program overview</span></span>

<span data-ttu-id="ed067-118">IoT Edge 认证计划实行基于功能的认证概念。</span><span class="sxs-lookup"><span data-stu-id="ed067-118">IoT Edge certification program has the capability-based certification concept.</span></span> <span data-ttu-id="ed067-119">每个功能具有自身的级别，提供设备客户寻求的 IoT Edge 设备粒度级，并允许 Azure IoT 认证计划在将来得到发展。</span><span class="sxs-lookup"><span data-stu-id="ed067-119">Each capability has its own level to provide granularity of the IoT Edge device that device seekers are looking for, and allows the Azure Certified for IoT program to evolve in the future.</span></span>

<span data-ttu-id="ed067-120">每个功能包含自身的级别，“级别 1”是最低级别。</span><span class="sxs-lookup"><span data-stu-id="ed067-120">Each capability contains its own leveling with **Level 1** being the lowest.</span></span> 

<span data-ttu-id="ed067-121">设备需要通过所有强制要求才能认证为 IoT Edge 设备：</span><span class="sxs-lookup"><span data-stu-id="ed067-121">For the device to be certified as IoT Edge device, the device needs to pass all mandatory requirements:</span></span>

-   <span data-ttu-id="ed067-122">[强制] Edge 运行时（仅限级别 1）</span><span class="sxs-lookup"><span data-stu-id="ed067-122">[Mandatory] Edge runtime (Level 1 only)</span></span>
-   <span data-ttu-id="ed067-123">[强制] 设备管理（仅限级别 1）</span><span class="sxs-lookup"><span data-stu-id="ed067-123">[Mandatory] Device management (Level 1 only)</span></span>
-   <span data-ttu-id="ed067-124">[可选] 安全性（4 个级别：级别 1 - 4）</span><span class="sxs-lookup"><span data-stu-id="ed067-124">[Optional] Security (4 levels: Level 1 – 4)</span></span>

# <a name="certification-criteria-description-of-capabilities-and-levels"></a><span data-ttu-id="ed067-125">认证条件：功能和级别的说明</span><span class="sxs-lookup"><span data-stu-id="ed067-125">Certification Criteria: Description of capabilities and levels</span></span>

<span data-ttu-id="ed067-126">下面描述了每个级别的 IoT Edge 设备认证条件和关联的功能：</span><span class="sxs-lookup"><span data-stu-id="ed067-126">Below describes the IoT Edge device certification criteria and associated capabilities for each level:</span></span>

-   <span data-ttu-id="ed067-127">设备管理：IoT 中心发出的消息触发的基本设备管理操作（重新启动、FW/OS 升级）。</span><span class="sxs-lookup"><span data-stu-id="ed067-127">Device management: Basic device management operations (reboot, FW/OS upgrades) triggered by messages from IoT Hub.</span></span>

-   <span data-ttu-id="ed067-128">安全性：Azure IoT Edge 自始至终是安全的。</span><span class="sxs-lookup"><span data-stu-id="ed067-128">Security: Azure IoT Edge is secure from the ground up.</span></span>  <span data-ttu-id="ed067-129">但是，需要使用安全硬件来实施安全措施，避免 Edge 设备上的操作造成其他威胁。</span><span class="sxs-lookup"><span data-stu-id="ed067-129">However, additional threats with operating at the edge demands security enforcements using secure hardware.</span></span>  <span data-ttu-id="ed067-130">此项认证旨在贯彻以下理念：努力使安全性超越部署中使用 HSM 保护设备的 Azure IoT Edge 所提供的安全性。</span><span class="sxs-lookup"><span data-stu-id="ed067-130">This certification aims to communicate diligence to security above and beyond that provided by Azure IoT Edge as in deployment using HSM secured devices.</span></span> <span data-ttu-id="ed067-131">以下功能描述设备缓解功能中存在的风险。</span><span class="sxs-lookup"><span data-stu-id="ed067-131">The below capabilities describe the risks within the devices mitigation capabilities.</span></span> <span data-ttu-id="ed067-132">其中既未提供安全保证，也未对安全强度做出表述。</span><span class="sxs-lookup"><span data-stu-id="ed067-132">It is neither a security guarantee nor a statement of the strength of security.</span></span> 

    ![](images/1.PNG)


    ![](images/2.PNG)

<span data-ttu-id="ed067-133">请在 [Securing the intelligent edge](https://azure.microsoft.com/en-us/blog/securing-the-intelligent-edge/)（保护智能边缘）博客文章中了解 Microsoft 通过哪种方式为 Azure IoT Edge 设备提供安全平台。</span><span class="sxs-lookup"><span data-stu-id="ed067-133">Read Microsoft’s approach to deliver a secure platform for Azure IoT Edge devices in [Securing the intelligent edge](https://azure.microsoft.com/en-us/blog/securing-the-intelligent-edge/) blog.</span></span> <span data-ttu-id="ed067-134">Microsoft 正在致力于定义安全要求方面的验证过程，包括审查第三方验证实验室的使用。</span><span class="sxs-lookup"><span data-stu-id="ed067-134">Microsoft is working on to define validation process for security requirement including exploration of leveraging 3rd party validation labs.</span></span>

# <a name="next-steps"></a><span data-ttu-id="ed067-135">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ed067-135">Next steps</span></span>

<span data-ttu-id="ed067-136">现在，你已了解正在扩展为支持 Azure IoT Edge 设备的 Azure IoT 认证计划的概述。</span><span class="sxs-lookup"><span data-stu-id="ed067-136">You have now learned about the overview of Azure Certified for IoT program extending to support Azure IoT Edge devices.</span></span>

<span data-ttu-id="ed067-137">接下来请详细了解认证为 Azure IoT Edge 设备所要满足的具体要求以及验证过程。</span><span class="sxs-lookup"><span data-stu-id="ed067-137">Read more details about specific requirements and validation process to be certified as Azure IoT Edge devices.</span></span> 

<span data-ttu-id="ed067-138">如有任何疑问，请通过 [iotcert@microsoft.com](mailto:iotcert@microsoft.com) 联系 Azure IoT 认证部门。</span><span class="sxs-lookup"><span data-stu-id="ed067-138">If you have any questions, please contact Azure Certified for IoT [iotcert@microsoft.com](mailto:iotcert@microsoft.com).</span></span>

