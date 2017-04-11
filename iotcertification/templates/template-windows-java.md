---
platform: 
device: 
language: java
ms.openlocfilehash: 33fd4b5464b0822dd577695b5f5c520f35bb8b53
ms.sourcegitcommit: c6e6e2af724a112c8dc1a00dee046036968ef192
translationtype: HT
---
<a name="run-a-simple-java-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a>在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JAVA 示例
===
---

# <a name="table-of-contents"></a>目录

-   [介绍](#Introduction)
-   [步骤 1：先决条件](#Prerequisites)
-   [步骤 2：准备设备](#PrepareDevice)
-   [步骤 3：生成并运行示例](#Build)

# <a name="instructions-for-using-this-template"></a>此模板的用法说明

-   将 {placeholders} 中的文本替换为正确的值。
-   阅读说明后，请删除 {{enclosed}} 行中包含的内容。
-   建议尽可能地使用外部链接。
-   请从最终文档中删除本部分。

<a name="Introduction"/>
# <a name="introduction"></a>介绍

**关于本文档**

本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。 此过程由多个步骤组成，其中包括：
-   配置 Azure IoT 中心
-   注册 IoT 设备
-   在设备上生成并部署 Azure IoT SDK

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a>步骤 1：先决条件

在开始过程前，应已准备好以下项目：

-   [准备开发环境][setup-devbox-windows]
-   [设置 IoT 中心][lnk-setup-iot-hub]
-   [预配设备并获取其凭据][lnk-manage-iot-hub]
-   {在此处输入设备名称} 设备。
-   {{请指定是否需要其他任何软件或硬件。}}

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a>步骤 2：准备设备
-   {{记下安装、配置和连接设备时需要遵循的说明。 请尽量使用指向自己的、包含设备准备步骤的页面的外部链接。}}

<a name="Build"></a>
# <a name="step-3-build-sdk-and-run-the-sample"></a>步骤 3：生成 SDK 并运行示例

<a name="Step_3_1"/>
## <a name="31-install-azure-iot-device-sdk-and-prerequisites-on-device"></a>3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件

-   运行 SDK 需要 Java SE 1.8。

-   在设备上使用命令行安装必备组件包。

<a name="Step_3_1_1"/>
### <a name="311--install-java-jdk-18-and-set-up-environment-variables"></a>3.1.1 安装 Java JDK 1.8 并设置环境变量
        
1.  有关下载和安装说明，请访问：<http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html>
       
2.  请确保 `PATH` 环境变量包含 jdk1.8.x\bin 目录的完整路径。 （示例：c:\Program Files\Java\jdk1.8.0_65）
        
3.  请确保 `JAVA_HOME` 环境变量包含 jdk1.8.x 目录的完整路径。 （示例：JAVA_HOME=c:\Program Files\Java\jdk1.8.0_65）

4.  可以通过重新启动控制台并运行 `java -version`，来测试是否已正确设置 PATH 变量。

<a name="Step_3_1_2"/>
### <a name="312--install-maven-and-set-up-environment-variables"></a>3.1.2 安装 Maven 并设置环境变量
建议使用 Maven 3 安装用于 Java 的 Azure IoT 设备 SDK。

1.  有关 Maven 3 的下载和安装说明，请访问：<https://maven.apache.org/download.cgi>

2.  请确保 PATH 环境变量包含 apache-maven-3.x.x\bin 目录的完整路径。 （示例：F:\Setups\apache-maven-3.3.3\bin）。 Apache maven 3.x.x 目录是 Maven 3 的安装位置。

2.  可以通过重新启动控制台并运行 `mvn --version.`，来验证是否已正确设置用于运行 Maven 3 的环境变量
  
<a name="Step_3_1_3"/>
### <a name="313--install-git"></a>3.1.3 安装 GIT

-   有关下载和安装说明，请访问：<http://git-scm.com/book/en/v2/Getting-Started-Installing-Git>


<a name="Step_3_1_4"/>
### <a name="314-build-the-azure-iot-device-sdk-for-java"></a>3.1.4 生成适用于 Java 的 Azure IoT 设备 SDK

1.  发出以下命令，将 SDK 下载到开发板：

        git clone https://github.com/Azure/azure-iot-sdks.git

2.  检查 **azure-iot-sdks** 目录中现在是否生成了源代码的副本。

3.  在设备上按顺序运行以下命令，生成 Azure IoT SDK。

        cd azure-iot-sdks/java/device
        mvn install

4.  上述命令将生成包含所有依赖项的已编译 JAR 文件。 可在以下位置找到此捆绑包：

        azure-iot-sdks/java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"/>
## <a name="32-run-and-validate-the-samples"></a>3.2 运行并验证示例

<a name="Step_3_2_1"/>
### <a name="321-send-device-events-to-iot-hub"></a>3.2.1 向 IoT 中心发送设备事件：

-   导航到包含发送事件示例 JAR 可执行文件的文件夹。

        cd /azure-iot-sdks/java/device/samples/send-event/target

-   发出以下命令运行该示例。
{{保留根据协议设置的命令并删除剩余内容。}}

    {{**如果使用 AMQPS 协议：**}}

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps"
    
    {{**如果使用 HTTPS 协议：**}}

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "https"

    {{**如果使用 MQTT 协议：**}}

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "mqtt"
        
    替换上述命令中的以下内容：
    
    -   `{version}`：生成的二进制文件的版本
    -   `{connection string}`：设备连接字符串
    -   `{number of requests to send}`：要发送到 IoT 中心的消息数

-   在 Windows 上，请参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“监视设备到云的事件”，确定设备是否正在发送数据。

<a name="Step_3_2_2"/>
### <a name="322-receive-messages-from-iot-hub"></a>3.2.2 从 IoT 中心接收消息

-   导航到包含接收消息示例 JAR 可执行文件的文件夹。

        cd /azure-iot-sdks/java/device/samples/handle-messages/target
     
-   发出以下命令运行该示例。

    {{**如果使用 AMQPS 协议：**}}
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps"
    
    {{**如果使用 HTTPS 协议：**}}
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "https"
        
     {{**如果使用 MQTT 协议：**}}
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "mqtt"

    替换上述命令中的以下内容：
    
    -   `{version}`：生成的二进制文件的版本
    -   `{connection string}`：设备连接字符串
    -   `{number of requests to send}`：要发送到 IoT 中心的消息数

-   在 Windows 上，请参阅 [DeviceExplorer 用法文档](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer/doc/how_to_use_device_explorer.md)中的“发送云到设备的消息”，获取有关向设备发送消息的说明。

[setup-devbox-windows]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/java-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md
