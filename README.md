# Vega: A Visualization Grammar

<a href="https://vega.github.io/vega/examples">
<img src="https://vega.github.io/vega/assets/banner.png" alt="Vega Examples" width="900"></img>
</a>

**Vega** is a *visualization grammar*, a declarative format for creating, saving, and sharing interactive visualization designs. With Vega you can describe data visualizations in a JSON format, and generate interactive views using either HTML5 Canvas or SVG.

**Vega**是一套可视化图形语法，用于声明式地创建、保存和分享可交互的可视化设计。使用Vega，可以使用JSON格式来描述并创建(使用Canvas或SVG)可交互的数据可视化视图。

For documentation, tutorials, and examples, see the [Vega website](https://vega.github.io/vega). For a description of changes between Vega 2 and later versions, please refer to the [Vega Porting Guide](https://vega.github.io/vega/docs/porting-guide/).

了解文档，教程和示例，可以查看[Vega website](https://vega.github.io/vega)。需要查看最新版本和Vega 2版本之间的详细更改，请移步至[Vega Porting Guide](https://vega.github.io/vega/docs/porting-guide/)。

Are you using Vega in a web application built with a bundler such as [Webpack](https://webpack.js.org/) or [Browserify](http://browserify.org/)? If so, and you _do not need server-side rendering support_, you might prefer using [vega-lib](https://github.com/vega/vega-lib) to include Vega in your app. The vega-lib repository also houses our general test suite.

## Build Instructions

For a basic setup allowing you to build Vega and run examples:

- Clone `https://github.com/vega/vega`.
- Run `yarn` to install dependencies. If you don't have yarn installed, see https://yarnpkg.com/en/docs/install. (If you do not wish to install yarn, you can alternatively run `npm install`. However, you will not be guaranteed to have dependencies matching those of the current release.)
- Once installation is complete, use `yarn build` to build output files.

This repository includes the website and documentation in the `docs` folder. To launch it, run `bundle install` and `bundle exec jekyll serve` in the `docs` folder. The last command launches a local webserver. Now, you can open [`http://127.0.0.1:4000/vega/`](http://127.0.0.1:4000/vega/) to see the website.

构建Vega并查看示例：

- 克隆Vega库。
- 执行`yarn`安装依赖。
- 执行`yarn build`(我本地报错，待验证)

☢️ 翻译补充：执行`yarn build`进行构建会报错，执行`npm run build`可以快速解决。

`docs`文件夹下包含站点和文档文件，如果想运行，在该目录下执行`bundle install`和`bundle exec jekyll serve`，然后访问[`http://127.0.0.1:4000/vega/`](http://127.0.0.1:4000/vega/)，即可查看站点。

☢️ 翻译补充：在执行`bundle install`之前，还需要安装一堆依赖，有点麻烦，可以直接略过。

## Contributions, Development, and Support

Interested in contributing to Vega? Please see our [contribution and development guidelines](CONTRIBUTING.md), subject to our [code of conduct](CODE_OF_CONDUCT.md).

Looking for support, or interested in sharing examples and tips? Post to the [Vega discussion forum]((https://groups.google.com/forum/#!forum/vega-js)) or join the [Vega slack organization](https://bit.ly/join-vega-slack)!

略