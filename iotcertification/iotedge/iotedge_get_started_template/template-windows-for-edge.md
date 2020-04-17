---
platform:
  enter the OS name running on edge device: 
device:
  enter your device name here: 
language:
  enter the language used to you edge device: 
ms.openlocfilehash: 22db77d2bf8b8194d07257118d3ba47a39768ea0
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "68862369"
---
*强烈建议使此文档保持最新，如果文档包含损坏的 URL 链接、不正确的信息等等，请记住，Microsoft 预留了从 Azure IoT 设备目录中删除设备和文档的权利。*

<a name="run-a-simple-enter-the-language-used-to-you-edge-device-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-edge-device-specify-distribution-or-windows-sku-information-ex-ubuntu-sever-1604-windows-10-iot-core-only-tier-1-os-is-allowed"></a>在运行 {输入 Edge 设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 {输入用于 Edge 设备的语言} 示例。 指定发行版或 Windows SKU 信息。 例如：Ubuntu Sever 16.04、Windows 10 IoT 核心版。 仅允许[第 1 层 OS](https://docs.microsoft.com/en-us/azure/iot-edge/support)。
===
---

# <a name="table-of-contents"></a>目录

-   [简介](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：在设备上对 Azure IoT Edge 进行手动测试](#Manual)
-   [步骤 4：后续步骤](#NextSteps)
-   [步骤 5：故障排除](#Step-5-Troubleshooting)

# <a name="instructions-for-using-this-template"></a>有关使用此模板的说明

-   将 {placeholders} 中的文本替换为正确的值。
-   阅读说明后，请删除 {{enclosed}} 行中包含的内容。
-   建议尽可能地使用外部链接。
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

-   [准备开发环境][setup-devbox-windows]
-   [设置 IoT 中心](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   [注册到 IOT 中心](https://account.windowsazure.com/signup?offer=ms-azr-0044p)
-   [添加 Edge 设备](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart)
-   [添加 Edge 模块](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart#deploy-a-module)
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备

-   {{写下安装、配置和连接设备所要遵照的说明。 请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}

<a name="Manual"></a>
# <a name="step-3-manual-test-for-azure-iot-edge-on-device"></a>步骤 3：在设备上对 Azure IoT Edge 进行手动测试

本部分将引导你在运行 Windows 操作系统的 Edge 设备上执行测试，从而使该设备符合 Azure IoT Edge 认证的要求。

<a name="Step-3-1-IoTEdgeRunTime"></a>
## <a name="31-edge-runtimeenabled-mandatory"></a>3.1：Edge RuntimeEnabled（必需）

**要求详细信息：**

预装以下组件，或者由分销点在设备上为客户安装这些组件：

-   Azure IoT Edge 安全守护程序
-   守护程序配置文件
-   Moby 容器管理系统
-   版本 `hsmlib` 

启用 Edge 运行时： 

在 IoT Edge 设备上打开 Powershell，确认 IoT Edge 服务的状态。

    Get-Service iotedge

检查过去 5 分钟的服务日志。 如果刚完成了 IoT Edge 运行时的安装，则可能会在运行 **Deploy-IoTEdge** 和**Initialize-IoTEdge** 之间看到一系列的错误。 这些错误是预期的错误，因为服务在配置前尝试启动。 

    . {Invoke-WebRequest -useb aka.ms/iotedge-win} | Invoke-Expression; Get-IoTEdgeLog

列出正在运行的模块。 在全新安装之后，应该看到运行的唯一模块是 **edgeAgent**。 [部署 IoT Edge 模块](how-to-deploy-modules-portal.md)后，你将看到其他模块。 

    iotedge list

![](images/edgemodule_status.PNG)

查看从你创建的模块发送到云的消息。

    iotedge logs {module name}

![](images/edgemodule_logs.PNG)

<a name="NextSteps"></a>
# <a name="step-4-next-steps"></a>步骤 4：后续步骤

与我们共享文档后，我们将在接下来的 48 到 72 个工作小时内与你取得联系，以提供后续步骤。

<a name="Step-5-Troubleshooting"></a>
# <a name="step-5-troubleshooting"></a>步骤 5：疑难解答

如需故障排除的帮助，请通过 **<mailto:iotcert@microsoft.com>** 联系工程支持部门。
  
[setup-devbox-windows]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md
