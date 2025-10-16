# YayuWiki

[![Deploy MkDocs](https://github.com/duya25446/YayuWiKi/actions/workflows/deploy.yml/badge.svg)](https://github.com/duya25446/YayuWiKi/actions/workflows/deploy.yml)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

企业产品知识库和技术文档中心，基于 MkDocs Material 主题构建，支持中英文双语。

🌐 **在线访问**: [https://duya25446.github.io/YayuWiKi/](https://duya25446.github.io/YayuWiKi/)

## 📖 项目简介

YayuWiki 是一个现代化的企业产品文档中心，提供：

- 📚 **全面的产品文档** - 详细的功能说明和使用指南
- 🔧 **完整的 API 文档** - RESTful API 接口文档和代码示例
- 🌍 **双语支持** - 中英文文档完整覆盖
- 🎨 **现代化界面** - 基于 Material for MkDocs 的精美主题
- 🔍 **强大的搜索** - 支持中英文全文搜索
- 📱 **响应式设计** - 完美适配各种设备

## 🚀 快速开始

### 本地开发

1. **克隆仓库**

```bash
git clone https://github.com/duya25446/YayuWiKi.git
cd YayuWiKi
```

2. **安装依赖**

```bash
pip install -r requirements.txt
```

3. **启动开发服务器**

```bash
mkdocs serve
```

4. **访问文档**

在浏览器中打开 [http://127.0.0.1:8000](http://127.0.0.1:8000)

### 构建静态文件

```bash
mkdocs build
```

生成的静态文件将位于 `site/` 目录。

## 📁 项目结构

```
YayuWiKi/
├── docs/                    # 文档源文件
│   ├── index.md            # 中文主页
│   ├── getting-started/    # 快速开始
│   ├── products/           # 产品文档
│   ├── api/                # API 文档
│   ├── en/                 # 英文文档
│   │   ├── index.md        # 英文主页
│   │   ├── getting-started/
│   │   ├── products/
│   │   └── api/
│   └── assets/             # 静态资源
│       ├── images/         # 图片
│       └── stylesheets/    # 自定义样式
├── .github/
│   └── workflows/
│       └── deploy.yml      # GitHub Actions 部署配置
├── mkdocs.yml              # MkDocs 配置文件
├── requirements.txt        # Python 依赖
└── README.md               # 项目说明
```

## 📝 文档编写指南

### 添加新页面

1. 在 `docs/` 目录下创建 Markdown 文件
2. 在 `mkdocs.yml` 的 `nav` 部分添加导航条目
3. 如需双语支持，在 `docs/en/` 下创建对应的英文版本

### Markdown 扩展

文档支持以下 Markdown 扩展：

- **代码高亮** - 支持多种编程语言
- **代码标签页** - 使用 `===` 创建标签页
- **提示框** - 使用 `!!!` 创建不同类型的提示框
- **表格** - 标准 Markdown 表格
- **Mermaid 图表** - 支持流程图、时序图等
- **数学公式** - 支持 LaTeX 数学公式

### 代码示例

````markdown
=== "Python"

    ```python
    def hello_world():
        print("Hello, World!")
    ```

=== "JavaScript"

    ```javascript
    function helloWorld() {
        console.log("Hello, World!");
    }
    ```
````

### 提示框

```markdown
!!! note "注意"
    这是一个注意提示框

!!! tip "技巧"
    这是一个技巧提示框

!!! warning "警告"
    这是一个警告提示框

!!! danger "危险"
    这是一个危险提示框
```

## 🔄 自动部署

项目配置了 GitHub Actions 自动部署：

1. **触发条件**：
   - 推送到 `main` 分支
   - 创建 Pull Request 到 `main` 分支
   - 手动触发工作流

2. **部署流程**：
   - 检出代码
   - 安装 Python 和依赖
   - 构建 MkDocs 站点
   - 部署到 GitHub Pages（`gh-pages` 分支）

3. **GitHub Pages 设置**：
   - 进入仓库 Settings → Pages
   - Source 选择 `gh-pages` 分支
   - 保存后即可通过 GitHub Pages 访问

## 🛠️ 技术栈

- **文档生成器**: [MkDocs](https://www.mkdocs.org/) 1.5+
- **主题**: [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 9.5+
- **Markdown 扩展**: [PyMdown Extensions](https://facelessuser.github.io/pymdown-extensions/)
- **CI/CD**: GitHub Actions
- **托管**: GitHub Pages

## 🎨 主题定制

### 修改颜色方案

在 `mkdocs.yml` 中修改：

```yaml
theme:
  palette:
    - scheme: default
      primary: indigo  # 主色调
      accent: indigo   # 强调色
```

### 添加自定义样式

1. 在 `docs/assets/stylesheets/` 创建 CSS 文件
2. 在 `mkdocs.yml` 中引入：

```yaml
extra_css:
  - assets/stylesheets/custom.css
```

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📞 联系方式

- **GitHub Issues**: [提交问题](https://github.com/duya25446/YayuWiKi/issues)
- **Email**: support@yourcompany.com

## 🙏 致谢

- [MkDocs](https://www.mkdocs.org/) - 优秀的静态文档生成器
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) - 精美的 Material Design 主题
- [GitHub Pages](https://pages.github.com/) - 免费的静态网站托管服务

---

⭐ 如果这个项目对您有帮助，请给我们一个 Star！
