# 启明云端文档

## 如何部署

1. 安装 python,推荐版本 python3.8.
2. 安装 teedoc

```shell
pip install teedoc
```

3. 安装插件

```shell
teedoc install
```

4. 编译出 html

```shell
teedoc build
```

5. 编译结果在`out`文件夹中

## 如何在首页中添加新的产品页

我们将首页中的页面结构样式与数据进行解耦，让后续的添加可以不用考虑页面结构样式的问题

### 文件位置

- 页面结构样式路径：`./layout/home.html`
- 页面样式路径：`./layout/style.html`
- 页面数据路径：`./static/data/home.json`
- 页面静态资源路径：`./static/home`

### 如何添加新的横幅内容

`./static/data/home.json` 下的 banner 数组中添加一个形似如下结构的内容：

```json
{
  "title": "<标题名称>",
  "img": "<图片路径（大小必须为2560x1216）>",
  "btns": [
    { "label": "文档", "link": "<官网产品地址>" },
    { "label": "购买", "link": "<淘宝地址>" }
  ]
}
```

- title 为横幅的标题
- img 为图片路径，图片统一放在`./static/home`路径下，大小要求必须为 2560x1216
- 这里的 btns 表示按钮，其中 label 是它所展现的文字，link 为跳转的连接。可以接多个

### 如何添加新的卡片内容

`./static/data/home.json` 下的 cards 数组中添加一个形似如下结构的内容：

```json
{
  "title": "<产品名称>",
  "img": "<产品图片路径（长宽比为1:1）>",
  "description": "<产品简述>",
  "link": "<链接跳转到文档>",
  "linkText": "查看详情"
}
```

- title 为卡片的标题
- img 为产品的图片路径，图片统一放在`./static/home`路径下，长宽比要求为 1:1
- description 为产品的简要描述
- link 为跳转到的本地文档页面
- linkText 为跳转按钮文字，一般为`"查看详情"`

## 如何添加新的产品文档

产品文档采用的是 markdown 形式，后续编译后可以得到样式丰富的文档内容。不仅如此，teedoc 还支持 jupyter 语法和 html 语法书写，为后续的文档样式添加了更丰富的展现方式。具体语法参考：

- [markdown 语法](https://teedoc.github.io/get_started/zh/syntax/syntax_markdown.html)
- [jupyter 语法](https://teedoc.github.io/get_started/zh/syntax/syntax_jupyter.html)
- [HTML 语法](https://teedoc.github.io/get_started/zh/syntax/syntax_html.html)

### 文件位置

- 中文文档位置：`./docs/docs/zh`
- 英文文档位置：`./docs/docs/en`
- 文档资源位置：`./docs/docs/assets`

### 如何添加新的产品文档

1. 在中文文档位置、英文文档位置和文档资源位置下添加自己的产品目录
2. `docs/docs/zh/sidebar.yaml`和`docs/docs/en/sidebar.yaml`生成了侧边栏目录结构。在两个 yaml 文件中添加自己的目录。比如：
   ```yaml
   - label: <产品名称>
     items:
       - label: 开发板功能介绍
         file: <产品文件夹>/board_features.md
       - label: 开发板相关资料
         file: <产品文件夹>/board_resources.md
       - label: 入门指南
         items:
           - label: 新手指南
             file: <产品文件夹>/getting_started.md
           - label: <文档名称>
             file: <产品文件夹>/<文档名称>.md
   ```
   > 注意：保持中英文的文件名称相同，方便后续维护
   > 其中，《开发板功能介绍》、《开发板相关资料》和《新手指南》三者必备。其它的文档则归到入门指南下面独立文档。这三份文档的规范后续会介绍。
3. 添加自己的中英文文档

## 文档规范

### 通用文档规范

1. 文档开头需要写文档头，文档头模板如下：

   ```yaml
   ---
   title: <文档标题>
   tags: <文档标签>
   keywords: <文档关键字>
   update:
     - date: <更新时间>
       author: <文档作者>
       version: <文档版本>
       content: <更新内容>
     - date: <更新时间>
       author: <文档作者>
       version: <文档版本>
       content: <更新内容>
   ---
   ```

   - 文档标题：整篇文章的标题会以一级标题的形式显示
   - 文档标签：方便用户站内搜索
   - 文档关键字：用于 SEO 优化
   - 更新时间：更新文档的时间
   - 文档作者：更新文档的人
   - 文档版本：版本为三段式，小幅度修改动最后一个版本，大幅度修改动第二个版本，整体升级动第一个版本
   - 更新内容：简要概括更新的内容

2. 由于整篇文章标题占用了一级标题，所以文档内容从二级标题开始

### board_features.md 文档模板

```markdown
省略头部分内容

## 简介

<简介正文>

---

### 🔧 核心硬件配置

<核心硬件配置介绍>

---

### 🛠️ 设计特点

<设计特点介绍>

---

### 📡 主要应用场景

<主要应用场景介绍>

---

### ⚙️ 开发优势

<开发优势介绍>

---

## 引脚描述

<引脚介绍>

---

## 电源特性

<供电介绍>

```
- 简介正文：一段话介绍产品
- 核心硬件配置介绍：用无序列表介绍硬件上特点
- 设计特点介绍：用有序列表介绍设计特点
- 主要应用场景介绍：无序列表介绍应用场景
- 开发优势介绍：无序列表介绍开发板和其它产品对比优势
- 引脚介绍：用表格介绍引脚功能
- 供电介绍：介绍供电方式

### board_resources.md 文档模板

```markdown
省略头部分内容

## <产品名称> 原理图

<iframe src="/docs/assets/<资源路径>#toolbar=0&navpanes=0" width="100%" height="1000px" style="border:none;"></iframe>

[📥 下载 PDF](/docs/assets/<资源路径>)
```

- PDF文档：PDF类型文档可以通过 iframe 的HTML标签进行预览，效果会更好。下方添加超链接方便下载。
- 普通资源：通过添加超链接的形式方便下载


### getting_started.md 文档内容

1. 提供固件烧录教程
2. 简要说明如何编译例程
