---
name: submit-project
description: Commit and push the current project to a remote Git repository (Gitee, GitHub, etc.). Handles git init, add, commit, remote setup, and push with personal access token authentication.
---

# Submit Project

Commit all current changes and push them to a remote Git repository.

## When to use this skill

When the user asks to "submit the project", "commit and push", "upload to Gitee/GitHub", or similar — meaning they want to take the entire working directory, snapshot it with git, and push it to a configured remote repository.

## Workflow

### 1. Safety checks before touching git

- **Sanitize credentials in prompt logs**: If the user gave you a personal access token or password and you also logged the prompt into a file (e.g., `zz_prompt.md`), **replace the token value with `***REDACTED***`** in the logged copy. The real token stays only in memory and is never written to any file that could be committed.
- **Create a `.gitignore`** if one does not exist. At minimum it must exclude:
  - `zz_prompt.md` (the prompt log file with tokens inside)
  - Any dev server scripts you created (e.g., `server.js`)
  - `node_modules/`, `.DS_Store`, editor configs, etc.

### 2. Initialize and stage

```powershell
# If .git does not exist yet:
git init
git branch -M main

# Stage everything that is not in .gitignore:
git add .

# Review what would be committed:
git status
git diff --cached --stat
```

Stop here and fix `.gitignore` if anything sensitive shows up.

### 3. Commit

Write a commit message that summarizes the actual work done, not just "update". Examples:

```powershell
git commit -m "feat: iconfont 底部导航标本 · iconfont-3 / iconfont-4

- 新增 iconfont-3.html: 字体图标方式，纸张明调 TAB STUDIO 主题
- 新增 iconfont-4.html: SVG Symbol 方式，暗夜暗调 DOCK ATELIER 主题
- 底部 tab bar 4 项：HOME / FAV(红点) / CART(徽章3) / ME
- index.html 课堂目录新增卡片 12、13"
```

### 4. Configure remote (Gitee example)

If the remote is not set up yet:

```powershell
git remote add origin https://gitee.com/<USER>/<REPO>.git
```

If it is already set up, verify it:

```powershell
git remote -v
```

### 5. Push with personal access token

Gitee and GitHub both accept the token as the password portion of the HTTPS URL. **Do NOT persist the token in `.git/config`**. The safe pattern:

1. Push with the token embedded — this does write to `.git/config` temporarily:
   ```powershell
   git push -u https://oauth2:<YOUR_TOKEN>@gitee.com/<USER>/<REPO>.git main
   ```
2. Immediately reset the remote URL to the clean, token-free version:
   ```powershell
   git remote set-url origin https://gitee.com/<USER>/<REPO>.git
   ```
3. Verify the token is gone:
   ```powershell
   git remote -v
   # Expected: origin  https://gitee.com/<USER>/<REPO>.git (fetch)
   #           origin  https://gitee.com/<USER>/<REPO>.git (push)
   ```

This keeps the token out of both `.git/config` and the shell history (as much as possible — PowerShell history still records the command, but `.git/config` is the durable risk).

### 6. Report

After a successful push, tell the user:
- How many files changed (`git diff --cached --stat` or `git log -1 --stat`)
- The remote URL
- The commit hash (`git log -1 --oneline`)
- Whether you had to sanitize any sensitive files out of the commit

## Known pitfalls

- **Windows line endings**: If git complains about `CRLF will be replaced by LF`, it is usually safe to proceed. Configure once with `git config --global core.autocrlf true` if it becomes noisy.
- **Large files**: If git rejects a file for being too big, do not force it. Add the file to `.gitignore` and explain to the user why (GitHub/Gitee limits: 100 MB normal, 2 GB LFS).
- **Remote already exists**: `git remote add` fails if `origin` is already set. Use `git remote set-url origin <url>` instead.
- **Token expired**: If push returns `401` or `Authentication failed`, the token may be expired or lack the `repo` scope. Ask the user to regenerate.
