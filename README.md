# solr
##### 一.安装jdk 
  1.下载jdk：(本版本1.8) 链接：https://pan.baidu.com/s/1kZ0fQ6KZoqENR56VI6LPiA 提取码：1234
	
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

		
##### 二.安装tomcat
  1.下载tomcat：(本版本8) 链接：https://pan.baidu.com/s/18iU2_MUjS_kwtO_FL8QWuw 提取码：1234
	
  2.下载后传到服务器解压
  
	tar xzvf apache-tomcat-8.5.72.tar.gz
	mv apache-tomcat-8.5.72 tomcat-8


##### 三.安装solr
  1.下载solr：(本版本8.11.0) 链接：https://pan.baidu.com/s/10dlGUhbrCpBH9f-WrsextA 提取码：1234
	
  2.下载后传到服务器解压
  
	tar xzvf solr-8.11.0.tgz

  3.启动solr
  	
	cd /data/app/solr-8.11.0/bin
	./solr start -p 8983 -force
  	
    提示warn
    *** [WARN] ***  Your Max Processes Limit is currently 15066.
    修改 bin目录下solr.in.sh 
    
    	vi solr.in.sh 
    
    将 #SOLR_ULIMIT_CHECKS=false either here or as part of your profile.
    改为
    	SOLR_ULIMIT_CHECKS=false 
	#either here or as part of your profile.
    再启动

