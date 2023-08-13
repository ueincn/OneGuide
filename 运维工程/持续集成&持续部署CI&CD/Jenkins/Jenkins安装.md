- [下载中心](#下载中心)
- [安装方式](#安装方式)
  - [Generic Java package (.war)](#generic-java-package-war)
  - [Debian/Ubuntu](#debianubuntu)
  - [CentOS/Fedora/Red Hat](#centosfedorared-hat)
#### 准备工作
第一次使用 Jenkins，您需要：
- 机器要求（最低推荐配置）：
  - 256 MB 内存，建议大于 512 MB
  - 1 GB 的硬盘空间
    - 作为一个Docker容器运行jenkins的话推荐10GB
- 需要安装以下软件：
  - Java 8 ( JRE 或者 JDK 都可以)
    - 如果将Jenkins作为Docker 容器运行，这不是必需的。
---
# 下载中心
- 最新War包
  - [http://mirrors.jenkins.io/war-stable/latest/jenkins.war](http://mirrors.jenkins.io/war-stable/latest/jenkins.war)
- 官网下载中心
  - [https://www.jenkins.io/zh/download/](https://www.jenkins.io/zh/download/)
- 开源软件镜像站（国内）
  - 清华大学：[https://mirrors.tuna.tsinghua.edu.cn/jenkins/](https://mirrors.tuna.tsinghua.edu.cn/jenkins/)
---
# 安装方式
## Generic Java package (.war)
#### 下载并运行 Jenkins
- 下载 [Jenkins](http://mirrors.jenkins.io/war-stable/latest/jenkins.war).
- 打开终端进入到下载目录.
- 运行命令 `java -jar jenkins.war --httpPort=8080`.
- 打开浏览器进入链接 http://localhost:8080.
- 按照说明完成安装.

安装完成后，您可以开始使用 Jenkins！
#### Shell安装Jenkins war包脚本
```bash
#!/bin/bash

#Program
#   Jenkins Install Scripts
#History
#2023   Ueincn  Release

function JenkinsIntsll(){
    wget -c --no-check-certificate https://mirrors.tuna.tsinghua.edu.cn/jenkins/war-stable/latest/jenkins.war
    if [ ! -d /opt/jenkins ]; then
        mkdir -p /opt/jenkins
    fi
    mv jenkins.war /opt/jenkins
    chmod -R +x /opt/jenkins
    echo "Jenkins installation complete."
    echo ""
    echo "Jenkins is starting ... "
    java -jar /opt/jenkins/jenkins.war --httpPort=6600
}

function JavaInstall(){
    if command -v java >/dev/null 2>&1; then
        echo "Java is installed ... "
        JenkinsIntsll
    else
        wget -c --no-check-certificate https://mirrors.tuna.tsinghua.edu.cn/Adoptium/17/jre/x64/linux/OpenJDK17U-jre_x64_linux_hotspot_17.0.8_7.tar.gz
        if [ ! -d /opt/java ]; then
            mkdir -p /opt/java
        fi
        tar -zxvf OpenJDK17U-jre_x64_linux_hotspot_17.0.8_7.tar.gz --strip-components 1 -C /opt/java
        cd ../ && rm -rf OpenJDK17U-jre_x64_linux_hotspot_17.0.8_7.tar.gz
        cp /etc/profile /etc/profile.bak
        JavaEnv
        source /etc/profile
        echo ""
        echo "Java installation complete."
        echo "Print the Java version ... "
        echo ""
        java --version
    fi
}

function JavaEnv(){
        cat >/etc/profile <<EOF 
export JAVA_HOME=/opt/java
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
EOF
}

function Main(){
    if command -v wget >/dev/null 2>&1; then
        JavaInstall
    else
        echo "Please try again after installing Wget ! "
    fi
}

if [ $UID -eq 0 ]; then
    Main
else
    echo "[ !! Please use sudo permissions or switch root to run the script !! ]"
fi
```
## Debian/Ubuntu
在基于Debian的发行版（如Ubuntu）上，您可通过`apt`安装Jenkins
在[an apt repository](https://pkg.jenkins.io/debian/)可获得最新版本，较老但稳定的LTS版本在[this apt repository](https://pkg.jenkins.io/debian-stable/)这里可获得
```bash
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install fontconfig openjdk-11-jre #如失败可自行安装jdk或jre
sudo apt-get install jenkins
```
安装这个软件包将会：
- 将Jenkins设置为启动时启动的守护进程。查看`/etc/init.d/jenkins`获取更多细节
- 创建一个'jenkins'用户来运行此服务
- 直接将控制台日志输出到文件`/var/log/jenkins/jenkins.log`。如果您正在解决Jenkins问题，请检查此文件
- /etc/default/jenkins`为启动填充配置参数，例如JENKINS_HOME
- 将Jenkins设置为在端口8080上进行监听。使用浏览器访问此端口以开始配置
> PS:
> 
> 如果你的`/etc/init.d/jenkins`文件无法启动Jenkins，编辑`/etc/default/jenkins`， 修改 ----HTTP_PORT=8080----`为----HTTP_PORT=8081----` 在这里，“8081”也可被换为其他可用端口。

## CentOS/Fedora/Red Hat
```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key

sudo yum install fontconfig java-11-openjdk #如失败可自行安装jdk或jre
sudo yum install jenkins
```