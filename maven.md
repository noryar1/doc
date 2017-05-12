# Maven使用手册

## 目录
- [介绍](#introduction)
- [常见插件](#commonPlugins)
    - [编译插件](#compilerPlugin)
    - [tomcat插件](#tomcatPlugin)

## <a name="introduction">介绍</a>


## <a name="commonPlugins">常见插件</a>
### <a name="compilerPlugin">编译插件</a>
```
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
        <source>1.7</source>
        <target>1.7</target>
        <encoding>UTF-8</encoding>
    </configuration>
</plugin>
```

### <a name="tomcatPlugin">tomcat插件</a>
```
<plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
    <configuration>
        <port>8080</port>
        <path>/</path>
        <uriEncoding>UTF-8</uriEncoding>
        <finalName>agile</finalName>
        <server>tomcat7</server>
    </configuration>
</plugin>
```