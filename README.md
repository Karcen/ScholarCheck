# ScholarCheck — Reference Verification Toolkit

[中文说明](README.zh-CN.md) · [English](#english)

## English

ScholarCheck brings two existing browser-based citation-checking tools into one GitHub Pages project. It keeps their original interfaces and verification logic intact, while adding a shared landing page, navigation, English/Chinese navigation copy, and a single deployment entry point.

This is a reference-screening aid, not a proof of publication authenticity. A result depends on the metadata indexed by Crossref and the matching heuristics in each tool. A failed match may reflect incomplete metadata, spelling differences, an unindexed work, or a network problem. Inspect DOI landing pages, publisher records, and the cited work before drawing conclusions.

### Included tools

**Citation Verifier** (`apps/citation/index.html`) accepts formatted and plain-language references, including numbered lists. It looks up DOIs when available, searches bibliographic text otherwise, groups results, and supports CSV, APA, Vancouver and BibTeX exports.

**BibTeX Reference Validator** (`apps/bibtex/index.html`) accepts pasted `.bib` entries, searches Crossref by title, shows candidate records, offers manual corrections and candidate adoption, and exports BibTeX, APA, Chicago, MLA, Harvard, RIS, JSON and CSV reports.

Both tools are the original HTML/CSS/JavaScript applications and keep their independent internal theme and export controls. The new shell uses tabs and isolated iframes to prevent JavaScript symbol and CSS conflicts; there is no shared state or automatic data transfer between the tools.

### Run locally

Open `index.html` in a current browser. For a local HTTP environment, run:

```sh
python3 -m http.server 8000
```

Then visit `http://localhost:8000/`. The shell requires no build step, package manager, login, or API key. Network access is required for Crossref lookups; Google Fonts may also load over the network.

### Publish with GitHub Pages

Upload the contents of this package to a new GitHub repository. In Settings → Pages, choose **Deploy from a branch**, select the main branch and `/ (root)`, and save. GitHub Pages will serve `index.html` as the home page. `.nojekyll` prevents unnecessary Jekyll processing. Alternatively, deploy the folder to any static host.

Navigation hashes `#citation` and `#bibtex` open the corresponding tabs. Both source tools can also be accessed directly at their respective `apps/.../index.html` paths.

### Project layout

```text
ScholarCheck/
├── index.html                # Unified home page, language and tool navigation
├── apps/
│   ├── citation/index.html   # Original formatted-reference verifier
│   └── bibtex/index.html     # Original BibTeX validator
├── README.md                 # English documentation
├── README.zh-CN.md           # Chinese documentation
└── .nojekyll                 # Disable Jekyll for GitHub Pages
```

### Privacy and limitations

Reference text or titles used in queries are sent directly from your browser to the public Crossref REST API (`https://api.crossref.org`). The shell has no backend and does not upload a document to a server controlled by this project. Both original tools store their theme preferences locally. Do not enter unpublished or confidential references if their titles must not be disclosed to Crossref. Network failure, rate limits, sparse metadata, and title similarity can affect results. “Found” does not independently establish a paper's scientific reliability, and “Not Found” is not evidence of fabrication.

### Source provenance

- [Citation Verifier](https://github.com/Karcen/is-this-paper-real.gitub.io) — `main/index.html`, retrieved 2026-11-03.
- [BibTeX Reference Validator](https://github.com/Karcen/bibtex-crossref-validator-online.github.io) — `main/index.html`, retrieved 2026-11-03.

The two original single-file applications are preserved without code changes in their respective `apps` directories. No third-party skills or build dependencies are bundled. The original repositories do not include standalone LICENSE files; do not infer an MIT license from README wording alone. Obtain an explicit license before redistributing code outside your own repositories.

### Author

Karcen Zheng · [Website](https://karcen.github.io/zhengjiacheng.github.io/)

Chinese documentation: [README.zh-CN.md](README.zh-CN.md).
