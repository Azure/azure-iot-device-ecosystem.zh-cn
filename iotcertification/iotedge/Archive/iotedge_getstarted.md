# <a name="introduction"></a>介绍

**关于本文档**

感谢你对认证 Microsoft Azure IoT 设备的关注。 本文档提供 **Microsoft Azure IoT Edge 设备**认证（Azure IoT 认证计划的一部分）的概述。

Azure IoT 认证计划持续为 [IoT 设备](https://github.com/Azure/azure-iot-device-ecosystem/tree/master/iotcertification)和[初学者工具包](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/kits/iotcertification/iot_certification_kit.md)的现有认证要求提供支持。 该计划正在不断扩展，支持名为 **Azure IoT Edge** 设备的新设备类型；与其他 IoT 设备和初学者工具包相比，此类设备可提供更高的质量标准。

# <a name="device-prerequisites"></a>设备先决条件

IoT Edge 设备上需要预装 [Azure IoT Edge](https://github.com/Azure/iot-edge/blob/master/README.md) 运行时，这样才能将它认证为 Azure IoT Edge 设备。  可以在价值链中的多个阶段在设备上预装 IoT Edge 运行时。

-   在 OEM 或 ODM 生产地预装 IoT Edge 运行时。
-   在分销点预装 OEM 提供的 IoT Edge 运行时。 例如，分销商、增值经销商等任何渠道都可以安装 OEM 提供的 IoT Edge 运行时。
-   如果渠道在 OEM Edge 设备上安装特定于该渠道的 IoT Edge 运行时，则认证计划将接受提交内容，但会将它视为不同的提交实体。 在这种情况下，渠道和 OEM 需要议定[设备目录](https://catalog.azureiotsolutions.com/)中所述的有关品牌和设备名称等的细节。

Raspberry Pi3 等 IoT 设备可以继续运行 IoT Edge 运行时。 Azure IoT 认证计划将会针对 OEM 或渠道控制的设备中预装的、用于在 IoT Edge 设备上提供最佳开箱即用体验的 Edge 运行时进行认证。

# <a name="iot-edge-device-certification-program-overview"></a>IoT Edge 设备认证计划概述

IoT Edge 认证计划实行基于功能的认证概念。 每个功能具有自身的级别，提供设备客户寻求的 IoT Edge 设备粒度级，并允许 Azure IoT 认证计划在将来得到发展。

每个功能包含自身的级别，“级别 1”是最低级别。 

设备需要通过所有强制要求才能认证为 IoT Edge 设备：

-   [强制] Edge 运行时（仅限级别 1）
-   [强制] 设备管理（仅限级别 1）
-   [可选] 安全性（4 个级别：级别 1 - 4）

# <a name="certification-criteria-description-of-capabilities-and-levels"></a>认证条件：功能和级别的说明

下面描述了每个级别的 IoT Edge 设备认证条件和关联的功能：

**注意：** 目前我们仅针对 [T1 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support) 进行认证

-   Azure IoT Edge 运行时：设备应该能够运行 IoT Edge 运行时。

-   设备管理：IoT 中心发出的消息触发的基本设备管理操作（重启、FW/OS 升级）。

-   安全性：Azure IoT Edge 自始至终是安全的。  但是，需要使用安全硬件来实施安全措施，避免 Edge 设备上的操作造成其他威胁。  此项认证旨在贯彻以下理念：努力使安全性超越部署中使用 HSM 保护设备的 Azure IoT Edge 所提供的安全性。 以下功能描述设备缓解功能中存在的风险。 其中既未提供安全保证，也未对安全强度做出表述。 

    ![](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/iotedge/images/1.PNG)


    ![](https://github.com/Azure/azure-iot-device-ecosystem/blob/master/iotcertification/iotedge/images/2.PNG)

请在 [Securing the intelligent edge](https://azure.microsoft.com/en-us/blog/securing-the-intelligent-edge/)（保护智能边缘）博客文章中了解 Microsoft 通过哪种方式为 Azure IoT Edge 设备提供安全平台。 Microsoft 正在致力于定义安全要求方面的验证过程，包括审查第三方验证实验室的使用。

请单击[此处](https://github.com/Azure/azure-iotedge/blob/master/LICENSE)以查看 IoT Edge 运行时的 MICROSOFT 软件许可条款

# <a name="next-steps"></a>后续步骤

现在，你已了解正在扩展为支持 Azure IoT Edge 设备的 Azure IoT 认证计划的概述。

接下来请详细了解认证为 Azure IoT Edge 设备所要满足的具体要求以及验证过程。 

如有任何疑问，请通过 [iotcert@microsoft.com](mailto:iotcert@microsoft.com) 联系 Azure IoT 认证部门。
