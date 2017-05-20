# homebrew文档
## 目录
- [安装](#install)
- [常用命令](#normalAdmin)
- [常见问题](#Q)
    - [权限问题](#rootQ)

## <a name="install">安装</a>
官网，可以去这里看：https://brew.sh/
安装：打开终端，直接输入下面的命令
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## <a name="normalAdmin">常用命令</a>
### 安装软件
```
brew install <软件名称>
```

### 卸载软件
```
brew remove <软件名称>
```

### 清除下载的安装包
```
brew cleanup
```

### brew升级
```
brew update
```

### 升级软件
```
brew <软件名称> upgrade
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