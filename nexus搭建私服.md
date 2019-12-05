## 利用nexus搭建maven私服仓库
### 1、官网下载 Nexus Repository Manager的安装包，下载地址为：https://www.sonatype.com/download-oss-sonatype
### 2、解压安装包tar -zxvf /home/nexus-2.14-bundle.tar.gz -C /usr/local/nexus/
### 3、解压后修改/usr/local/nexus/nexus-2.14/bin/nexus中设置run_as_user=root 、 run_as_root=false
### 4、启动/usr/local/nexus/nexus-2.14/bin/nexus start
### 5、初始登录账户admin 密码在/usr/local/nexus/sonatype-work/nexus3/admin.password中
### 6、登录成功后，选择左边 Views/Repositories 菜单下的 Repositories，可以看到一些预设的仓库，我们会用到的一般只有 Public Repositories 和 3rd party ， Public Repositories 为公共仓库，3rd party 为第三方仓库，可以上传第三方的 Jar （当然也可以是自己封装的 Jar），其实在Nexus仓库中，一个仓库一般分为public(Release)仓和SNAPSHOT仓，前者存放正式版本，后者存放快照版本。如果在项目配置文件中（无论是build.gradle还是pom.xml）指定的版本号带有’-SNAPSHOT’后缀，比如版本号为’Junit-4.10-SNAPSHOT’，那么打出的包就是一个快照版本。https://blog.csdn.net/wangb_java/article/details/66000956
### 7、上传jar到3rd party后，在maven项目中pom文件添加如下代码，即可使用
	<repositories>
        <repository>
            <id>nexus</id>
            <url>http://host:port/nexus/content/groups/public/</url>
        </repository>
    </repositories>
