# ScholarCheck

[简体中文](README.zh-CN.md)

ScholarCheck checks formatted references and BibTeX entries against Crossref metadata. Both tools are included in one `index.html`, with a shared interface, light and dark themes, and a layout that works on desktop and mobile.

The checker helps identify records worth reviewing. It cannot determine whether a paper was published or whether its findings are reliable. A missing Crossref match may reflect incomplete indexing, a title variation, or a failed request.

## What's included

### Formatted citations

Paste APA, MLA, Chicago, Vancouver, numbered references, or plain bibliographic text. The tool queries a DOI directly when one is present; otherwise it searches Crossref using the reference text. It groups the responses into Verified, Possibly Real, and Not Found, and displays the matched metadata for inspection.

You can copy individual formatted references or export CSV, APA, Vancouver, and BibTeX outputs.

### BibTeX entries

Paste one or more `.bib` entries. The tool parses each entry, searches Crossref by title, scores candidate records, and displays the results. You can examine candidates, adopt a candidate's metadata, or edit an entry manually.

Exports include BibTeX, APA 7, Chicago, MLA 9, Harvard, RIS, JSON, and a CSV report. Export scope can be restricted by verification or correction status.

## Quick start

1. Download or extract the archive.
2. Open `index.html` in a current browser.
3. Choose **Formatted citations** or **BibTeX entries**, paste your input, and run the check.
4. Inspect the returned records before copying or exporting them.

The interface does not require installation, an account, an API key, or a build step. A network connection is required to query Crossref. If your browser restricts local file access, you can serve the folder over HTTP:

```sh
python3 -m http.server 8000
```

Open `http://localhost:8000/`.

## Themes, language, and navigation

The theme button switches between light and dark appearances across the main page and both embedded tools. The initial appearance follows your operating system unless you've chosen a theme manually. Manual preference is saved in browser `localStorage` under `scholarcheck-theme`.

The language button changes the outer page between English and Simplified Chinese. It does not translate the original applications' internal labels: the formatted-reference tool is primarily English, and the BibTeX tool uses a mix of Chinese and English. The page language is also saved locally under `scholarcheck-language`.

The tools are available at `#citation` and `#bibtex`. They keep their own inputs and results when you switch tabs, but do not transfer information to each other. The tab buttons support left/right arrow keys, Home, and End.

## Single-file design

`index.html` contains the interface, styles, and both original JavaScript applications. The tool documents are stored as UTF-8/Base64 strings inside the file; at runtime they load into separate `srcdoc` iframes. This prevents CSS and script-name conflicts without requesting `apps/citation/index.html` or `apps/bibtex/index.html` from a server.

The original checking and export logic has been retained. The embedded documents have been restyled to match the new design, and external Google Fonts imports were removed. System fonts are used instead.

Project files:

```text
ScholarCheck/
├── index.html       # Complete standalone application
├── README.md        # English instructions
├── README.zh-CN.md  # Chinese instructions
├── LICENSE          # License supplied with the project
└── .nojekyll        # GitHub Pages configuration
```

To change the theme or page copy, edit the host HTML/CSS in `index.html`. Changes to either verification engine require updating its embedded Base64 payload; the source applications linked below are easier to work on before rebundling.

## Deploy to GitHub Pages

Push the contents of the `ScholarCheck` folder to a repository root. Under **Settings → Pages**, choose **Deploy from a branch**, select your deployment branch and `/ (root)`, then save. GitHub Pages serves `index.html` automatically. Any static hosting service that serves HTML also works.

The page itself loads without external assets. Crossref lookups still require an internet connection.

## Privacy and result interpretation

The project has no custom backend. When you start a verification, the browser sends reference text, titles, or DOIs directly to the public Crossref REST API at `https://api.crossref.org`. These requests can reveal unpublished titles or other sensitive bibliographic information to Crossref. Do not submit confidential information unless you are comfortable with that disclosure.

Theme and language preferences are saved in the browser. The application does not save submitted references to project-controlled servers. Downloads are assembled in the browser.

A high similarity score is a matching signal, not evidence that a paper's methods or results are sound. Likewise, a “Not Found” result does not establish fabrication. Review the DOI landing page, publisher website, and source document where possible.

## Credits and licensing

The two verification engines derive from the user's supplied project, which cites these upstream sources:

- [Citation Verifier](https://github.com/Karcen/is-this-paper-real.gitub.io)
- [BibTeX Reference Validator](https://github.com/Karcen/bibtex-crossref-validator-online.github.io)

The interface uses a white-first light theme with an optional dark mode. The archive includes the original project's MIT `LICENSE`. That file does not by itself establish the license status of the independently developed upstream applications. Confirm their redistribution permissions if you plan to publish or redistribute the combined code beyond your own repositories.

Author: [Karcen Zheng](https://karcen.github.io/)
