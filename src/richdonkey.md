# Show me a rich donkey lol

> 2025-03-20


```admonish note
人不是对过去发生的事情进行原始的、客观的回忆，而是容易犯错误。  
简而言之，我们根本记不起来自己犯过哪些错，给自己带来多严重的影响，以及犯错的频率是多少。
```

## 因此需要自检清单

```admonish note
记录自己的时间和精力构成。两者都是消耗品。  I
花在哪里了，简单做个记录，哪些可以改善。  
```

## 产出如下改善感知( Self-awareness of Improvement )

### 一、 电子化且多终端同步笔记记录
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

### 二、 搜索整理的电子笔记
> Powershell安装ripgrep文本搜索工具

#### 1. 设置PowerShell的输出编码为UTF-8

```powershell
$OutputEncoding = [System.Text.Encoding]::UTF8
chcp 65001  # 将控制台代码页设置为 UTF-8
```

#### 2. 配置Vim的编码设置

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
