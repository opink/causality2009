# Show me a rich donkey lol

> 2025-03-20


```admonish note
人不是对过去发生的事情进行原始的、客观的回忆，而是容易犯错误。  
简而言之，我们根本记不起来自己犯过哪些错，给自己带来多严重的影响，以及犯错的频率是多少。
```

## 因此需要自检清单

```admonish note
记录自己的时间和精力构成。两者都是消耗品。  
花在哪里了，简单做个记录，哪些可以改善。  
```

## 产出如下改善感知( Self-awareness of Improvement )

### 0. 电子化且多终端同步笔记记录
> GitHub管理以md为基础的mdbook电子书项目  
> 使用mathjax插件写公式、exciladraw手绘示意图

```powershell
git clone https://github.com/opink/causality2009.git
cd causality2009

git status  # 查看当前状态

# 推送更新至远端仓库
git add .
git commit -m "add new content"
git push

# 同步远端版本
git fetch
git merge

git pull
```

### 1. 搜索整理的电子笔记
> Powershell安装ripgrep文本搜索工具

#### 1.1. 设置PowerShell的输出编码为UTF-8

```powershell
$OutputEncoding = [System.Text.Encoding]::UTF8
chcp 65001  # 将控制台代码页设置为 UTF-8
```

#### 1.2. 配置Vim的编码设置

在Pwsh中临时修复:
```powershell
rg 定理 | vim -c "set encoding=utf-8 fileencodings=utf-8" -
```
或永久配置（在 .vimrc 中添加）:
```vim
set encoding=utf-8
set fileencodings=utf-8
```

```powershell
rg 定理 | vim -
```

### 2. 终端分屏复用
#### 2.1. Windows Powershell :
   - `Shift + Alt` + `+` : 左右横向分屏2个窗口
   - `Shift + Alt` + `-` : 上下向分屏2个窗口
   - `Alt` + `方向键` : 切换窗口
   - `Alt + Shift` + `方向键` : 调整窗口大小
   - `Ctrl + Shift` + `w` : 关闭当前分屏窗口
  
#### 2.2. Linux Tmux :
- 默认 `Ctrl + b` 为 `triger`
- `Ctrl + b` + `?` : 显示所有快捷键帮助

#### Level1 会话(Session)操作
  - 新建会话 : `$ tmux new -s <session_name>`
  - 分离会话回到原shell : `Ctrl + b` + `d` (等同于`$ tmux detach`)
  - Tui模式列出所有会话level并可切换, q退出 : `Ctrl + b` + `s`
  - 切换会话 : `$ tmux switch -t <session_name>`
  - 从shell中进入会话 : `$ tmux attach -t <session_name>`
  - 杀死当前窗口(最终会话) : `Ctrl + d` (等同于`$ tmux kill-session -t <session_name>`)
  - 重命名会话 : `Ctrl +b` + `$` (等同于`$ tmux rename-session -t <old_name> <new_name>`)

#### Level2 窗口(Window)操作
  - 新建窗口 : `Ctrl + b` + `c`
  - 切换窗口 : `Ctrl + b` + `n` or `p`
  - 切换到指定窗口 : `Ctrl + b` + `0`~`9`
  - 切换窗口(需要输入index) : `Ctrl + b` + `'`
  - 关闭当前窗口 : `Ctrl + b` + `&`
  - 重命名窗口 : `Ctrl + b` + `,`
    
#### Level3 分面板(Pane)操作
  - 新建上/下分面板 : `Ctrl + b` + `"`
  - 新建左/右分面板 : `Ctrl + b` + `%`
  - 可视切换轮流分面板 : `Ctrl + b` + `o`
  - 显示分面板的编号来切换分面板 : `Ctrl + b` + `q`
  - 使用方向键来Jump分面板 : `Ctrl + b` + `方向键`
  - Tui模式列出所有窗口level并可切换, q退出 : `Ctrl + b` + `w`
  - 切换分面板布局 : `Ctrl + b` + `space`
  - 调整分面板大小 : `Ctrl + b + 方向键` 三者同时按
  - 分面板zoom到满屏/再按缩回 : `Ctrl + b` + `z`
  - 显示数字时钟, q退出 : `Ctrl + b` + `t`
  - 杀死当前分面板 : `Ctrl + b` + `x` / 确认 or `Ctrl + d` 直接杀

#### Level4 复制模式(Copy Mode)操作
- 先进入命令行模式  `Ctrl + b` + `:` 后输入 `setw -g mode-keys vi` 把默认的emacs模式改为vi模式
  - 进入文本复制模式 : `Ctrl + b` + `[`
  - 搜索文本 : `/` 后输入搜索内容
  - 复制模式下复制文本 : 使用vi命令，如 `y` 、`p` 等。
  - 退出复制模式后, 在需要粘贴的地方按 : `Ctrl + b` + `]`

### 3. Pro Git Book

#### [撤销操作 https://www.progit.cn/#_undoing](https://www.progit.cn/#_undoing)
有时候我们提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 --amend 选项的提交命令尝试重新提交：  
`git commit --amend` : 修改最后一次提交  
  
这个命令会将暂存区中的文件提交。 如果自上次提交以来你还未做任何修改（例如，在上次提交后马上执行了此命令），那么快照会保持不变，而你所修改的只是提交信息。

```bash
$ git commit -m 'initial commit'  
$ git add forgotten_file  
$ git commit --amend  
```