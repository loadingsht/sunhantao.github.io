---
layout: post
comments: true
categories: cocos lua
---
## Mac下编码调试Cocos2dx-lua的工具



### 环境

- Mac: 10.11.3 
- Xcode: 7.2.1
- Cocos + CocosStudio: 3.10。其实大部分用quick-cocos2d-x开发，但它已经合并到cocos里了，对应位置：

        /Applications/Cocos/Cocos2d-x/cocos2d-x-3.10/cocos/scripting/lua-bindings/script/framework/

- Lua: 5.1.4
- Zerobrane: 1.30 免费跨平台lua调试器。
- atom: 1.5.2 配合插件language-lua可以写lua代码，写着比Zerobrane舒服。（Cocos Code IDE暂停维护，关注后续发展）

### 工作流程

1. 把需要的开发软件下好
- API文档准备好：
  + [cocos2dx API](http://api.cocos.com/cn/)，页面右侧有lua，js，c++可选项。
  + quick-cocos2d-x API文档一份。github上clone [quick-cocos2d-x](https://github.com/chukong/quick-cocos2d-x)，API首页在：
      quick-cocos2d-x/docs/api/index.html

- 建议在[cocos文档](http://www.cocos.com/doc/)中熟悉Cocos和cocos2dx的概念，lua其实和c＋＋的概念是一样的，api也都类似，如果遇到坑可以试着解决（cocos你懂的）
- 首先在Cocos中建立工程。
- 在Cocos Studio中编辑UI。
- 导出xcode工程后，用atom编码。
- 调试：
  + 将Zerobrane的mobdebug.lua文件拷贝到项目的src目录：
  
            /Applications/ZeroBraneStudio.app/Contents/ZeroBraneStudio/lualibs/mobdebug/mobdebug.lua
    
    cocos2dx的lua-empty-test/src中也有这个文件，但是版本不一样。两个文件调试结果暂时没有发现差别。
  + 在项目的main.lua中填加两句：
  
  ```lua
  mobdebug = require "mobdebug"   -- 第一句
  require "config"
  require "cocos.init"

  local function main()
    mobdebug.start()  -- 第二句
    require("app.MyApp"):create():run()
  end
  ```
  
  + 打开ZeroBrane，加载项目的src文件。
  + 打开ZeorBrane->Project->Start Debugger Server。
  + 设置断点。
  + 在xcode中用模拟器运行项目工程，可以看到断点生效了。

- 真机测试、打包，待续...。
