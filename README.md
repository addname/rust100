# Rust 100 问

这是一个使用 [MkDocs](https://www.mkdocs.org/) 和 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 构建的《Rust 100 问》学习指南项目。

本书旨在通过一系列精心设计的问答，帮助学习者系统地掌握 Rust 程序设计语言的核心概念。

## 本地开发

如果你想在本地运行、修改或构建这个网站，请遵循以下步骤：

1.  **克隆仓库**
    ```bash
    git clone https://github.com/addname/rust100.git
    cd rust100
    ```

2.  **安装依赖**
    推荐创建一个 Python 虚拟环境。本项目需要 `mkdocs` 和 `mkdocs-material` 主题。
    ```bash
    pip install mkdocs mkdocs-material
    ```

3.  **启动本地服务器**
    这个命令会启动一个本地开发服务器，当你修改文件时，网站会自动重新加载。
    ```bash
    mkdocs serve
    ```
    现在，你可以在浏览器中打开 `http://127.0.0.1:8000` 来查看网站。

4.  **构建静态网站**
    如果你想生成静态 HTML 文件，可以运行以下命令。生成的文件将位于 `site` 目录中。
    ```bash
    mkdocs build
    ```

## 贡献

欢迎对本书内容进行补充或修正。你可以通过提交 Pull Request 或创建 Issue 的方式来贡献。
