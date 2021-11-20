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


##### 四.移植到Tomcat服务器上
  1.进入到Solr的/server/solr-webapp下面，将webapp复制到Tomcat下面的webapps，并且重命名为solr
  
  	cp -r webapp  /data/app/tomcat-8/webapps/solr8
  
  2.复制关键架包
    2.1 复制solr/dist下面的solr-dataimporthandler-*.jar到Tomcat下的WEB-INF/lib下
    
    	cp solr-dataimporthandler-*.jar /data/app/tomcat-8/webapps/solr8/WEB-INF/lib/

    2.2进入到/server/lib/ext目录，将里面（下面）的所有架包复制
    
    	cd /data/app/solr-8.11.0/server/lib/ext/
	cp * /data/app/tomcat-8/webapps/solr8/WEB-INF/lib/
	
    2.3进入到/server/lib目录，把里面以metrics开头的架包全部复制
    
    	cd /data/app/solr-8.11.0/server/lib
	cp metrics*.jar /data/app/tomcat-8/webapps/solr8/WEB-INF/lib/
	
  3.复制配置文件 进入到/server/resources目录，将里面关于log4j的配置都进行复制 进tomcat/solr/WEB-INF/ 创建classes目录存放配置文件
  	
	cd /data/app/solr-8.11.0/server/resources/
	cp log4j*.xml /data/app/tomcat-8/webapps/solr8/WEB-INF/classes/
  
  4.创建solr-home 目录
  
  	cd /data/app/solr-8.11.0/
	mkdir solr-home
  
  4.编辑Tomcat下Solr的web.xml文件
  
  	cd /data/app/tomcat-8/webapps/solr8/WEB-INF/
	vi web.xml
      添加内容
      	<env-entry>
		<env-entry-name>/solr/home</env-entry-name>
		<env-entry-value>/data/app/solr-8.11.0/solr-home</env-entry-value>
		<env-entry-type>java.lang.String</env-entry-type>
	</env-entry>
	
      注释下面内容	
	
	  <!-- Get rid of error message -->
	 <!-- <security-constraint>
	    <web-resource-collection>
	      <web-resource-name>Disable TRACE</web-resource-name>
	      <url-pattern>/</url-pattern>
	      <http-method>TRACE</http-method>
	    </web-resource-collection>
	    <auth-constraint/>
	  </security-constraint>-->
    
  5.复制配置文件
  	
	cd /data/app/solr-8.11.0/server/solr
	cp -rf * /data/app/solr-8.11.0/solr-home/
	
  6.启动tomcat 通过8080端口访问

  	
