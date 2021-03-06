# NPM

> 有趣的事实是`npm`[不是一个缩写](https://twitter.com/npmjs/status/347057301401763840)，因此它不能展开，但是我们通常把它叫做`node package manage`。

`npm`是一个二进制，默认随着`node`的安装，用于管理社区分享的 JavaScript/TypeScript 包。

- NPM 包部署在（从这里安装）[https://www.npmjs.com/](https://www.npmjs.com/)（云上）


### 快速常见设置

- npm 包使用`package.json`配置。你可以使用`npm init -y`快速生成一个文件。
- 包被安装到一个`./node_modules`文件夹。通常将这个文件放到你的`.gitignore`


> 即使你可能正在构建一个应用，一个`package.json`也让你的项目成为一个包。因此，术语`project | package`可以互换。

当你检出某个人的（你的团队的）包，它将会包含一个`package.json`，并且列出运行这个项目需要的依赖。你只需要运行`npm install`，npm 就会将他们从云端拉下来

### 安装一个包

你可以运行`npm install <something>`。大部分人们将会使用简短的`npm i <something>`，比如：
```ts
// Install react
npm i react
```

> 这也会自动添加`react`到你的`package.json`的依赖。

### 安装一个 devDependency

`devDependencies`是只在开发阶段需要的依赖，如果你的项目在考法之后不需要。

`typescript`通常在`devDependencies`，因为它只在构建`.ts -> .js`的时候需要。你通常部署构建的`.js`文件：
- 进入产品模式
- 或供给其他 npm 消费

### 安全

公开的`npm`包被全世界的安全团队扫描，并报告给 npm 团队。然后他们发布问题详细的安全建议和潜在修复。常见的修复是简单更新包。

你可以通过简单运行`npm audit`来审查你的 node 项目。这将会高亮包内/依赖的任何漏洞。
```
┌───────────────┬──────────────────────────────────────────────────────────────┐
│ Low           │ Regular Expression Denial of Service                         │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Package       │ debug                                                        │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Dependency of │ jest [dev]                                                   │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ Path          │ jest > jest-cli > istanbul-lib-source-maps > debug           │
├───────────────┼──────────────────────────────────────────────────────────────┤
│ More info     │ https://nodesecurity.io/advisories/534                       │
└───────────────┴──────────────────────────────────────────────────────────────┘
```

注意问题通常在 development 依赖找到（比如，这个例子是 jest）。因为这不是产品部署的一部分，大部分你的产品应用没有漏洞。但是保持漏洞为`0`依旧是一个好的实践。

简单的添加`npm audit`（在错误的时候命令行使用错误码 1 退出）作为你部署的一部分去确保项目保持更新。

### npm 脚本

#### 脚本中的`--`是什么


你可以构建一个基本脚本，使用有限集合的命令行参数，比如这是一个脚本，目标是为 TypeScript 编译器去运行`tsc`：
```ts
{
  "scripts": {
    "build": "tsc -p ."
  }
}
```

你可以在`--`之后传递任意多个你想要的标志。比如，在下面的例子`build:more`和`something --foo -f -d --bar`有相同的效果。
```
{
  "scripts": {
    "build": "something --foo",
    "build:more": "npm run build -- -f -d --bar"
  }
}
```

### 公开和私有的包

你不需要这个，当使用任何常见公开 npm 包的时候。只知道这是为企业/贸易客户的。

#### 公开的包

- 包默认是公开的
- 任何人可以部署一个包到 npm
- 你只需要一个账号（你可以免费得到）

下载一个公开的包不需要账号

包的自有分享是 npm 成功的主要原因之一。

#### 私有的包

如果你的公司/团队/企业想要一个私有包，你需要注册一个简单的计划，详细在这里：[https://www.npmjs.com/pricing](https://www.npmjs.com/pricing)。

当然，你需要一个有权限的账户去下载一个私有的包。