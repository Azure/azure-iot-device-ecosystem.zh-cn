---
platform:
  enter the OS name running on edge device: 
device:
  enter your device name here: 
language:
  enter the language used to you edge device: 
ms.openlocfilehash: 8caacd02385cde10b4830926d09accb5243dd4a3
ms.sourcegitcommit: aa21feba9737583dca35278c8cf3fa302a130b31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2019
ms.locfileid: "56334242"
---
*强烈建议使此文档保持最新，如果文档包含损坏的 URL 链接、不正确的信息等等，请记住，Microsoft 预留了从 Azure IoT 设备目录中删除设备和文档的权利。*

<a name="run-a-simple-enter-the-language-used-to-you-edge-device-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-edge-device-specify-distribution-or-windows-sku-information-ex-ubuntu-sever-1604-windows-10-iot-core-only-tier-1-oshttpsdocsmicrosoftcomen-usazureiot-edgesupport-is-allowed"></a>在运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 {输入用于 Edge 设备的语言} 示例。 指定发行版或 Windows SKU 信息。 例如：Ubuntu Sever 16.04、Windows 10 IoT 核心版。 仅允许[第 1 层 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support)。
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：在设备上对 Azure IoT Edge 进行手动测试](#Manual)
-   [步骤 4：后续步骤](#NextSteps)
-   [步骤 5：故障排除](#Step-5-Troubleshooting)

# <a name="instructions-for-using-this-template"></a>有关使用此模板的说明

-   将 {placeholders} 中的文本替换为正确的值。
-   遵照 {{enclosed}} 行之间的说明后，删除这些行。
-   建议尽量使用外部链接。
-   请从最终文档中删除本部分。

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档介绍了如何使用预先安装的 Azure IoT Edge 运行时和“设备管理”来连接运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备。 此过程由多个步骤构成，具体包括：

-   配置 Azure IoT 中心
-   注册 IoT 设备
-   构建并部署客户端组件来测试设备管理功能 

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a>步骤 1：先决条件

在开始过程前，应已准备好以下项目：

-   [准备开发环境][setup-devbox-linux]
-   [设置 IoT 中心](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   [注册到 IOT 中心](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   [添加 Edge 设备](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux)
-   [添加 Edge 模块](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#deploy-a-module)
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备

-   {{写下安装、配置和连接设备所要遵照的说明。 请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}

<a name="Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a>步骤 3：在设备上对 Azure IoT Edge 进行手动测试

本部分将引导你在运行 Linux 操作系统的 Edge 设备上执行测试，使该设备符合 Azure IoT Edge 认证的要求。

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a>3.1：Edge RuntimeEnabled（必需）

**要求详细信息：**

预装以下组件，或者由分销点在设备上为客户安装这些组件：

-   Azure IoT Edge 安全守护程序
-   守护程序配置文件
-   Moby 容器管理系统
-   版本 `hsmlib` 

启用 Edge 运行时：

**检查 iotedge 守护程序命令：** 

在 IoT Edge 设备上打开命令提示符，确认 Azure IoT Edge 守护程序处于“正在运行”状态

    systemctl status iotedge

 ![](./images/Capture.png)

在 IoT Edge 设备上打开命令提示符，确认从云中部署的模块正在 IoT Edge 设备上运行

    sudo iotedge list

 ![](./images/iotedgedaemon.png) 

在 Azure 的设备详细信息页面上，应当会看到运行时模块（edgeAgent、edgeHub 和 tempSensor 模块）处于“正在运行”状态

 ![](./images/tempSensor.png)

<a name="Step-3-2-DeviceManagement"></a>
## <a name="32-device-management-optional"></a>3.2 设备管理（可选）

**先决条件：** 设备连接。

**说明：** 可以执行由 IoT 中心发出的消息触发的基本设备管理操作（重启和固件更新）的设备。

## <a name="321-firmware-update-using-microsoft-sdk-samples"></a>3.2.1 固件更新（使用 Microsoft SDK 示例）：

指定安装了 firmwareupdate 客户端组件的路径 {{输入路径}}。

若要运行模拟设备应用程序，请打开 shell 或命令提示符窗口，并导航到下载的 Node.js 项目中的 **iot-hub/Tutorials/FirmwareUpdate** 文件夹。 然后运行以下命令：

    npm install
    node SimulatedDevice.js "{your device connection string}"

若要运行后端应用程序，请打开另一个 shell 或命令提示符窗口。 导航到下载的 Node.js 项目中的 **iot-hub/Tutorials/FirmwareUpdate** 文件夹。 然后运行以下命令：

    npm install
    node ServiceClient.js "{your service connection string}"

IoT 设备客户端将得到消息并将状态报告给设备孪生。

 ![](./images/devicetwin.png)

**更新固件**

确认 IoT 中心、设备 ID、方法名称和方法有效负载，如下所示：

-   按下“调用方法”按钮
-   检查返回状态，如下所示：

 ![](./images/firmware.png)


## <a name="322-reboot-using-microsoft-sdk-samples"></a>3.2.2 重启（使用 Microsoft SDK 示例）：

指定安装了组件的路径 {{输入路径}} 

确认 IoT 中心、设备 ID、方法名称，如下所示：

-   按下“调用方法”按钮
-   检查返回状态，如下所示：

 ![](./images/reboot.png)


IoT 设备客户端将得到消息并将状态报告给设备孪生。

 ![](./images/devicetwinmessage.png)
  
## <a name="333-firmware-update-modified-sdk-samplescustom-made-application"></a>3.3.3 固件更新（修改的 SDK 示例/定制的应用程序）：

如果客户端组件是定制的，请通过“设备孪生”添加步骤来执行固件更新。

**注意**：设备必须附带客户端组件 

## <a name="334-reboot-modified-sdk-samplescustom-made-application"></a>3.3.4 重启（修改的 SDK 示例/定制的应用程序）：

如果客户端组件是定制的，请通过“直接方法”添加步骤来执行设备重启。

**注意**：设备必须附带客户端组件 

<a name="NextSteps"></a>
# <a name="step-4-next-steps"></a>步骤 4：后续步骤

与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：故障排除

如需故障排除的帮助，请通过 **<mailto:iotcert@microsoft.com>** 联系工程支持部门。
  
[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md
