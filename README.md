# solr
##### 一.安装jdk 
  1.下载jdk：(本版本1.8) 链接：https://pan.baidu.com/s/1vxBOi4p-2zQ3SPA_kEsTEQ 提取码：1234 
	
  2.下载后传到服务器解压
  
	tar xzvf jdk-8u311-linux-x64.tar.gz 
	
  3.添加环境变量 vim /etc/profile 配置javahome 
  
		export JAVA_HOME=/data/app/jdk1.8.0_311
		export JRE_HOME=${JAVA_HOME}/jre
		export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib:$CLASSPATH
		export JAVA_PATH=${JAVA_HOME}/bin:${JRE_HOME}/bin
		export PATH=$PATH:${JAVA_PATH}

  4.保存刷新并检查是否成功

		source /etc/profile
		java -vsersion

		
##### 一.安装jdk 

