---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: java
translationtype: Human Translation
ms.sourcegitcommit: 342b2e268ae6ff4885f2d7b015f1c5dd4c3ae0ad
ms.openlocfilehash: 25bdbbc752599eb178ff7ba6453737184210ac04
ms.lasthandoff: 01/19/2017

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

-   [准备开发环境][setup-devbox-linux]
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

-   打开 PuTTY 会话并连接到设备。

-   在设备上的命令行中发出以下命令，安装必备组件包。

<a name="Step_3_1_1"/>
### <a name="311--install-java-jdk-and-set-up-environment-variables"></a>3.1.1 安装 Java JDK 并设置环境变量
        
1.  {{保留根据 OS 设置的命令并删除剩余内容。}}
        
    {{**Debian**}}

        sudo apt-get update        
        sudo apt-get install openjdk-8-jdk      
   
    ***注意：****如果 openjdk-8-jdk 包不可用，请使用以下步骤在 sources.list 中添加源，然后再次重新运行上述命令。*
    
    -   编辑 /etc/apt/sources.list
    
    -   添加以下代码行并保存更改。
        
        `deb http://ftp.debian.org/debian testing main`
   
    {{**Ubuntu**}}

        sudo apt-get update        
        sudo apt-get install openjdk-8-jdk 
   
    {{**Fedora**}}
   
        sudo dnf check-update -y
        sudo dnf install java-1.8.0-openjdk-devel
        
    {{**其他任何 Linux OS**}}

        Use equivalent commands on the target OS
       
2.  更新 PATH 环境变量，加入包含 Java 的 bin 文件夹的完整路径。 为确保 Java 路径正确，请运行以下命令：     
       
        which java
        
3.  确保 `which java` 命令显示的目录与 $PATH 变量中显示的某个目录匹配。 可运行以下命令来确认是否存在匹配项：

        echo $PATH

4.  如果 PATH 环境变量中缺少 Java 路径，请运行以下命令设置相同的路径。    

        export PATH=[PathToJava]/bin:$PATH       

    ***注意：****此处的 **[PathToJava]** 是 `which java` 命令的输出。例如，如果 `which java` 输出为 /usr/bin/java，则导出命令为* **export PATH=/usr/bin/java/bin:$PATH**

5.  确保 JAVA_HOME 环境变量包含 JDK 的完整路径。 使用以下命令获取 JDK 路径。

        update-alternatives --config java

6.  记下 JDK 位置。 `update-alternatives` 的输出类似于 **/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java**。 在此情况下，JDK 目录为 **/usr/lib/jvm/java-8-openjdk-amd64/**。

7.  运行以下命令设置 **JAVA_HOME** 环境变量。

        export JAVA_HOME=[PathToJDK]

    ***注意***：*此处的 [PathToJDK] 是 JDK 目录。例如，如果 jdk 目录为 /usr/lib/jvm/java-8-openjdk-amd64/，则导出命令为* **export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/**

<a name="Step_3_1_2"/>
### <a name="312--install-maven-and-set-up-environment-variables"></a>3.1.2 安装 Maven 并设置环境变量

1.  {{保留根据 OS 设置的命令并删除剩余内容。}}

    {{**Debian 或 Ubuntu**}}

        sudo apt-get install maven

    {{**Fedora**}}

        sudo dnf install maven
   
    {{**其他任何 Linux OS**}}

        Use equivalent commands on the target OS

2.  更新 PATH 环境变量，加入包含 Maven 的 bin 文件夹的完整路径。 为确保 Maven 路径正确，请运行以下命令：     
       
        which mvn
         
3.  确保 `which mvn` 命令显示的目录与 $PATH 变量中显示的某个目录匹配。 可运行以下命令来确认是否存在匹配项：
 
        echo $PATH

4.  如果 PATH 环境变量中缺少 Maven 路径，请运行以下命令设置相同的路径。     

        export PATH=[PathToMvn]/bin:$PATH

    ***注意***：*此处的 [PathToMvn] 是 `which mvn` 的输出。例如，如果 `which mvn` 输出为 /usr/bin/mvn，则导出命令为* **export PATH=/usr/bin/mvn/bin:$PATH**
   
5.  可以运行 `mvn --version` 来验证是否已正确设置用于运行 Maven 3 的环境变量。

<a name="Step_3_1_3"/>
### <a name="313--install-git"></a>3.1.3 安装 GIT

1.  {{保留根据 OS 设置的命令并删除剩余内容。}}

    {{**Debian 或 Ubuntu**}}

        sudo apt-get install git

    {{**Fedora**}}

        sudo dnf install git   

    {{**其他任何 Linux OS**}}

        Use equivalent commands on the target OS

<a name="Step_3_1_4"/>
### <a name="314-build-the-azure-iot-device-sdk-for-java"></a>3.1.4 生成适用于 Java 的 Azure IoT 设备 SDK

1.  在 PuTTY 中发出以下命令，将 SDK 下载到开发板：

        git clone https://github.com/Azure/azure-iot-sdks.git

2.  检查 **azure-iot-sdks** 目录中现在是否生成了源代码的副本。

3.  在设备上按顺序运行以下命令，生成 Azure IoT SDK。

        cd azure-iot-sdks/java/device
        mvn install | tee JavaSDK_Build_Logs.txt

4.  上述命令将生成包含所有依赖项的已编译 JAR 文件。 可在以下位置找到此捆绑包：

        azure-iot-sdks/java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"/>
## <a name="32-run-and-validate-the-samples"></a>3.2 运行并验证示例

<a name="Step_3_2_1"/>
### <a name="321-send-device-events-to-iot-hub"></a>3.2.1 向 IoT 中心发送设备事件：

-   导航到包含发送事件示例 JAR 可执行文件的文件夹。

        cd azure-iot-sdks/java/device/samples/send-event/target

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

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。

<a name="Step_3_2_2"/>
### <a name="322-receive-messages-from-iot-hub"></a>3.2.2 从 IoT 中心接收消息

-   导航到包含接收消息示例 JAR 可执行文件的文件夹。

        cd azure-iot-sdks/java/device/samples/handle-messages/target
     
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

-   请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。


[setup-devbox-linux]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/java-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

