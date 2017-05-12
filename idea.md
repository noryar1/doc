# idea使用手册

## 目录
- [安装](#install)
- [基本配置](#setting)
    - [按键设置](#keymap)
    - [jdk设置](#jdk)
    - [maven启动项目](#mavenrun)

## <a name="install">安装</a>
下载安装dmg文件，打开，选择License server：http://idea.iteblog.com/key.php

## <a name="setting">基本配置</a>
### <a name="keymap">按键设置</a>
```
打开idea，左上角
        ->preferences，搜索keymap，设置为eclipse按键风格
```

### <a name="jdk">jdk设置</a>
在idea右上角找到Project Structure图片![projectStructure](./idea/projectStructure.png)。
```
进入以后选择左侧菜单
        ->Global Libraries，选择+号，JAVA
            ->路径一般使用/Library/Java/JavaVirtualMachines/java版本//Contents/Home
        这个时候有，一般在Global Libraries菜单上面的SDKs就能看到自己配置的了。
        
        进入->Peoject菜单，选择刚才配置的jdk，保存
```
过程如图：
![jdk](./idea/jdk.png)

### <a name="mavenrun">maven启动项目</a>
1. 找到配置位置：
    ![](./idea/mavenrun1.png)
2. 选择Edit Configuration，新增一个，选择Maven，右侧选择项目，起名字，配置JVM参数。
3. 回到主界面，配置右侧有个绿色箭头，点击启动。