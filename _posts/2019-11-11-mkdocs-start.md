---
categories:
  - Tools
tags:
  - Mkdocs
---


  MkDocs 快速上手教學, 主要就是編輯 yml 檔案去更改 Theme 和 doc 語法

## Theme

安裝完後內建 [Read The Docs](https://github.com/rtfd/sphinx_rtd_theme) Theme最為普及, 其他 Theme 也可[參考這裡下載](https://github.com/mkdocs/mkdocs/wiki/MkDocs-Themes) ,

<span class="s1">更改使用的 Theme 於 mkdocs.yml 放入 `theme: readthedocs` 並 `mkdocs build` 即可完成, e.g.</span>

    site_name: My Docs
    theme: readthedocs

![](/assets/images/Screen-Shot-2019-01-15-at-9.52.47-PM-1024x563.png)  

## Popular Extension

### Install method:

    pip3 install Pygments pymdown-extensions

### 將以下模組放入 yml file:

    markdown_extensions:
      - codehilite
      - pymdownx.arithmatex
      - pymdownx.betterem:
          smart_enable: all
      - pymdownx.caret
      - pymdownx.critic
      - pymdownx.details
      - pymdownx.emoji:
          emoji_generator: !!python/name:pymdownx.emoji.to_svg
      - pymdownx.inlinehilite
      - pymdownx.magiclink
      - pymdownx.mark
      - pymdownx.smartsymbols
      - pymdownx.superfences
      - pymdownx.tasklist:
          custom_checkbox: true
      - pymdownx.tilde

### 個人常用:

#### <span class="s1">Pygments</span>

*   [CodeHilite](https://python-markdown.github.io/extensions/code_hilite/)

#### <span class="s1">pymdown-extensions</span>

[PyMdown Extensions](http://facelessuser.github.io/pymdown-extensions/) 集合了與許多重要且實用的功能, 強烈建議安裝.

*   Details[¶](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#details "Permanent link")

[Details](https://facelessuser.github.io/pymdown-extensions/extensions/details/) 提供縮合功能, 並可以支援不同顏色根據 e.g. `note`, `question`, `warning` etc.:

*   Mark[¶](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#mark "Permanent link")

[Mark](https://facelessuser.github.io/pymdown-extensions/extensions/mark/) 提供 <mark>highlight text</mark> like it was marked with a <mark>text marker</mark>. e.g. `==...==`.

*   SuperFences[¶](https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#superfences "Permanent link")

[SuperFences](https://facelessuser.github.io/pymdown-extensions/extensions/superfences/) 提供 code block 顯示正常於 Details 開合區塊內

### Not Support

1.  圖片大小, 但可以使用一般 html 語法完成
2.  超連結開啟分頁, 但可以使用一般 html 語法完成

### Reference:

*   https://squidfunk.github.io/mkdocs-material/extensions/pymdown/#details
