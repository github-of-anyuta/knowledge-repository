
OpenJDK 安装与配置
=================

## 安装前准备工作

### 卸载之前已安装的 Java 环境(建议也同样检查非 Java 环境，卸载干净)

#### CentOS

	$ sudo yum remove *jdk*
	$ sudo yum remove *jre*
	$ sudo yum remove *java*
	rpm -qa | grep jdk && rpm -e ...
	rpm -qa | grep jre && rpm -e ...
	rpm -qa | grep java && rpm -e ...

#### Debian & Ubuntu

##### 从候选项列表移除要卸载的java路径

	$ update-alternatives --list java

	$ sudo update-alternatives --remove java [路径]

##### 查找到需要卸载的java包，并执行卸载

	$ dpkg --list | grep java

	$ sudo apt-get purge [包名]

## 安装软件

### 安装开发环境（JDK 包含 JRE，无需再单独安装 JRE）

#### CentOS

##### JDK 8

	$ sudo yum install -y java-1.8.0-openjdk-devel

##### JDK 7

	$ sudo yum install -y java-1.7.0-openjdk-devel

##### JDK 6

	$ sudo yum install -y java-1.6.0-openjdk-devel

#### Debian & Ubuntu

##### JDK 8

	$ sudo apt-get install -y openjdk-8-jdk

##### JDK 7

	$ sudo apt-get install -y openjdk-7-jdk

##### JDK 6

	$ sudo apt-get install -y openjdk-6-jdk

### 安装运行环境

#### CentOS

##### JRE 8

	$ sudo yum install -y java-1.8.0-openjdk

##### JRE 7

	$ sudo yum install -y java-1.7.0-openjdk

##### JRE 6

	$ sudo yum install -y java-1.6.0-openjdk

#### Debian && Ubuntu

##### JRE 8

	$ sudo apt-get install -y openjdk-8-jre

##### JRE 7

	$ sudo apt-get install -y openjdk-7-jre

##### JRE 6

	$ sudo apt-get install -y openjdk-6-jre

## 配置环境

### 配置开发环境

#### CentOS

	export JAVA_HOME=/usr/lib/jvm/java-openjdk

	export JRE_HOME=/usr/lib/jvm/jre-openjdk

	export CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar

	export PATH=$JAVA_HOME/bin:$PATH

#### Debian、Ubuntu

找到javahome目录
	ls -l /usr/lib/jvm/

配置到nano /etc/profile.d/openjdk.sh

	export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
	export JRE_HOME=$JAVA_HOME/jre
	export CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar
	export PATH=$JAVA_HOME/bin:$PATH

查看java命令配置
update-alternatives --config java
update-alternatives --install java /usr/bin/java /usr/lib/jvm/java-1.8.0-openjdk-amd64/bin/java

### 配置运行环境

#### CentOS

	export JAVA_HOME=/usr/lib/jvm/jre-openjdk

	export PATH=$JAVA_HOME/bin:$PATH

#### Debian、Ubuntu

略

## 更多安装方法

官网：[http://openjdk.java.net/install/](http://openjdk.java.net/install/)
