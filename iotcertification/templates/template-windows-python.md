---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: python
translationtype: Human Translation
ms.sourcegitcommit: 342b2e268ae6ff4885f2d7b015f1c5dd4c3ae0ad
ms.openlocfilehash: 7d1e20786e56b8376f1078f5c2b7b7ad37790d06
ms.lasthandoff: 01/19/2017

---

<a name="run-a-simple-python-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 python 示例
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：设置开发环境](#Environment)
-   [步骤 4：生成并运行示例](#Build)

# <a name="instructions-for-using-this-template"></a>此模板的用法说明

-   将 {placeholders} 中的文本替换为正确的值。
-   阅读说明后，请删除 {{enclosed}} 行中包含的内容。
-   建议尽可能地使用外部链接。
-   请从最终文档中删除本部分。

<a name="Introduction"></a>
# <a name="introduction"></a>介绍

**关于本文档**

本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。 此过程由多个步骤组成，其中包括：
-   配置 Azure IoT 中心
-   注册 IoT 设备
-   在设备上生成并部署 Azure IoT SDK

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a>步骤 1：先决条件

在开始过程前，应已准备好以下项目：

-   [准备开发环境][setup-devbox-python]
-   [设置 IoT 中心][lnk-setup-iot-hub]
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备
-   {{记下安装、配置和连接设备时需要遵循的说明。 请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

<a name="Load"></a>
## <a name="31-build-sdk-and-sample"></a>3.1 生成 SDK 和示例

-   使用以下命令下载最新的 SDK：

        git clone --recursive https://github.com/Azure/azure-iot-sdks.git

- 确保已安装所需的 Python 版本（2.7.x、3.4.x 或 3.5.x）。 在命令行中运行 python --version 或 python3 --version 可检查版本。 

- 打开 Visual Studio 2015 x86 本机工具命令提示，然后导航到存储库本地副本中的 python/build_all/windows 文件夹。

- 在 python\build_all\windows 目录中运行脚本 build.cmd。

- 这样就会将 **iothub_client.pyd** Python 扩展模块复制到 python/device/samples 文件夹。

- 导航到存储库本地副本中的 python/device/samples 文件夹。

- 在文本编辑器中打开 **iothub_client_sample_amqp.py**、**iothub_client_sample_http.py** 或 **iothub_client_sample_mqtt.py** 文件。

- 在该文件中找到以下代码：

        connectionString = "[device connection string]"

-   将 [device connection string] 替换为设备的连接字符串。 保存更改。

## <a name="32-send-device-events-to-iot-hub"></a>3.2 向 IoT 中心发送设备事件：

-   通过 Visual Studio 2015 x86 本地工具命令提示使用以下命令运行示例应用程序，然后导航到存储库本地副本中的 python/build_all/windows 文件夹：{{***保留根据协议设置的命令并删除剩余内容。***}}

    {{**如果使用 AMQP 协议：**}}

        python iothub_client_sample_amqp.py

    {{**如果使用 HTTPS 协议：**}}

        python iothub_client_sample_http.py

    {{**如果使用 MQTT 协议：**}}

        python iothub_client_sample_mqtt.py

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。

## <a name="33-receive-messages-from-iot-hub"></a>3.3 从 IoT 中心接收消息

-   请参阅[管理 IoT 中心](https://github.com/Azure/azure-iot-sdks/blob/develop/doc/manage_iot_hub.md)，了解如何将云到设备的消息发送到应用程序。

[setup-devbox-python]: <https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/python-devbox-setup.md>
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
