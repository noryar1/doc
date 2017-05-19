# homebrew文档
## 目录
- [安装](#install)
- [常用命令](#normalAdmin)
    - [安装软件](#softInstall)
    - [卸载软件](#removeSoft)
- [常见问题](#Q)
    - [权限问题](#rootQ)

## <a name="install">安装</a>
官网，可以去这里看：https://brew.sh/
安装：打开终端，直接输入下面的命令
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## <a name="normalAdmin">常用命令</a>
### <a name="softInstall">安装软件</a>
```
brew install <软件名称>
```

## <a name="removeSoft">卸载软件</a>
```
brew remove <软件名称>
```

## <a name="Q">常见问题</a>
### <a name="rootQ">权限问题</a>
如果安装完软件，提示如下：
```
Homebrew: Could not symlink, /usr/local/bin is not writable

```
解决如下：
```
sudo chown -R `whoami`:admin /usr/local/bin
sudo chown -R `whoami`:admin /usr/local/share
```