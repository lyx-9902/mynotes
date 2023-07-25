## npm 中的package.json

## 1. npm

package又叫node package manager  包管理器

## 2. package.json

作用是： 项目中都是用了什么包， 相互依赖关系是什么。 node_modules丢失了，怎么恢复，留作备案。

我们建议每个项目总都要有一个package。json文件（报表数文件，就像产品的说明书一样，给人踏实的感觉。）

如何备案  :   npm install  art-template --save        这个save就是保存依赖信息  

存放位置是   package.json  中的   "dependencies": {
                                                    "jquery": "^3.5.1"
                                                                                         }



### 3.作用： 

如果node_modules 删除了， 命令行中执行npm install ， 会自动下载依赖项。



### 4.向导方式 init

```
 npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (test)
version: (0.0.1)
git repository:
keywords:
license: (ISC)
About to write to C:\Users\luyunxiao\Desktop\node\test\package.json:

{
  "name": "test",
  "version": "0.0.1",
  "description": "鎻忚堪锛氳繖鏄竴涓祴璇曢」鐩?,
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "lyx",
  "license": "ISC"
}


Is this OK? (yes) y

```

