# AGENTS.md

## Project overview
Static HTML/CSS/JS course portfolio for \"Advanced Web Design\" (225-). Main entry: index.html. Contains exercises (flexbox, iconfonts, SVG, JS basics/OOP/events) and a student grade dashboard task.

## Structure
- index.html - course index linking all exercises
- 1.html, 1.css - flexbox practice
- font/ - iconfont assets (local)
- svg005.html, css/svg005.css - SVG demo
- data.js - shared data for grade dashboard (window.STUDENTS, window.SUBJECTS)
- starter-level1.html - grade dashboard template (student to complete JS)
- starter-level1-0225-ZYT.html - target/complete version
- iconfont-*.html - iconfont/fontawesome/lucide demos and bottom navs
- function*.html, JS_boj_apply.html, dataType.html, text*.html - JS exercises
- cdn/ - local CDN assets
- zz_prompt.md - prompt history log

## Conventions (from zz_prompt.md)
- All CSS class names, id names, JS variables must start with zz_
- All prompts must be logged to zz_prompt.md before execution (append, include time/model/prompt)
- All new HTML files must be linked from index.html

## Running
Open HTML files directly in browser (no build step). Fonts/assets are local.

## Git
Remote: origin https://gitee.com/neusoft_wangyao_jsj/kkl.git (branch main). Follow skill web-project workflow: pull --rebase before push, don't commit .git, zz-master/, IDE dirs.
