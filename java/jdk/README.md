# JDK


linux环境配置JDK
```
#编辑文件
vim /etc/profile

#添加环境变量
export JAVA_HOME=/fw/java/jdk1.8.0_191
export JRE_HOME=${JAVA_HOME}/jre
export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH
export JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin
export PATH=$PATH:${JAVA_PATH}

#激活
source /etc/profile
```

