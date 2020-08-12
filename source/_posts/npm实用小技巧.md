---
title: 'npm实用小技巧'
date: 2020-07-27 14:16:50
---
## 初始化包
- `npm init` 询问关于包、作者等信息
- `npm init -y` 自动生成我们的`package.json`
- 配置默认初始化配置，例如作者详细信息deng

    ```
    npm config set init-author-name "Ankit Jain"
    npm config set init-author-email "ankitjain28may77@gmail.com"
    ```
    然后运行`npm init -y`自定生成我们的包
    
    ```
    {
      "name": "<name of the root dir>",
      "version": "1.0.0",
      "description": "",
      "main": "index.js",
      "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
      },
      "keywords": [],
      "author": "Ankit Jain <ankitjain28may77@gmail.com>",
      "license": "ISC"
    }
    ```

## 简约安装包命令

```
# Install package
npm install <package_name>
Shortcut: npm i <package_name>
# Install devDependencies
npm install --save-dev <package_name>
Shortcut: npm i -D <package_name>
# Install dependencies (This is default)
npm install --save-prod <package_name>
Shortcut: npm i -P <package_name>
# Install packages globally
npm install --global <package_name>
Shortcut: npm i -g <package_name>

```
*从`npm 5.x`开始，默认什么参数都不加，自动添加到`dependencies`中*
## main
- 一个常用的npm包
```
{
    main:'lib/index.js'
}
```
指定程序的主入口文件，其他项目引用这个`npm`包时，实际上引入的是`lib/index`中暴露出去的模块

## 全新安装依赖包
- `npm ci`
    - 根据`package-lock.json`安装依赖包，保证团队使用版本完全一致
    - 会删除项目中现有的`node_modules`，重新安装
    - 不会写入`package.json` 安装基本是冻结的
    - 只能一次安装一整个项目，不能安装单独的依赖包
    - 如果`package-lock.json`过时（和`packge.json`冲突），会报错，避免项目依赖陷入过时状态
    - 如果使用它，记得把`package-lock.json`加入`git`仓库
  
## 快速导航到任何npm软件包的文档

- 导航到文档
    ```
    npm docs <package-name>
    OR
    npm home <package-name>
    ```
- 导航到github

    ```
    npm repo <package-name>
    ```

- 导航到github的issue

    ```
    npm bug <package-name>
    ```

## 删除重复的包

- 我们可以通过运行 npm dedupe 命令删除重复的依赖项。 它通过删除重复的程序包并在多个从属程序包之间有效地共享公共依赖项，简化了总体结构。 这样就形成了一个平面且具有重复数据删除功能的树。

    ```
    npm dedupe or npm ddp
    ```

## 列出所有已安装的软件包

- 通过运行 npm list 命令，我们可以列出项目中安装的所有npm包。它将创建一个树结构，显示已安装的包及其依赖项。

    ```
    npm list or npm ls
    ```
- 我们可以使用 —depth 标志来限制搜索深度：

    ```
    npm ls --depth=1
    ```

## NPM scripts
- 列出项目存在的所有npm环境变量

    ```
        npm run env
    ```
    输出
    
    ```
    npm_config_save_dev=
    npm_config_legacy_bundling=
    npm_config_dry_run=
    npm_config_viewer=man
    .
    .
    npm_package_license=ISC                # Package properties
    npm_package_author_name=Ankit Jain
    npm_package_name=npm-tips-and-tricks   # Name of our package

    ```
    可以通过`process.env.npm_package_name`和类似的其他变量在代码中访问上述`env`变量
    
- 在`package.json`中配置自己的变量

    ```
    "config"：{
        "myvariable":"Hello World"
    }
    ```
    使用`npm run env`查看
    
    ![npm run env](https://note.youdao.com/yws/api/personal/file/E81983B86AD34F4997F79D04082E8357?method=download&shareKey=bb4eeee3c7c28ad319d6b898caa069b6)
    
- 运行脚本
    - package.json
    
        ```
        "scripts":{
            "echo-hello":"echo 'Hello'",
            "echo-helloworld":"echo 'Helloworld'"
            "echo-both":"npm run echo-hello && npm run echo-helloworld",
            "echo-both-in-parallel":"npm run echo-hello & npm run echo-helloworld"
        }
        ```
    - 连续运行可使用`&&`
        ```
        npm run echo-both
        # Output
        > npm run echo-hello && npm run echo-helloworld
        > npm-tips-and-tricks@1.0.0 echo-hello 
        > echo "Hello"
        Hello
        > npm-tips-and-tricks@1.0.0 echo-helloworld
        > echo "Helloworld"
        Helloworld
        ```
    - 并行运行`&`
    
        ```
        npm run echo-both-in-parallel
        # Output
        > npm run echo-hello & npm run echo-helloworld
        > npm-tips-and-tricks@1.0.0 echo-hello
        > echo "Hello"
        > npm-tips-and-tricks@1.0.0 echo-helloworld
        > echo "Helloworld"
        Hello
        Helloworld
        ```
- npm命令中使用npm 环境变量使用`$`

    ```
    npm run echo-packagename
    # Output
    > echo $npm_package_name
    npm-tips-and-tricks
    -------------
    npm run echo-myvariable
    # Output
    > echo $npm_package_config_myvariable
    Hello World
    ```
    
- 将参数传递给另一个npm脚本

    ```
    npm run echo-passargument
    # Output
    > npm run echo-packagename -- "hello"
    > npm-tips-and-tricks@1.0.0 echo-packagename
    > echo $npm_package_name "hello"
    npm-tips-and-tricks hello

    ```

## 脚本跨平台兼容 
- 安装开发依赖项 cross-env

    ```
    npm i -D cross-env
    ```

- 使用在任何环境变量之前包括关键字cross-env，就像这样：

    ```
    {
      "scripts": {
        "build": "cross-env NODE_ENV=production webpack --config build/wepack.config.js"
      }
    }
    ```

## 在不同的目录中运行脚本
- 方法一 手动cd
 
    ```
    cd folder && npm start && cd ..
    ```

- 方法二 指定路径
    
    ```
    npm start --prefix path
    ```

## 并行运行脚本
- 安装开发依赖

    ```
    npm i -D concurrently
    ```
- 然后按照以下格式将其添加到脚本中

    ```
    {
    "start": "concurrently \"(npm start --prefix client)\" \"(npm start --prefix server)\"",
    }
    ```
- 延迟运行脚本直到端口准备就绪

    例如，这是我在使用React前端的Electron项目中使用的dev脚本。 同时使用，脚本并行加载表示层和Electron窗口。 但是，使用wait-on，只有在 http://localhost:3000 启动好，才会打开Electron窗口。

    ```
    "dev": "concurrently \"cross-env BROWSER=none npm run start\" \"wait-on http://localhost:3000 && electron .\"",
    
    ```

- 列出并选择可用脚本
    - 方法一

        ```
        npm run
        ```
    - 方法二 全局安装 NTL (npm任务列表)模块:

        ```
        npm i -g ntl
        ```
        效果如下：
        
        ![](https://note.youdao.com/yws/api/personal/file/C93F234742134A32841BC74102CB0936?method=download&shareKey=52fa62500654a44d1ea75a3b1ea9a5b1)
