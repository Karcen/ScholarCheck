# ScholarCheck — 学术参考文献核验工具箱

[English README](README.md)

ScholarCheck 将两个已有的浏览器端参考文献核验工具整合到同一个 GitHub Pages 项目。新入口提供工具切换、中英文导航和统一部署路径；两套原有的核验算法、交互界面和导出功能保持不变。

本项目用于辅助筛查引用信息，不是判断论文真伪的最终依据。Crossref 未返回匹配结果，可能是因为文献未被收录、元数据缺失、标题拼写有差异或网络请求失败。需要结合 DOI 落地页、出版机构网站及原文进一步核实。

## 功能

普通参考文献核验（`apps/citation/index.html`）：粘贴 APA、MLA、Chicago、Vancouver 或普通文本引用，支持编号列表；优先进行 DOI 查询，再进行书目信息检索；按核验状态分组，并可导出 CSV、APA、Vancouver、BibTeX 等格式。

BibTeX 条目核验（`apps/bibtex/index.html`）：粘贴 `.bib` 内容，通过标题在 Crossref 搜索候选文献；查看相似度和候选记录，可采用候选元数据或手动修改；支持导出 BibTeX、APA、Chicago、MLA、Harvard、RIS、JSON 及 CSV 报告。

两个原始应用分别运行在独立 iframe 中，避免 CSS 样式和 JavaScript 全局函数冲突。切换工具不会自动把输入数据或核验结果传给另一工具。原工具内部的主题切换和结果导出仍可使用。

## 本地运行

直接使用现代浏览器打开项目根目录的 `index.html`。也可在项目根目录执行：

```sh
python3 -m http.server 8000
```

然后访问 `http://localhost:8000/`。无需安装前端依赖，也不需要 API 密钥。实际查询 Crossref 时需要网络连接。

## 部署到 GitHub Pages

将压缩包中的项目文件上传至一个新的 GitHub 仓库。在 Settings → Pages 中，将发布方式设为 Deploy from a branch，选择 `main` 分支和 `/ (root)` 目录后保存。根目录 `index.html` 即为统一入口。

访问地址添加 `#citation` 可进入普通参考文献核验；添加 `#bibtex` 可进入 BibTeX 核验。也可以使用 `apps/citation/index.html` 和 `apps/bibtex/index.html` 直接进入独立工具。

## 项目结构

```text
ScholarCheck/
├── index.html                # 统一入口、双语导航和工具切换
├── apps/
│   ├── citation/index.html   # 原普通参考文献核验工具
│   └── bibtex/index.html     # 原 BibTeX 核验工具
├── README.md                 # 英文说明
├── README.zh-CN.md           # 中文说明
└── .nojekyll                 # 关闭 GitHub Pages 的 Jekyll 处理
```

## 数据隐私与局限

浏览器会向 Crossref 公共 API（`https://api.crossref.org`）发送用于检索的参考文献信息或标题。此项目不运行独立后端，也不由项目服务器接收上传文件。两份原始应用会在浏览器本地保存主题偏好。如果未公开论文的标题、研究内容需要保密，不应直接提交到公共检索接口。

核验结果受数据库覆盖范围、相似度阈值、元数据质量和接口可用性影响。显示“存在”并不代表论文可靠；显示“未找到”也不能据此认定为虚构。

## 来源与许可说明

原项目：[Citation Verifier](https://github.com/Karcen/is-this-paper-real.gitub.io) 与 [BibTeX Reference Validator](https://github.com/Karcen/bibtex-crossref-validator-online.github.io)。本次使用 2026 年 11 月 3 日取得的 `main` 分支 `index.html` 文件，原样放入 `apps/` 对应目录。

两个原仓库均未提供单独的 LICENSE 文件，因此不能仅凭 README 中提到 MIT 或开放使用的文字认定其已有明确的代码许可证。向其他主体重新分发前，请确认许可条件。

作者：Karcen Zheng · [个人主页](https://karcen.github.io/zhengjiacheng.github.io/)
