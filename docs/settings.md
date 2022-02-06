+ 配置环境
- [下载java](https://docs.microsoft.com/zh-cn/java/openjdk/download) 根据你家中的电脑系统来选择java版本
- [idea下载](https://www.jetbrains.com/zh-cn/idea/download/) Community是免费版，推荐大家使用，如果你是学生党，那么可以凭借学生证去申请ULtimate
- [forge下载](https://files.minecraftforge.net/net/minecraftforge/forge/) 选择对应版本号的mdk下载
---
+ 配置安装环境
- 首先，我们需要安装java，idea，forge
- 初学者的idea的设置我推荐不会多少英文的去idea里面找中文语言插件，具体是:
- file-> settings -> plugin -> Marketplace 搜索 chinese/中文 找到 Chinese(Simplified) Language Pack/中文语言包 
- 下载forge mdk 解压到自己喜爱的磁盘内的特定英文文件夹内里面的架构有
---
- 文件夹
  * .gradle
  * .idea
  * build
  * gradle
  * run
  * src
- 文件
  * .gitattributes
  * .gitignore
  * build.gradle
  * CREDITS.txt
  * README.txt
* 等
---
- 我们看看build.gradle文件

示例

    buildscript {
        repositories {
       
            maven { url = 'https://maven.minecraftforge.net' }
            maven { url = 'https://maven.parchmentmc.org' }
        
            mavenCentral()
        }
        dependencies {
            classpath group: net.minecraftforge.gradle, name: ForgeGradle, version: project.forgegradle_version,     changing: true
            classpath "org.parchmentmc:librarian:${project.librarian}"
        }
    }


我们看这几行，repositories相当于依赖文件的获取，dependencies是获取依赖的版本
project.xxx 是把gradle.properties 的xxx变量导入到项目中，它的值是String字符型${xxx}也是

    librarian = 1.+
    forgegradle_version = 5.1.+
    maven { url = 'https://maven.parchmentmc.org' }的添加是为了防止构建的时候产生eula的警告
    其次呢再添加apply plugin: 'org.parchmentmc.librarian.forgegradle'

然后我们再看

    version = project.mod_version
    group = project.group
    archivesBaseName = project.mod_main
    group就是我们的src/main 里面的项目路径例如io.github.overrun
    version是模组的版本号
    archivesBaseName是模组名称
    

build.gradle里面的其他设置

    minecraft{
	      mappings channel: official, version: 1.18.1
    }

    dependencies {
	      minecraft "net.minecraftforge:forge:1.18.1-5.1.+"
    }

最后

    在idea中我们要找到文件->设置 搜索gradle
    找到构建工具中的gradle
    把gradle目录主动转移到其他大空间中，gradle的默认位置在c盘，c盘太小的友友们可以转到其他英文文件夹内
    Gradle JVM选择17版本的java
    文件项目结构里面的SDK也选择17然后确认
    gradle文件夹内的wrapper里面的gradle-wrapper.properties里面的gradle版本修改为7.3.3版本号

删除src/main/java里面所有的文件夹并添加 刚才group的多级层次文件io.github.overrun.模组名字（英文首字母小写）
然后新建JAVA类为你的模组名字（首字母大写）

写入

    @Mod(modid) //forge的注解标识没有这个标识forge无法辨认模组
    public class 模组名字 {
        private static final Logger msg = LogManager.getLogger();//获取log4j 给控制台发送消息
        public 模组名字(){
            msg.info("模组加载modid成功");
        }//实现方法类
    }

然后我们在resources文件夹下META-INF中找到 mods.toml文件我们需要修改

    modId = "abcdefg"   ##你的模组名字英文的全小写
    displayName = "Abc Defg"   ##模组名字
    authors= "authors"  ##作者名字 多个作者用,分开

    dependencies.abcdefg ##你的模组依赖原来是modid的改成你的模组名字