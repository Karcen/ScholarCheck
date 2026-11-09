# ScholarCheck：参考文献核验工具

[English README](README.md)

ScholarCheck 将普通参考文献核验和 BibTeX 核验整合到一个 `index.html` 中。页面采用浅绿配色，支持暗色模式、手机屏幕和中英文导航。下载后即可打开，不需要安装前端依赖。

这是一套文献元数据核对工具。Crossref 匹配成功，不代表论文的研究结论可靠；没有匹配结果，也不能认定文献是伪造的。

## 功能

### 普通参考文献

支持粘贴 APA、MLA、Chicago、Vancouver、编号列表及普通文本引用。引用中包含 DOI 时，工具优先按 DOI 查询；否则使用参考文献文本检索 Crossref。

查询结果分为 Verified（已匹配）、Possibly Real（可能匹配）和 Not Found（未找到）。可以查看候选记录及书目信息，复制整理后的引文，或导出 CSV、APA、Vancouver、BibTeX 文件。

### BibTeX 条目

粘贴一个或多个 `.bib` 条目后，工具解析条目，通过标题检索 Crossref，计算候选文献的相似度，并展示匹配情况。可以查看候选记录、采用候选元数据，也可以手动修改条目。

支持导出 BibTeX、APA 7、Chicago、MLA 9、Harvard、RIS、JSON 和 CSV 报告。导出时可以选择包含全部条目，或只包含特定核验、修正状态的条目。

## 如何使用

1. 解压下载的文件。
2. 用现代浏览器打开 `index.html`。
3. 选择“普通参考文献”或“BibTeX 条目”，粘贴文本并启动核验。
4. 检查返回的 DOI、作者、题名、期刊和年份，再复制或导出结果。

页面不需要账号、API 密钥或构建工具。查询 Crossref 时需要联网。如果浏览器限制本地文件运行，可以在文件所在目录执行：

```sh
python3 -m http.server 8000
```

随后打开 `http://localhost:8000/`。

## 暗色模式与语言切换

右上角的主题按钮控制整页和两套内嵌工具的浅色、深色外观。首次打开时，页面跟随系统配色；手动切换后，选择会保存到浏览器的 `localStorage`（键名 `scholarcheck-theme`）。

语言按钮控制首页标题、导航与提示文字，支持英文和简体中文。两套原始工具的内部文字没有整体翻译：普通参考文献工具主要使用英文，BibTeX 工具同时包含中文和英文。语言偏好保存在 `scholarcheck-language`。

网址加上 `#citation` 可直接打开普通参考文献核验；加上 `#bibtex` 可打开 BibTeX 核验。切换标签时，两套工具分别保留各自的输入和结果，不会互相传输数据。标签支持左右方向键、Home 和 End 键操作。

## 为什么只需要一个 HTML

`index.html` 已包含入口页面、CSS 和两套核验工具的 JavaScript。原工具的文档以 UTF-8/Base64 形式内嵌，运行时分别放入 `srcdoc` iframe。这样既保留了两套工具各自的脚本和结果导出功能，也避免了样式及全局变量冲突。

核验和导出的原有逻辑没有改动；原工具的界面样式已统一调整，Google Fonts 网络字体依赖已删除，改用系统字体。实际部署不再需要 `apps/` 文件夹。

```text
ScholarCheck/
├── index.html       # 完整的单文件应用
├── README.md        # 英文说明
├── README.zh-CN.md  # 中文说明
├── LICENSE          # 原项目随附的许可证
└── .nojekyll        # GitHub Pages 配置
```

修改配色和首页文案可直接编辑 `index.html`。修改核验算法时，需要更新 HTML 中对应的 Base64 工具内容；建议先在下方原始项目中修改源码，再重新打包。

## 发布到 GitHub Pages

将 `ScholarCheck` 文件夹内的文件放在 GitHub 仓库根目录。在仓库的 Settings → Pages 页面选择 Deploy from a branch，指定部署分支和 `/ (root)`，保存后即可通过 GitHub Pages 访问。

也可以部署到其他静态网站托管服务。页面本身不依赖外部静态资源，但文献检索需要能够访问 Crossref。

## 数据与核验结果

项目没有自建后端。执行核验时，浏览器会直接向 `https://api.crossref.org` 发送用于检索的引文文本、文献标题或 DOI。Crossref 因此可能接收到尚未公开的研究题名等敏感信息；对于要求保密的内容，应先判断是否适合提交公共检索接口。

页面仅在浏览器本地保存主题和语言偏好，不把参考文献上传到本项目控制的服务器。导出文件由浏览器生成。

匹配结果受 Crossref 收录范围、元数据完整性、标题差异、相似度规则及网络状态影响。引用文献前，仍应查对 DOI 落地页、出版商记录及原文。匹配分数不能替代对论文质量的判断。

## 源码来源与许可

压缩包中两套工具的原始项目来源为：

- [Citation Verifier](https://github.com/Karcen/is-this-paper-real.gitub.io)
- [BibTeX Reference Validator](https://github.com/Karcen/bibtex-crossref-validator-online.github.io)

本次保留了用户提供项目中的 MIT `LICENSE`。但该文件本身不能证明两套上游工具分别拥有独立的 MIT 授权；如果要在其他仓库或平台公开再分发合并后的代码，应先确认上游许可条件。

作者：[Karcen Zheng](https://karcen.github.io/zhengjiacheng.github.io/)
