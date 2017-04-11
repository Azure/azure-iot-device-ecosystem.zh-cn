---
platform: 
device: 
language: c
ms.openlocfilehash: 9f6d3ca994ac5f514dbd267450a16d1eb7229071
ms.sourcegitcommit: c6e6e2af724a112c8dc1a00dee046036968ef192
translationtype: HT
---
<a name="run-a-simple-c-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C 示例
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：生成并运行示例](#Build)
-   [提示](#tips)

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

-   [准备开发环境][setup-devbox-linux]
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

-   打开 PuTTY 会话并连接到设备。

-   在开发上的命令行中发出以下命令，安装用于 C 的 Microsoft Azure IoT 设备 SDK 的必备组件包：{{***保留根据 OS 设置的命令并删除剩余内容。***}}

    {{**Debian 或 Ubuntu**}}

        sudo apt-get update

        sudo apt-get install -y curl libcurl4-openssl-dev uuid-dev uuid g++ make cmake git unzip openjdk-7-jre

    {{**Fedora**}}

        sudo dnf check-update -y

        sudo dnf install libcurl-devel openssl-devel libuuid-devel uuid-devel gcc-c++ make cmake git unzip java-1.7.0-openjdk

    {{**其他任何 Linux OS**}}

        Write equivalent commands on the target OS

    {{***如果需要其他任何软件，请在此处指定用于安装这些软件的命令。***}}

-   在开发板上发出以下命令，将用于 C 的 Microsoft Azure IoT 设备 SDK 下载到开发板：

        git clone --recursive https://github.com/Azure/azure-iot-sdks.git

-   使用所选的任何文本编辑器编辑以下文件：{{***根据协议保留文件并删除剩余内容。***}}

    {{**对于 AMQP 协议：**}}

        azure-iot-sdks/c/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp.c

    {{**对于 HTTPS 协议：**}}

        azure-iot-sdks/c/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http.c

-   找到 IoT 连接字符串的以下占位符：

        static const char* connectionString = "[device connection string]";

-   将上述占位符替换为在[步骤 1](#Prerequisites) 中获取的设备连接字符串，然后保存更改。

-   使用以下命令生成 SDK。

        sudo ./azure-iot-sdks/c/build_all/linux/build.sh

## <a name="32-send-device-events-to-iot-hub"></a>3.2 向 IoT 中心发送设备事件：

-   发出以下命令运行示例：{{***保留根据协议设置的命令并删除剩余内容。***}}

    {{**如果使用 AMQP 协议：**}}

        ~/azure-iot-sdks/c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_amqp/iothub_client_sample_amqp

    {{**如果使用 HTTP 协议：**}}

        ~/azure-iot-sdks/c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_http/iothub_client_sample_http

    {{**如果使用 MQTT 协议：**}}

        ~/azure-iot-sdks/c/cmake/iotsdk_linux/iothub_client/samples/iothub_client_sample_mqtt/iothub_client_sample_mqtt

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。

## <a name="33-receive-messages-from-iot-hub"></a>3.3 从 IoT 中心接收消息

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。

<a name="tips"></a>
# <a name="tips"></a>提示

- 如果只想要生成序列化程序示例，请运行以下命令：

  ```
  cd ./c/serializer/build/linux
  make -f makefile.linux all
  ```

[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
