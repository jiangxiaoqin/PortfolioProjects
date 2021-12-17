**Java环境搭建**

[TOC]

# JDK下载和环境变量配置

## Java下载

JDK(Java Development Kit)：Java开发工具包
共享盘：Z:\Public\IT-DownloadCenter\Developer\jdk-11.0.9+11.zip

将下载的文件放到D:\Java目录下，并解压到当前文件夹。

## 配置Java环境变量

1.在桌面上，右击【此电脑】->【属性】

![](C:\Users\Admin\Pictures\此电脑-属性.png)



2.点击【高级系统设置】

![image-20210219110526608](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110526608.png)



3.点击【环境变量】

![image-20210219110623227](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110623227.png)



4.点击【系统变量->新建】

![image-20210219110723044](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110723044.png)

5.然后输入固定的变量名JAVA_HOME，变量值选择jdk的目录，然后点击【确定】

![image-20210219110910845](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219110910845.png)



6.在系统变量中，往下翻选中【Path】后，点【编辑】

![image-20210219111447988](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219111447988.png)



7.点击【编辑】，输入%JAVA_HOME%\bin并【确定】，将所有的【确定】点击，即完成了Java配置。

![image-20210219111549292](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219111549292.png)



8.验证Java配置，输入cmd回车

![image-20210219112011011](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219112011011.png)

输入java -version后看到如下截图信息，即表示Java配置成功。

![image-20210219112113763](C:\Users\Admin\AppData\Roaming\Typora\typora-user-images\image-20210219112113763.png)



# IDEA安装

安装文件，所在共享目录：Z:\Public\IT-DownloadCenter\Developer\IDE

![image-20210608123016771](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608123016771.png)

ideaIU-2020.2.4.exe是安装文件，ide-eval-resetter-2.1.6.jar永久试用破解方法



# 自带Maven配置

File->Settings->搜索maven

![image-20210608122557000](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608122557000.png)



在settings.xml中设置阿里云仓库，下载Jar包更快。

```xml
  <mirror>
      <id>aliyunmaven</id>
      <mirrorOf>*</mirrorOf>
      <name>阿里云公共仓库</name>
      <url>https://maven.aliyun.com/repository/public</url>
  </mirror>
```



# 下载代码并启动项目

自行去下载searcheway-java项目，在IDEA中打开指定项目：

File->Open 然后选择项目所在路径即可，会提示是否作为Maven Project，选择是，会自动进行Jar包下载。

本地启动项目，建议屏蔽nacos（后续考虑会删除nacos）

searchway-api模块的启动类：ApiApplication，将以下代码注释：

![image-20210608130139014](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608130139014.png)



项目启动配置文件：searcheway-java/config/application.yml

![image-20210608125734519](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608125734519.png)

还有redis、mq、数据库等配置。

143开发环境使用的最新的、最稳定的数据库，会统一为以下4个名称不变：

业务库：businessdata

化学库：chemicalinfo

ELN库：eln

BB库：buildingblock

画图需要配置：

![image-20210608130559336](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608130559336.png)

ChemAxon的License所在共享目录：Z:\Public\SharedSpace\License.zip

在D盘新建work目录，然后将License.zip放到work目录，然后直接解压到当前文件夹即可。



SpringBoot2.5.0所需的启动配置：

![image-20210608130833995](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608130833995.png)

单击之后如下：

![image-20210608131008600](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608131008600.png)

SPRING_CONFIG_LOCATION=optional:file:./config/

输入配置，然后点击OK即可。

本地Jar包引入：Z:\Public\SharedSpace\ChemAxon-Jar\lib 将ChemAxon相关的jar包，复制到以下截图的lib目录下即可。

![image-20210608153924222](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608153924222.png)



编译项目：

![image-20210608131255361](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608131255361.png)

编译成功之后，终于可以启动项目了：

![image-20210608131408304](C:\Users\chengsl\AppData\Roaming\Typora\typora-user-images\image-20210608131408304.png)

选择启动类ApiApplication，然后点击小虫图标，debug启动。

浏览器输入：localhost:9998/swagger-ui/

以后启动，尽量先更新代码，然后clean、compile成功，最后启动项目。







