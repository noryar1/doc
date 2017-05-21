# git手册

## 目录
- [安装与配置](#install)


## <a name = "install">安装与配置</a>
### 1. mac：使用brew进行安装
```
brew install git
```
### 2. 配置：
```
git config --global user.name "用户名"
git config --global user.email "用户email"
```
### 3. 配置ssh
```
cd ~ 
看看有没有.ssh目录，如果有cd .ssh
ls 看看有没有id_rsa.pub或id_dsa.pub，有的话备份并删除
ssh-keygen -t rsa -C "用户email"
一路回车即可
参数解释：
-t 指定密钥类型，默认是 rsa ，可以省略。
-C 设置注释文字，比如邮箱。
-f 指定密钥文件存储文件名。
```

### 4. 配置github
```
vi id_rsa.pub，把里面的内容复制
进入github，右上角个人中心->setting，左侧进入ssh配置，将复制的密钥粘贴即可。
```