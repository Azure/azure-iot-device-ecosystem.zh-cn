---
platform:
  enter the OS name running on device: 
device:
  enter your device name here: 
language: java
ms.openlocfilehash: 86978cd10db22b4a576cfcea7f91392f211d0c86
ms.sourcegitcommit: 46cea633cf6b8105790bb3c1d5b1a81c44035391
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "62453320"
---
<a name="run-a-simple-java-sample-on-enter-your-device-name-here-device-running-enter-the-os-name-running-on-device"></a><span data-ttu-id="b1b54-101">在运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备上运行简单的 JAVA 示例</span><span class="sxs-lookup"><span data-stu-id="b1b54-101">Run a simple JAVA sample on {enter your device name here} device running {enter the OS name running on device}</span></span>
===
---

# <a name="table-of-contents"></a><span data-ttu-id="b1b54-102">目录</span><span class="sxs-lookup"><span data-stu-id="b1b54-102">Table of Contents</span></span>

-   [<span data-ttu-id="b1b54-103">简介</span><span class="sxs-lookup"><span data-stu-id="b1b54-103">Introduction</span></span>](#Introduction)
-   [<span data-ttu-id="b1b54-104">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="b1b54-104">Step 1: Prerequisites</span></span>](#Prerequisites)
-   [<span data-ttu-id="b1b54-105">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="b1b54-105">Step 2: Prepare your Device</span></span>](#PrepareDevice)
-   [<span data-ttu-id="b1b54-106">步骤 3：生成并运行示例</span><span class="sxs-lookup"><span data-stu-id="b1b54-106">Step 3: Build and Run the Sample</span></span>](#Build)
-   [<span data-ttu-id="b1b54-107">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b1b54-107">Next Steps</span></span>](#NextSteps)

# <a name="instructions-for-using-this-template"></a><span data-ttu-id="b1b54-108">此模板的用法说明</span><span class="sxs-lookup"><span data-stu-id="b1b54-108">Instructions for using this template</span></span>

-   <span data-ttu-id="b1b54-109">将 {placeholders} 中的文本替换为正确的值。</span><span class="sxs-lookup"><span data-stu-id="b1b54-109">Replace the text in {placeholders} with correct values.</span></span>
-   <span data-ttu-id="b1b54-110">阅读说明后，请删除 {{enclosed}} 行中包含的内容。</span><span class="sxs-lookup"><span data-stu-id="b1b54-110">Delete the lines {{enclosed}} after following the instructions enclosed between them.</span></span>
-   <span data-ttu-id="b1b54-111">建议尽可能地使用外部链接。</span><span class="sxs-lookup"><span data-stu-id="b1b54-111">It is advisable to use external links, wherever possible.</span></span>
-   <span data-ttu-id="b1b54-112">请从最终文档中删除本部分。</span><span class="sxs-lookup"><span data-stu-id="b1b54-112">Remove this section from final document.</span></span>

<a name="Introduction"/>
# <a name="introduction"></a><span data-ttu-id="b1b54-113">介绍</span><span class="sxs-lookup"><span data-stu-id="b1b54-113">Introduction</span></span>

<span data-ttu-id="b1b54-114">**关于本文档**</span><span class="sxs-lookup"><span data-stu-id="b1b54-114">**About this document**</span></span>

<span data-ttu-id="b1b54-115">本文档介绍如何将运行 {输入设备上运行的 OS 名称} 的 {在此处输入设备名称} 设备连接到 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="b1b54-115">This document describes how to connect {enter your device name here} device running {enter the OS name running on device} with Azure IoT SDK.</span></span> <span data-ttu-id="b1b54-116">此过程由多个步骤组成，其中包括：</span><span class="sxs-lookup"><span data-stu-id="b1b54-116">This multi-step process includes:</span></span>
-   <span data-ttu-id="b1b54-117">配置 Azure IoT 中心</span><span class="sxs-lookup"><span data-stu-id="b1b54-117">Configuring Azure IoT Hub</span></span>
-   <span data-ttu-id="b1b54-118">注册 IoT 设备</span><span class="sxs-lookup"><span data-stu-id="b1b54-118">Registering your IoT device</span></span>
-   <span data-ttu-id="b1b54-119">在设备上生成和部署 Azure IoT SDK</span><span class="sxs-lookup"><span data-stu-id="b1b54-119">Build and deploy Azure IoT SDK on device</span></span>

<a name="Prerequisites"></a>
# <a name="step-1-prerequisites"></a><span data-ttu-id="b1b54-120">步骤 1：先决条件</span><span class="sxs-lookup"><span data-stu-id="b1b54-120">Step 1: Prerequisites</span></span>

<span data-ttu-id="b1b54-121">在开始过程前，应已准备好以下项目：</span><span class="sxs-lookup"><span data-stu-id="b1b54-121">You should have the following items ready before beginning the process:</span></span>

-   <span data-ttu-id="b1b54-122">[准备开发环境][setup-devbox-linux]</span><span class="sxs-lookup"><span data-stu-id="b1b54-122">[Prepare your development environment][setup-devbox-linux]</span></span>
-   <span data-ttu-id="b1b54-123">[设置 IoT 中心][lnk-setup-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="b1b54-123">[Setup your IoT hub][lnk-setup-iot-hub]</span></span>
-   <span data-ttu-id="b1b54-124">[预配设备并获取其凭据][lnk-manage-iot-hub]</span><span class="sxs-lookup"><span data-stu-id="b1b54-124">[Provision your device and get its credentials][lnk-manage-iot-hub]</span></span>
-   <span data-ttu-id="b1b54-125">{在此处输入设备名称} 设备。</span><span class="sxs-lookup"><span data-stu-id="b1b54-125">{enter your device name here} device.</span></span>
-   <span data-ttu-id="b1b54-126">{{请指定是否需要其他任何软件或硬件。}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-126">{{Please specify if any other software(s) or hardware(s) are required.}}</span></span>

<a name="PrepareDevice"></a>
# <a name="step-2-prepare-your-device"></a><span data-ttu-id="b1b54-127">步骤 2：准备设备</span><span class="sxs-lookup"><span data-stu-id="b1b54-127">Step 2: Prepare your Device</span></span>
-   <span data-ttu-id="b1b54-128">{{写下安装、配置和连接设备所要遵照的说明。</span><span class="sxs-lookup"><span data-stu-id="b1b54-128">{{Write down the instructions required to setup, configure and connect your device.</span></span> <span data-ttu-id="b1b54-129">请尽量使用指向自己页面的外部链接，该页面提供了设备准备步骤。}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-129">Please use external links when possible pointing to your own page with device preparation steps.}}</span></span>

<a name="Build"></a>
# <a name="step-3-build-sdk-and-run-the-sample"></a><span data-ttu-id="b1b54-130">步骤 3：生成 SDK 并运行示例</span><span class="sxs-lookup"><span data-stu-id="b1b54-130">Step 3: Build SDK and Run the sample</span></span>

<a name="Step_3_1"/>
## <a name="31-install-azure-iot-device-sdk-and-prerequisites-on-device"></a><span data-ttu-id="b1b54-131">3.1 在设备上安装 Azure IoT 设备 SDK 和必备组件</span><span class="sxs-lookup"><span data-stu-id="b1b54-131">3.1 Install Azure IoT Device SDK and prerequisites on device</span></span>

-   <span data-ttu-id="b1b54-132">打开 PuTTY 会话并连接到设备。</span><span class="sxs-lookup"><span data-stu-id="b1b54-132">Open a PuTTY session and connect to the device.</span></span>

-   <span data-ttu-id="b1b54-133">在设备上的命令行中发出以下命令，安装必备组件包。</span><span class="sxs-lookup"><span data-stu-id="b1b54-133">Install the prerequisite packages by issuing the following commands from the command line on the device.</span></span>

<a name="Step_3_1_1"/>
### <a name="311--install-java-jdk-and-set-up-environment-variables"></a><span data-ttu-id="b1b54-134">3.1.1 安装 Java JDK 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="b1b54-134">3.1.1  Install Java JDK and set up environment variables</span></span>
        
1.  <span data-ttu-id="b1b54-135">{{保留根据 OS 设置的命令并删除剩余内容。}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-135">{{Keep the command set based on your OS and remove the rest.}}</span></span>
        
    <span data-ttu-id="b1b54-136">{{**Debian**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-136">{{**Debian**}}</span></span>

        sudo apt-get update        
        sudo apt-get install openjdk-8-jdk      
   
    <span data-ttu-id="b1b54-137">***注意：*** 如果 openjdk-8-jdk 包不可用，请使用以下步骤在 sources.list 中添加源，然后再次重新运行上述命令。 </span><span class="sxs-lookup"><span data-stu-id="b1b54-137">***Note:*** *If openjdk-8-jdk package is not available, use following steps to add source in sources.list and rerun above commands again.*</span></span>
    
    -   <span data-ttu-id="b1b54-138">编辑 /etc/apt/sources.list</span><span class="sxs-lookup"><span data-stu-id="b1b54-138">Edit /etc/apt/sources.list</span></span>
    
    -   <span data-ttu-id="b1b54-139">添加以下代码行并保存更改。</span><span class="sxs-lookup"><span data-stu-id="b1b54-139">Add below line and save the changes.</span></span>
        
        `deb http://ftp.debian.org/debian testing main`
   
    <span data-ttu-id="b1b54-140">{{**Ubuntu**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-140">{{**Ubuntu**}}</span></span>

        sudo apt-get update        
        sudo apt-get install openjdk-8-jdk 
   
    <span data-ttu-id="b1b54-141">{{**Fedora**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-141">{{**Fedora**}}</span></span>
   
        sudo dnf check-update -y
        sudo dnf install java-1.8.0-openjdk-devel
        
    <span data-ttu-id="b1b54-142">{{**其他任何 Linux OS**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-142">{{**Any Other Linux OS**}}</span></span>

        Use equivalent commands on the target OS
       
2.  <span data-ttu-id="b1b54-143">更新 PATH 环境变量，加入包含 Java 的 bin 文件夹的完整路径。</span><span class="sxs-lookup"><span data-stu-id="b1b54-143">Update the PATH environment variable to include the full path to the bin folder containing Java.</span></span> <span data-ttu-id="b1b54-144">为确保 Java 路径正确，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b1b54-144">To ensure the correct path of Java run below command:</span></span>     
       
        which java
        
3.  <span data-ttu-id="b1b54-145">确保 `which java` 命令显示的目录与 $PATH 变量中显示的某个目录匹配。</span><span class="sxs-lookup"><span data-stu-id="b1b54-145">Ensure that the directory shown by the `which java` command matches one of the directories shown in your $PATH variable.</span></span> <span data-ttu-id="b1b54-146">可运行以下命令来确认是否存在匹配项：</span><span class="sxs-lookup"><span data-stu-id="b1b54-146">You can confirm this by running following command.</span></span>

        echo $PATH

4.  <span data-ttu-id="b1b54-147">如果 PATH 环境变量中缺少 Java 路径，请运行以下命令设置相同的路径。</span><span class="sxs-lookup"><span data-stu-id="b1b54-147">If Java path is missing in PATH environment variable, run following command to set the same.</span></span>    

        export PATH=[PathToJava]/bin:$PATH       

    <span data-ttu-id="b1b54-148">\*\**注意：\*\*\*\*此处的 [PathToJava]  是 `which java` 命令的输出。例如，如果 `which java` 输出为 /usr/bin/java，则导出命令为* **export PATH=/usr/bin/java/bin:$PATH**</span><span class="sxs-lookup"><span data-stu-id="b1b54-148">***NOTE:*** *Here **[PathToJava]** is output of `which java` command. For example, if `which java` output is /usr/bin/java, then export command will be* **export PATH=/usr/bin/java/bin:$PATH**</span></span>

5.  <span data-ttu-id="b1b54-149">确保 JAVA_HOME 环境变量包含 JDK 的完整路径。</span><span class="sxs-lookup"><span data-stu-id="b1b54-149">Make sure that the JAVA_HOME environment variable includes the full path to the JDK.</span></span> <span data-ttu-id="b1b54-150">使用以下命令获取 JDK 路径。</span><span class="sxs-lookup"><span data-stu-id="b1b54-150">Use below command to get the JDK path.</span></span>

        update-alternatives --config java

6.  <span data-ttu-id="b1b54-151">记下 JDK 位置。</span><span class="sxs-lookup"><span data-stu-id="b1b54-151">Take note of the JDK location.</span></span> <span data-ttu-id="b1b54-152">`update-alternatives` 的输出类似于 **/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java**。</span><span class="sxs-lookup"><span data-stu-id="b1b54-152">`update-alternatives` output will show something similar to **/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java**.</span></span> <span data-ttu-id="b1b54-153">在此情况下，JDK 目录为 **/usr/lib/jvm/java-8-openjdk-amd64/** 。</span><span class="sxs-lookup"><span data-stu-id="b1b54-153">The JDK directory would then be **/usr/lib/jvm/java-8-openjdk-amd64/**.</span></span>

7.  <span data-ttu-id="b1b54-154">运行以下命令设置 **JAVA_HOME** 环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1b54-154">Run the following command to set **JAVA_HOME** environment variable.</span></span>

        export JAVA_HOME=[PathToJDK]

    <span data-ttu-id="b1b54-155">***注意***：此处的 [PathToJDK] 是 JDK 目录。*例如，如果 jdk 目录为 /usr/lib/jvm/java-8-openjdk-amd64/，则导出命令为* **export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/**</span><span class="sxs-lookup"><span data-stu-id="b1b54-155">***Note***: *Here [PathToJDK] is JDK directory. For example if jdk directory is /usr/lib/jvm/java-8-openjdk-amd64/, export command will be* **export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/**</span></span>

<a name="Step_3_1_2"/>
### <a name="312--install-maven-and-set-up-environment-variables"></a><span data-ttu-id="b1b54-156">3.1.2 安装 Maven 并设置环境变量</span><span class="sxs-lookup"><span data-stu-id="b1b54-156">3.1.2  Install Maven and set up environment variables</span></span>

1.  <span data-ttu-id="b1b54-157">{{保留根据 OS 设置的命令并删除剩余内容。}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-157">{{Keep the command set based on your OS and remove the rest.}}</span></span>

    <span data-ttu-id="b1b54-158">{{**Debian 或 Ubuntu**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-158">{{**Debian or Ubuntu**}}</span></span>

        sudo apt-get install maven

    <span data-ttu-id="b1b54-159">{{**Fedora**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-159">{{**Fedora**}}</span></span>

        sudo dnf install maven
   
    <span data-ttu-id="b1b54-160">{{**其他任何 Linux OS**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-160">{{**Any Other Linux OS**}}</span></span>

        Use equivalent commands on the target OS

2.  <span data-ttu-id="b1b54-161">更新 PATH 环境变量，加入包含 Maven 的 bin 文件夹的完整路径。</span><span class="sxs-lookup"><span data-stu-id="b1b54-161">Update the PATH environment variable to include the full path to the bin folder containing maven.</span></span> <span data-ttu-id="b1b54-162">为确保 Maven 路径正确，请运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="b1b54-162">To ensure the correct path of maven, run below command:</span></span>     
       
        which mvn
         
3.  <span data-ttu-id="b1b54-163">确保 `which mvn` 命令显示的目录与 $PATH 变量中显示的某个目录匹配。</span><span class="sxs-lookup"><span data-stu-id="b1b54-163">Ensure that the directory shown by the `which mvn` command matches one of the directories shown in your $PATH variable.</span></span> <span data-ttu-id="b1b54-164">可运行以下命令来确认是否存在匹配项：</span><span class="sxs-lookup"><span data-stu-id="b1b54-164">You can confirm this by running following command.</span></span>
 
        echo $PATH

4.  <span data-ttu-id="b1b54-165">如果 PATH 环境变量中缺少 Maven 路径，请运行以下命令设置相同的路径。</span><span class="sxs-lookup"><span data-stu-id="b1b54-165">If maven path is missing in PATH environment variable, run following command to set the same.</span></span>     

        export PATH=[PathToMvn]/bin:$PATH

    <span data-ttu-id="b1b54-166">***注意***：此处的 [PathToMvn] 是 `which mvn` 的输出。*例如，如果 `which mvn` 输出为 /usr/bin/mvn，则导出命令为* **export PATH=/usr/bin/mvn/bin:$PATH**</span><span class="sxs-lookup"><span data-stu-id="b1b54-166">***Note***: *Here [PathToMvn] is output of `which mvn`. For example if `which mvn` output is /usr/bin/mvn, export command will be* **export PATH=/usr/bin/mvn/bin:$PATH**</span></span>
   
5.  <span data-ttu-id="b1b54-167">可以运行 `mvn --version` 来验证是否已正确设置用于运行 Maven 3 的环境变量。</span><span class="sxs-lookup"><span data-stu-id="b1b54-167">You can verify that the environment variables necessary to run Maven 3 have been set correctly by running `mvn --version`.</span></span>

<a name="Step_3_1_3"/>
### <a name="313--install-git"></a><span data-ttu-id="b1b54-168">3.1.3 安装 GIT</span><span class="sxs-lookup"><span data-stu-id="b1b54-168">3.1.3  Install GIT</span></span>

1.  <span data-ttu-id="b1b54-169">{{保留根据 OS 设置的命令并删除剩余内容。}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-169">{{Keep the command set based on your OS and remove the rest.}}</span></span>

    <span data-ttu-id="b1b54-170">{{**Debian 或 Ubuntu**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-170">{{**Debian or Ubuntu**}}</span></span>

        sudo apt-get install git

    <span data-ttu-id="b1b54-171">{{**Fedora**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-171">{{**Fedora**}}</span></span>

        sudo dnf install git   

    <span data-ttu-id="b1b54-172">{{**其他任何 Linux OS**}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-172">{{**Any Other Linux OS**}}</span></span>

        Use equivalent commands on the target OS

<a name="Step_3_1_4"/>
### <a name="314-build-the-azure-iot-device-sdk-for-java"></a><span data-ttu-id="b1b54-173">3.1.4 生成适用于 Java 的 Azure IoT 设备 SDK</span><span class="sxs-lookup"><span data-stu-id="b1b54-173">3.1.4 Build the Azure IoT Device SDK for Java</span></span>

1.  <span data-ttu-id="b1b54-174">在 PuTTY 中发出以下命令，将 SDK 下载到开发板：</span><span class="sxs-lookup"><span data-stu-id="b1b54-174">Download the SDK to the board by issuing the following command in PuTTY:</span></span>

        git clone https://github.com/Azure/azure-iot-sdk-java.git

2.  <span data-ttu-id="b1b54-175">验证 **azure-iot-sdk-java** 目录中现在是否有源代码的副本。</span><span class="sxs-lookup"><span data-stu-id="b1b54-175">Verify that you now have a copy of the source code under the directory **azure-iot-sdk-java**.</span></span>

3.  <span data-ttu-id="b1b54-176">在设备上按顺序运行以下命令，生成 Azure IoT SDK。</span><span class="sxs-lookup"><span data-stu-id="b1b54-176">Run the following commands on device in sequence to build Azure IoT SDK.</span></span>

        cd azure-iot-sdk-java/device
        mvn install | tee JavaSDK_Build_Logs.txt

4.  <span data-ttu-id="b1b54-177">上述命令将生成包含所有依赖项的已编译 JAR 文件。</span><span class="sxs-lookup"><span data-stu-id="b1b54-177">Above command will generate the compiled JAR files with all dependencies.</span></span> <span data-ttu-id="b1b54-178">可在以下位置找到此捆绑包：</span><span class="sxs-lookup"><span data-stu-id="b1b54-178">This bundle can be found at:</span></span>

        azure-iot-sdk-java/device/iothub-java-client/target/iothub-java-client-{version}-with-deps.jar

<a name="Step_3_2"/>
## <a name="32-run-and-validate-the-samples"></a><span data-ttu-id="b1b54-179">3.2 运行并验证示例</span><span class="sxs-lookup"><span data-stu-id="b1b54-179">3.2 Run and Validate the Samples</span></span>

<a name="Step_3_2_1"/>
### <a name="321-send-device-events-to-iot-hub"></a><span data-ttu-id="b1b54-180">3.2.1 向 IoT 中心发送设备事件：</span><span class="sxs-lookup"><span data-stu-id="b1b54-180">3.2.1 Send Device Events to IoT Hub:</span></span>

-   <span data-ttu-id="b1b54-181">导航到包含发送事件示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b1b54-181">Navigate to the folder containing the executable JAR file for send event sample.</span></span>

        cd azure-iot-sdk-java/device/samples/send-event/target

-   <span data-ttu-id="b1b54-182">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="b1b54-182">Run the sample by issuing following command.</span></span>
<span data-ttu-id="b1b54-183">{{保留根据协议设置的命令并删除剩余内容。}}</span><span class="sxs-lookup"><span data-stu-id="b1b54-183">{{Keep the command set based on your protocol(s) and remove the rest.}}</span></span>

    <span data-ttu-id="b1b54-184">{{**如果使用 AMQPS 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="b1b54-184">{{**If using AMQPS protocol:**}}</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "amqps"
    
    <span data-ttu-id="b1b54-185">{{**如果使用 HTTPS 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="b1b54-185">{{**If using HTTPS protocol:**}}</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "https"

    <span data-ttu-id="b1b54-186">{{**如果使用 MQTT 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="b1b54-186">{{**If using MQTT protocol:**}}</span></span>

        java -jar ./send-event-{version}-with-deps.jar "{connection string}" "{number of requests to send}" "mqtt"
          
    <span data-ttu-id="b1b54-187">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="b1b54-187">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="b1b54-188">`{version}`设置用户帐户 ：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="b1b54-188">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="b1b54-189">`{connection string}`设置用户帐户 ：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="b1b54-189">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="b1b54-190">`{number of requests to send}`设置用户帐户 ：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="b1b54-190">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

-   <span data-ttu-id="b1b54-191">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何监视 IoT 中心从应用程序接收的消息。</span><span class="sxs-lookup"><span data-stu-id="b1b54-191">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.</span></span>

<a name="Step_3_2_2"/>
### <a name="322-receive-messages-from-iot-hub"></a><span data-ttu-id="b1b54-192">3.2.2 从 IoT 中心接收消息</span><span class="sxs-lookup"><span data-stu-id="b1b54-192">3.2.2 Receive messages from IoT Hub</span></span>

-   <span data-ttu-id="b1b54-193">导航到包含接收消息示例 JAR 可执行文件的文件夹。</span><span class="sxs-lookup"><span data-stu-id="b1b54-193">Navigate to the folder containing the executable JAR file for the receive message sample.</span></span>

        cd azure-iot-sdk-java/device/samples/handle-messages/target
     
-   <span data-ttu-id="b1b54-194">发出以下命令运行该示例。</span><span class="sxs-lookup"><span data-stu-id="b1b54-194">Run the sample by issuing following command.</span></span>

    <span data-ttu-id="b1b54-195">{{**如果使用 AMQPS 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="b1b54-195">{{**If using AMQPS protocol:**}}</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "amqps"
    
    <span data-ttu-id="b1b54-196">{{**如果使用 HTTPS 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="b1b54-196">{{**If using HTTPS protocol:**}}</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "https"

    <span data-ttu-id="b1b54-197">{{**如果使用 MQTT 协议：** }}</span><span class="sxs-lookup"><span data-stu-id="b1b54-197">{{**If using MQTT protocol:**}}</span></span>
   
        java -jar ./handle-messages-{version}-with-deps.jar "{connection string}" "mqtt"
        
    <span data-ttu-id="b1b54-198">替换上述命令中的以下内容：</span><span class="sxs-lookup"><span data-stu-id="b1b54-198">Replace the following in above command:</span></span>
    
    -   <span data-ttu-id="b1b54-199">`{version}`设置用户帐户 ：生成的二进制文件的版本</span><span class="sxs-lookup"><span data-stu-id="b1b54-199">`{version}`: Version of binaries you have build</span></span>
    -   <span data-ttu-id="b1b54-200">`{connection string}`设置用户帐户 ：设备连接字符串</span><span class="sxs-lookup"><span data-stu-id="b1b54-200">`{connection string}`: Your device connection string</span></span>
    -   <span data-ttu-id="b1b54-201">`{number of requests to send}`设置用户帐户 ：要发送到 IoT 中心的消息数</span><span class="sxs-lookup"><span data-stu-id="b1b54-201">`{number of requests to send}`: Number of messages you want to send to IoT Hub</span></span>

-   <span data-ttu-id="b1b54-202">请参阅[管理 IoT 中心][lnk-manage-iot-hub]，了解如何将云到设备的消息发送到应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1b54-202">See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.</span></span>


<a name="NextSteps"></a>
# <a name="next-steps"></a><span data-ttu-id="b1b54-203">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b1b54-203">Next Steps</span></span>

<span data-ttu-id="b1b54-204">现在，你已了解如何运行用于收集传感器数据并将其发送到 IoT 中心的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1b54-204">You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub.</span></span> <span data-ttu-id="b1b54-205">若要探究如何使用各种不同的服务在 Azure 中存储、分析以及可视化来自此应用程序的数据，请单击以下课程：</span><span class="sxs-lookup"><span data-stu-id="b1b54-205">To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:</span></span>

-   <span data-ttu-id="b1b54-206">[使用 iothub-explorer 管理云设备消息传送]</span><span class="sxs-lookup"><span data-stu-id="b1b54-206">[Manage cloud device messaging with iothub-explorer]</span></span>
-   <span data-ttu-id="b1b54-207">[将 IoT 中心消息保存到 Azure 数据存储]</span><span class="sxs-lookup"><span data-stu-id="b1b54-207">[Save IoT Hub messages to Azure data storage]</span></span>
-   <span data-ttu-id="b1b54-208">[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="b1b54-208">[Use Power BI to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="b1b54-209">[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]</span><span class="sxs-lookup"><span data-stu-id="b1b54-209">[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]</span></span>
-   <span data-ttu-id="b1b54-210">[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]</span><span class="sxs-lookup"><span data-stu-id="b1b54-210">[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]</span></span>
-   <span data-ttu-id="b1b54-211">[使用逻辑应用执行远程监视和发送通知]</span><span class="sxs-lookup"><span data-stu-id="b1b54-211">[Remote monitoring and notifications with Logic Apps]</span></span>   

[使用 iothub-explorer 管理云设备消息传送]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[将 IoT 中心消息保存到 Azure 数据存储]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[使用 Power BI 可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[使用 Azure Web 应用可视化来自 Azure IoT 中心的实时传感器数据]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[在 Azure 机器学习中使用 IoT 中心的传感器数据进行天气预报]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[使用逻辑应用执行远程监视和发送通知]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[setup-devbox-linux]: https://github.com/Azure/azure-iot-device-ecosystem/blob/master/get_started/java-devbox-setup.md
[lnk-setup-iot-hub]: ../../setup_iothub.md
[lnk-manage-iot-hub]: ../../manage_iot_hub.md

