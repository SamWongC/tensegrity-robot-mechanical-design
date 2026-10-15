# Upload to GitHub

Create an empty repository named `tensegrity-robot-mechanical-design` under `SamWongC`. Start with Private. Do not initialize a README, license or .gitignore on GitHub.

Open PowerShell. Keep Clash running on the previously used local HTTP proxy port 7897. Run the commands below in order; stop if any command fails. Initialize Git LFS before adding files. The first upload may take longer because this archive contains hundreds of megabytes of CAD assets. LFS storage and download quotas apply to the account; see [GitHub billing documentation](https://docs.github.com/en/billing/concepts/product-billing/git-lfs).

---

# 上传步骤

在 GitHub 创建空仓库 `tensegrity-robot-mechanical-design`，Owner 选 `SamWongC`，建议 Private，不勾选 README、许可证和 .gitignore。

保持 Clash 开启且 HTTP 代理端口为 7897，在 PowerShell 逐段执行。遇到错误先停止，不要继续。先启用 Git LFS 再添加文件，避免把 CAD 大文件提交到普通 Git 历史。

```powershell
$env:Path = "C:\Users\1oofey\.cache\codex-runtimes\codex-primary-runtime\dependencies\native\git\cmd;$env:Path"
cd "D:\codex_workspace\Gitlab\tensegrity-robot-mechanical-design"
git --version
git lfs version
git init -b main
git lfs install --local
git config user.name "SamWongC"
git config user.email "wanglufei@yeah.net"
git add -A
git --no-pager diff --cached --stat
git lfs ls-files
```

Confirm that `git lfs ls-files` lists CAD and 3MF files before committing.

确认 LFS 清单包含 CAD 及 3MF 文件，然后提交和推送：

```powershell
git commit -m "Add tensegrity robot mechanical design archive"
git remote add origin "https://github.com/SamWongC/tensegrity-robot-mechanical-design.git"
git -c http.proxy=http://127.0.0.1:7897 push -u origin main
```

After a successful push, confirm the README, source folders and LFS upload status on GitHub. For a future clone, install Git LFS and run `git lfs pull` inside the cloned repository. Do not assume a ZIP download contains the actual LFS files.

推送成功后检查 GitHub 中的 README、材料目录及 LFS 上传状态。以后克隆到其他电脑，先安装 Git LFS，再在克隆目录执行 `git lfs pull`，不要默认网页 ZIP 下载含实际大文件。首次上传需传输较多 CAD 数据，耗时通常长于之前的文档项目。
