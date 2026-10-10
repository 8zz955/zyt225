---
name: web-project
description: Use when working on the Web frontend project (225-朱禹同). Covers the site structure (HTML/SVG/CSS web pages, iconfont assets), how to preview pages locally, and how to commit and push changes to the gitee zz repository. Front-load keywords like "Web", "网页", "前端", "225-朱禹同".
---

# Web Project

This skill documents the `Web` front-end project for 225-朱禹同 (network design practice assignment).

## Project structure

```
Web/
├── 1.css           Stylesheet for 1.html
├── 1.html          First HTML page
├── index.html      Main entry page
├── svg005.html     SVG demo page
├── css/
│   └── svg005.css  Stylesheet for svg005.html
├── font/           iconfont assets (ICONFONT via iconfont.cn)
│   ├── iconfont.css / .js / .json
│   ├── iconfont.ttf / .woff / .woff2
│   └── demo.css / demo_index.html
└── .opencode/skills/web-project/   this skill
```

## Workflow

1. **Preview**: open `index.html`, `1.html`, or `svg005.html` in a browser for local preview. Fonts are bundled locally (no network needed).
2. **New pages**: follow the existing HTML/CSS style; use the iconfont classes from `font/iconfont.css` for icons.
3. **Commit & push** to the gitee repository `https://gitee.com/neusoft_wangyao_jsj/zz.git` under the `225-朱禹同/` folder:
   - Stage the changed files.
   - Commit with a concise Chinese message describing the change.
   - Pull first (`git pull --rebase`) so the remote history stays linear, then `git push`.

## Notes

- The `.git` directory and any nested `zz-master/` zip artifacts must not be committed.
- Render Chinese content with `charset="utf-8"`.