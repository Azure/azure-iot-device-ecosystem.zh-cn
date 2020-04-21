---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: c
ms.openlocfilehash: ca3899acfb442ecf82a50517884a1ccf9d67e481
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62456405"
---
<a name="run-a-simple-c-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 C 示例
===
---

# <a name="table-of-contents"></a>目录

-   [简介](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：生成并运行示例](#Build)
-   [提示](#tips)
-   [后续步骤](#NextSteps)

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
-   在设备上生成和部署 Azure IoT SDK

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
-   {{写下安装、配置和连接设备所要遵照的说明。 请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}

<a name="Build"></a>
# <a name="step-3-build-and-run-the-sample"></a>步骤 3：生成并运行示例

## <a name="31-load-the-azure-iot-bits-and-prerequisites-on-device"></a>3.1：在设备上加载 Azure IoT 代码和必备组件

-   打开 PuTTY 会话并连接到设备。

-   在设备上的命令行中发出以下命令，安装必备组件包。 根据设备上运行的 OS 选择命令。

    **Debian 或 Ubuntu**

        sudo apt-get update

        sudo apt-get install -y curl uuid-dev libcurl4-openssl-dev build-essential cmake git

    **Fedora**

        sudo dnf check-update -y

        sudo dnf install uuid-devel libcurl-devel openssl-devel gcc-c++ make cmake git

    **其他任何 Linux OS**

        Use equivalent commands on the target OS

    ***注意：*** 此安装过程需要 cmake 2.8.12 版或更高版本。  
    
    可使用以下命令来验证环境中当前安装的版本： 

        cmake --version

    *此库还需要 gcc 4.9 或更高版本。* 可使用以下命令来验证环境中当前安装的版本：
    
        gcc --version 

    有关如何升级 Ubuntu 14.04 上的 gcc 版本的信息，请参阅 <http://askubuntu.com/questions/466651/how-do-i-use-the-latest-gcc-4-9-on-ubuntu-14-04>。 
    
-   在 PuTTY 中发出以下命令，将 SDK 下载到开发板：

        git clone --recursive https://github.com/Azure/azure-iot-sdk-c.git

-   验证 ~/azure-iot-sdk-c 目录中现在是否生成了源代码的副本。

<a name="Step-3-2-Build"></a>
## <a name="32-build-the-samples"></a>3.2：生成示例

有两个示例：一个用于向 IoT 中心发送消息，另一个用于从 IoT 中心接收消息。 这两个示例支持不同的协议。 在生成示例之前，可以使用所选的协议对示例示例进行修改。 默认情况下，将会针对 AMQP 协议生成示例。  在生成之前，遵照以下说明编辑示例： 
    
### <a name="321-send-telemetry-to-iot-hub-sample"></a>3.2.1：向 IoT 中心示例发送遥测数据：

1.  在文本编辑器中打开遥测示例文件

        nano azure-iot-sdk-c/iothub_client/samples/iothub_ll_telemetry_sample/iothub_ll_telemetry_sample.c     

2. 找到 IoT 连接字符串的以下占位符：

        static const char* connectionString = "[device connection string]";

3. 将上述占位符替换为设备连接字符串。
    
4. 找到以下占位符以编辑协议：

          // Select the Protocol to use with the connection
        #ifdef USE_AMQP
            //protocol = AMQP_Protocol_over_WebSocketsTls;
            protocol = AMQP_Protocol;
        #endif
        #ifdef USE_MQTT
            //protocol = MQTT_Protocol;
            //protocol = MQTT_WebSocket_Protocol;
        #endif
        #ifdef USE_HTTP
            //protocol = HTTP_Protocol;
        #endif
    
5. 取消注释要测试的协议，并注释其他协议。 若要测试多个协议，请对每个协议重复上述步骤。 

6. 按 Ctrl+O 保存更改，当 nano 提示是否保存为同一文件时，请按 ENTER。

7. 按 Ctrl+X 退出 nano。

### <a name="321-send-message-from-iot-hub-to-device-sample"></a>3.2.1：将消息从 IoT 中心发送到设备示例：

1. 在文本编辑器中打开遥测示例文件

        nano azure-iot-sdk-c/iothub_client/samples/iothub_ll_c2d_sample/iothub_ll_c2d_sample.c

2. 遵循上述步骤 1-7 编辑此示例。

### <a name="321-build-the-samples"></a>3.2.1：生成示例：

-   使用以下命令生成 SDK。 如果生成期间遇到任何问题。

        sudo ./azure-iot-sdk-c/build_all/linux/build.sh | tee LogFile.txt
    
    ***注意：*** 应将上述命令中的 LogFile.txt 替换为要将生成输出写入到的文件名。 
    
    build.sh 在“~/azure-iot-sdk-c/”下创建名为“cmake”的文件夹。 *“cmake”中保存了整个软件的所有编译结果。*


<a name="Step-3-3-Run"></a>
## <a name="33-run-and-validate-the-samples"></a>3.3 运行并验证示例

在本部分，我们将运行 Azure IoT 客户端 SDK 示例来验证设备与 Azure IoT 中心之间的通信。 我们要向 Azure IoT 中心服务发送消息，然后验证 IoT 中心是否成功接收数据。 此外，我们还会监视从 Azure IoT 中心发送到客户端的任何消息。

### <a name="331-send-device-events-to-iot-hub"></a>3.3.1：向 IOT 中心发送设备事件：

-   发出以下命令运行示例。    

        azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_ll_telemetry_sample/iothub_ll_telemetry_sample


### <a name="332-receive-messages-from-iot-hub"></a>3.3.2：从 IoT 中心接收消息

-   发出以下命令运行示例。

        azure-iot-sdk-c/cmake/iotsdk_linux/iothub_client/samples/iothub_ll_c2d_sample/iothub_ll_c2d_sample
        

<a name="NextSteps"></a>
# <a name="next-steps"></a>后续步骤

现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。 若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：

-   [使用 iothub-explorer 管理云设备消息传送]
-   [将 IoT 中心消息保存到 Azure 数据存储]
-   [使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]
-   [使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]
-   [在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]
-   [使用逻辑应用执行远程监视和发送通知]   

[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[setup-devbox-linux]: https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
