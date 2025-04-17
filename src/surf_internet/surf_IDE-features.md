# 码代码IDE真正需要的功能

## 1. Linux Shell 中：
### 1.1. IDE内分屏查询手册文档
- NeoVim
	1. 安装插件：
```vim
" 使用Telescope插件实现文档搜索
Plug 'nvim-telescope/telescope.nvim'
Plug 'nvim-lua/plenary.nvim'

" 或者使用专用man插件
Plug 'vim-utils/vim-man'
```
	2. 配置按键绑定：
```lua
-- 分屏查看man手册
vim.keymap.set('n', '<leader>Km', ':split | :term man <cword><CR>', {desc = "Split man page"})

-- 使用Telescope搜索man
vim.keymap.set('n', '<leader>M', function()
  require('telescope.builtin').man_pages({ sections = { "1", "2", "3" } })
end)
```

### 1.2. 在依赖源代码项中实现快速跳转、跳回
快速访问从crate导入的结构体或枚举上的可用方法，无需在IDE和docs.rs之间不断切换
- NeoVim
	1. 安装LSP：
	```bash
	npm install -g rust-analyzer
```
	2. 配置lua/lsp.lua：
	```lua
local opts = { noremap=true, silent=true }
vim.keymap.set('n', 'gd', '<cmd>lua vim.lsp.buf.definition()<CR>', opts)
vim.keymap.set('n', 'gD', '<cmd>lua vim.lsp.buf.declaration()<CR>', opts)
vim.keymap.set('n', 'gr', '<cmd>lua vim.lsp.buf.references()<CR>', opts)
vim.keymap.set('n', 'K', '<cmd>lua vim.lsp.buf.hover()<CR>', opts)
vim.keymap.set('n', '<leader>co', '<cmd>lua vim.lsp.buf.code_action()<CR>', opts)

-- 跳转历史管理
vim.keymap.set('n', '<C-o>', '<C-o>', { desc = "Jump back" })
vim.keymap.set('n', '<C-i>', '<C-i>', { desc = "Jump forward" })
```

- VScode
	- 安装rust-analyzer扩展
	- (可选的)配置keybindings.json：
```json
	{
  "key": "f12",
  "command": "editor.action.goToImplementation",
  "when": "editorHasImplementationProvider && editorTextFocus && !isInEmbeddedEditor"
},
{
  "key": "ctrl+shift+r",
  "command": "editor.action.goToReferences"
},
{
  "key": "alt+left",
  "command": "workbench.action.navigateBack"
}
```

- NeoVim
	- `gd` 跳转到定义
	- `Ctrl + o` 跳回
	- `Ctrl + i`  再跳入
- VScode
	- 使用Vim插件同上
## 1.3. 调出命令行执行编译、测试
`[norm]` - `:terminal` 命令打开终端

## 1.4. LSP提供函数说明

```
lsp查看函数文档快捷键为 K ，弹出的为hover

想翻页hover内容，向下翻是<C - f >   向上翻是 <C - b>。
```

```
<C-e> 还原到调用自动补全之前的状态，即退出补全模式。

<C-n> 和 <C-p> 分别用于选择下一个和上一个补全项。
<C-y> 确认使用当前选中的匹配项。
```

```
[norm]模式 <Alt-j> <Alt-k> 上 下 调整一行的位置
```