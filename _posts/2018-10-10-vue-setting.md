---
title: vscode下VUE开发环境配置
categories:
  - linux
tags:
  - linux
  - systemd
---

1. 安装 VSCODE 插件

   - atom one dark
   - material icon
   - Vue Development Extension Pack (这是一个 VUE 开发环境的包)

2. 安装`npm`插件

```
npm install -g eslint-config-with-prettie
```

3. 打开设置窗口


    * 从打开`文件`->`首选项`->`设置`
    * 在`扩展`栏中随便找一个插件设置，并且下啦找到`在setting.json中编辑`
    * 打开`setting.json`

4. 往`setting.json`写入设置

```
{
  // 0- 使用说明:下载(修改setting.json1 为json) || 直接复制文本到setting.json
  // 0- 总原则:Less is More
  // 0- 插件配置原则:够用即可,不贪婪插件,绝对不装功能重复的,比如各种snippet,蛋疼
  // 0- snippet配置原则:我一般很少用别人的snippet,一下太多了,掌握不了,更不利于熟练运用.用到什么就把snippet加到自己的snippet中
  // 0- 界面原则:能不显示的就不显示(比如minimap,)需要显示的底部状态栏,顶部文件栏(仅此而已),半显示的(explorer(alt+.),menu(alt)),全屏不是很喜欢,影响其他功能
  // 1- 主题 Theme------------------------------------------ 需要安装atom one dark 和 material icon
  "workbench.colorTheme": "Atom One Dark", // atom 主题,字体配色好,比 Material配色舒服  sublime直接是 material
  "workbench.iconTheme": "material-icon-theme", // icon主题 material
  "material-icon-theme.folders.theme": "specific", // spaecific风格
  "material-icon-theme.activeIconPack": "angular_ngrx", //主题样式
  "material-icon-theme.hidesExplorerArrows": true, //隐藏图标箭头
  // 2- 字体 Font---------------------------------------------
  // 关于注释为什么是斜体,也是非常纠结啊,中文斜体不好看,英文斜体很漂亮,真是鱼与熊掌
  //"editor.fontFamily": "Consolas,'Microsoft yahei", // 英文:consolas 中文:雅黑
  // "editor.fontSize": 20, // 字号
  // "editor.lineHeight": 40, // 行高
  // 3- 显示 view-----------------------------------------------
  "window.zoomLevel": 0, //视窗缩放
  "editor.renderWhitespace": "all", // 显示空格,写代码嘛,显示空格舒服,区分tab和空格 ,''和 ' '
  "workbench.activityBar.visible": true, // 显示右侧快捷菜单 alt+shift+. 切换
  "editor.minimap.enabled": false, // 不显示右侧 minimap
  "workbench.statusBar.visible": true, // 显示状态条
  //"window.menuBarVisibility": "toggle", //隐藏菜单栏
  "explorer.openEditors.visible": 0, //最近打开的文件不显示
  // 5- 起始页 startup -----------------------------------------
  "workbench.startupEditor": "none", // 起始页啥也不显示
  // 14- 烦人的括号匹配matchBrackets ----------------------------------------------- 需要安装Subtle Match Brackets
  // "editor.matchBrackets": false, // 干掉原先的丑陋的恼人的匹配
  // "subtleBrackets.style": {
  //   // 换上我们漂亮的小金条
  //   "global": {
  //     "borderColor": "GoldenRod",
  //     "borderWidth": "4px"
  //   }
  // },
  // 使用插件格式化 html
  "vetur.format.defaultFormatter.html": "prettyhtml",
  // 格式化插件的配置
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      // 属性强制折行对齐
      "wrap_attributes": "force-aligned"
    },
    "prettyhtml": {
      "printWidth": 200,
      // "singleQuote": true,
      "wrapAttributes": false,
      "sortAttributes": true
    },
    "prettier": {
      "printWidth": 200,
      "singleQuote": true,
      "wrapAttributes": false,
      "sortAttributes": true,
      "semi": false
    }
  },
  "editor.matchBrackets": false,
  "git.enableSmartCommit": true,
  "git.confirmSync": false,
  "files.exclude": { // 文件夹不显示
        "**/node_modules": true
  },
}
```

5. 修改项目根目录下的`eslint`设置

```
  // https://github.com/standard/standard/blob/master/docs/RULES-en.md
  // extends: 'standard',
  "extends": ["prettier", "prettier/react"],
  // required to lint *.vue files

  // add your custom rules here
  rules: {
    //关闭函数括号前空格验证
    'space-before-function-paren': 'off',
    // allow async-await
    'generator-star-spacing': 'off',
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
  },
  "files.watcherExclude": {
    "**/.git/objects/**": true,
    "**/.git/subtree-cache/**": true,
    "**/node_modules/*/**": true
  }
```

## 问题解决

```
ERROR in ./src/main.js
Module build failed: Error: Cannot find module 'eslint-config-prettier/react'
Referenced from: /home/workspace/jenkins_home/workspace/ares-admin-ui/.eslintrc.js
    at ModuleResolver.resolve (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/util/module-resolver.js:74:19)
    at resolve (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config/config-file.js:515:25)
    at load (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config/config-file.js:532:26)
    at configExtends.reduceRight (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config/config-file.js:424:36)
    at Array.reduceRight (<anonymous>)
    at applyExtends (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config/config-file.js:408:28) at Object.load (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config/config-file.js:566:22)
    at loadConfig (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config.js:63:33)
    at getLocalConfig (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config.js:130:29)
    at Config.getConfig (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/config.js:260:26)
    at processText (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/cli-engine.js:224:33)
    at CLIEngine.executeOnText (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint/lib/cli-engine.js:754:26)
    at lint (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint-loader/index.js:211:17)
    at Object.module.exports (/home/workspace/jenkins_home/workspace/ares-admin-ui/node_modules/eslint-loader/index.js:206:21)
 @ multi babel-polyfill ./src/main.js
```

解决办法

```
npm install -g eslint-config-prettie
```
