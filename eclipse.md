# Eclipse使用说明
在这里做一个eclipse使用的相关笔记

## 目录
- [常规配置](#normal)
    - [字体大小](#font)
    - [背景色](#bgc)
    - [Tab切换4空格](#tab)


## <span name="normal">常规配置</span>
### <span name="font">字体大小</span>
```
打开eclipse
    ->偏好设置
        ->General
            ->Apperance
                ->Colors and Fonts，右侧Basic->Text Font，编辑，选字字号，保存。
```

### <span name="bgc">背景色</span>
```
打开eclipse
    ->偏好设置
        ->General
            ->Editors
                ->Text Editors，右侧最下面，选择Background color，颜色使用C7EDCC，保存。
```

### <span name="tab">Tab切换4空格</span>
```
打开eclipse
    ->偏好设置
        ->General
            ->Editors
                ->Text Editors，勾选insert space for tab
                
打开eclipse
    ->偏好设置
        ->Java
            ->Code Style
                ->Formatter，右侧new
                在Profile name中自己取个名字，然后下面选择Eclipse [built-in]，点击ok。
                然后在Acrive profile中选择自己创建的，点击Edit。
                Tab policy选择Spaces only，下面连个size写4即可。保存。
```
