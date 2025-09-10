# Wireless-Tag Documentation

## How to Deploy

1. Install Python, recommended version: Python 3.8.
2. Install teedoc:

```shell
pip install teedoc
```

3. Install plugins:

```shell
teedoc install
```

4. Build HTML:

```shell
teedoc build
```

5. The compiled result will be located in the `out` folder.

---

## How to Add a New Product Page on the Homepage

We decouple the page structure/style from the data on the homepage, so that future additions do not need to consider page layout issues.

### File Locations

- Page structure file: `./layout/home.html`
- Page style file: `./layout/style.html`
- Page data file: `./static/data/home.json`
- Page static resources: `./static/home`

### How to Add New Banner Content

Add a new entry under the `banner` array in `./static/data/home.json`, structured like this:

```json
{
  "title": "<Banner Title>",
  "img": "<Image Path (must be 2560x1216)>",
  "btns": [
    { "label": "Docs", "link": "<Official Product URL>" },
    { "label": "Buy", "link": "<Taobao URL>" }
  ]
}
```

- **title**: banner title
- **img**: image path (all images must be placed under `./static/home` and size must be 2560x1216)
- **btns**: buttons; `label` is the displayed text, `link` is the redirect URL. Multiple buttons are supported.

### How to Add New Card Content

Add a new entry under the `cards` array in `./static/data/home.json`, structured like this:

```json
{
  "title": "<Product Name>",
  "img": "<Product Image Path (aspect ratio 1:1)>",
  "description": "<Product Description>",
  "link": "<Link to Docs>",
  "linkText": "View Details"
}
```

- **title**: card title
- **img**: product image path (all images must be placed under `./static/home`, aspect ratio 1:1)
- **description**: brief product description
- **link**: link to the local documentation page
- **linkText**: button text, usually `"View Details"`

---

## How to Add New Product Documentation

Product documentation uses **Markdown** format. After compilation, the result will have rich styling. In addition, teedoc also supports **Jupyter** and **HTML** syntax, which allows more flexible documentation presentation. See syntax references:

- [Markdown Syntax](https://teedoc.github.io/get_started/zh/syntax/syntax_markdown.html)
- [Jupyter Syntax](https://teedoc.github.io/get_started/zh/syntax/syntax_jupyter.html)
- [HTML Syntax](https://teedoc.github.io/get_started/zh/syntax/syntax_html.html)

### File Locations

- Chinese docs: `./docs/docs/zh`
- English docs: `./docs/docs/en`
- Doc resources: `./docs/docs/assets`

### How to Add New Product Documentation

1. Add your own product directory under the Chinese docs, English docs, and assets directories.
2. Update `docs/docs/zh/sidebar.yaml` and `docs/docs/en/sidebar.yaml` to generate the sidebar structure. Example:
   ```yaml
   - label: <Product Name>
     items:
       - label: Board Features
         file: <product_folder>/board_features.md
       - label: Board Resources
         file: <product_folder>/board_resources.md
       - label: Getting Started
         items:
           - label: Beginner Guide
             file: <product_folder>/getting_started.md
           - label: <Doc Name>
             file: <product_folder>/<Doc Name>.md
   ```
   > Note: Keep file names consistent between Chinese and English versions for easier maintenance.  
   > The three required documents are **Board Features**, **Board Resources**, and **Beginner Guide**. Other docs should be placed under "Getting Started" as standalone items. The standards for these three documents will be introduced later.
3. Add your Chinese and English documentation files.

---

## Documentation Standards

### General Documentation Standards

1. Each document must start with a header. Template:

   ```yaml
   ---
   title: <Document Title>
   tags: <Document Tags>
   keywords: <Document Keywords>
   update:
     - date: <Update Date>
       author: <Author>
       version: <Version>
       content: <Update Content>
     - date: <Update Date>
       author: <Author>
       version: <Version>
       content: <Update Content>
   ---
   ```

   - **title**: the main title of the article (displayed as H1)
   - **tags**: used for internal site search
   - **keywords**: used for SEO optimization
   - **date**: when the document was updated
   - **author**: who updated the document
   - **version**: follows a three-level versioning scheme (minor changes → last number, major changes → middle number, full upgrade → first number)
   - **content**: a brief summary of the update

2. Since the document title already occupies the H1 level, content should start from H2 headings.
