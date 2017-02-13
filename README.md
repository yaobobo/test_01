
How To Build Richui2(for windows os)
A\
 Install necessary tools: 
JDK7
JDK环境变量配置：
	下栏：JAVA_HOME :刚刚安装的路  path：;%JAVA_HOME%\bin;
上栏：CLASS_PATH：.;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
java -version 测试是否安装成功
2)	Tomcat7
 Tomcat7环境变量配置:
下栏：CATALINA_HOME：刚刚安装的路径
输入http：//localhost:8080.如果出现下面的内容说明成功了
  3) Python 3.3.4 
  4) ant 1.9.3
ant 环境变量配置:
ANT_HOME值为F:\cocos2d-x\apache-ant-1.9.4
path值为F:\cocos2d-x\apache-ant-1.9.4\bin
classpath的值为F:\cocos2d-x\apache-ant-1.9.4\lib

  5) Git
  7) Ruby
  6) Sencha CMD 4.0.0.203 (for richui2)
node.js


Fork and checkout related projects: Peridot, KIWI
Do some settings: 
Tomcat: add the following line to bin/startup.bat
set INTERMAIL=rme://rwc-hinoki05:5003

or

set INTERMAIL=rme://rwc-hinoki07:5000
Change ect/hosts file: add the following lines to c:/windows/system32/drivers/etc/hosts
172.26.80.109 rwc-hinoki01 rwc-hinoki01.owmessaging.com
172.26.80.114 rwc-hinoki02 rwc-hinoki02.owmessaging.com
172.26.80.113 rwc-hinoki03 rwc-hinoki03.owmessaging.com
172.26.80.111 rwc-hinoki04 rwc-hinoki04.owmessaging.com
54.241.27.99 rwc-hinoki05 rwc-hinoki05.owmessaging.com
54.241.28.137 rwc-hinoki06 rwc-hinoki06.owmessaging.com
54.215.3.137 rwc-hinoki07 rwc-hinoki07.owmessaging.com
10.171.9.19 rwc-hinoki08 rwc-hinoki08.owmessaging.com
54.176.96.97 rwc-ux01 rwc-ux01.owmessaging.com

Build project: run the following command at first time(at least) under your local  kiwi fork directory
 ant -Dsdk.client.home=[your local peridot fork directory]  -Dclient.mode=dev -Dclient.type=both -Dconnector=octane  ubi
Once build successfully at the first time, if you then
want to build as fast as a rocket? Add the following parameter 
-Dskip.resolve  	(build without resolve resource from server everytime)
 just want to build sass file, run this command:
ant -Dsdk.client.home=[your local peridot fork directory]  -Dclient.mode=dev -Dclient.type=rich compile-css
Use these account to login:  08032153623~08032153626 password: p


**** Cross domain api request

1) change browser's lanuch parameter
–- chrome: add these parameters to its launch command
	--args --disable-web-security  --user-data-dir

2) change data request url 
– Webtop.js (QA's build)

 options.url = 'http://172.26.203.54:8080/kiwi-2.1.109/' + options.url;
            //options.url = 'http://rwc-hinoki06:8080/kiwi-uxdevelop/' + options.url;
        }
– JsonRpc.js

if(requestConfig.url){
         requestConfig.url = 'http://172.26.203.54:8080/kiwi-2.1.109/' + requestConfig.url;
            //requestConfig.url = 'http://rwc-hinoki06:8080/kiwi-uxdevelop/' + requestConfig.url;
        }

==== enhanced code snippet
- Webtop.js
var cross = Common.util.ApplicationUtil.getQueryParam('cross'); // rwc-master => ['rwc', 'master'], qa-2.1.111 => ['qa', '2.1.111']
        if (cross) {
            cross = cross.split('-');
            options.url = {
                            rwc: 'http://rwc-hinoki06.owmessaging.com:8080/',
                            qa: 'http://172.26.203.54:8080/',
                            qacpms: 'https://172.26.203.57:8443/'
                        }[cross[0]] + 'kiwi-' + cross[1] + '/' + options.url;
        }

--JsonRpc.js
var cross = Common.util.ApplicationUtil.getQueryParam('cross'); // rwc-master => ['rwc', 'master'], qa-2.1.111 => ['qa', '2.1.111']
        if (cross) {
            cross = cross.split('-');
            requestConfig.url = {
                            rwc: 'http://rwc-hinoki06.owmessaging.com:8080/',
                            qa: 'http://172.26.203.54:8080/',
                            qacpms: 'https://172.26.203.57:8443/'
                        }[cross[0]] + 'kiwi-' + cross[1] + '/' + requestConfig.url;
        }



**** Use QA's server in webtop.xml

* config info page: https://village.owmessaging.com/display/EN/E2E+evironment+-+QE+Lab

* login account:
	rwc: dev01~05/p
	qa: violin1~7@openwave.com/p
	qacpms: u20~30@openwave.com/p
