# 補充工具和技巧

## 1. Git Bash 配置（Windows）

在用戶目錄創建 `.bash_profile`：

```bash
# Git 別名
alias gs='git status'
alias gl='git log --pretty=oneline --abbrev-commit'
alias ga='git add'
alias gc='git commit -m'
alias gp='git push'
alias gd='git diff'
alias gb='git branch'
alias gco='git checkout'
alias gsw='git switch'
```

應用配置：`source ~/.bash_profile`

## 2. Linux 常用命令

### 文件和目錄操作

#### 目錄導航

- `cd <目錄路徑>` : 切換目錄
  - `cd ..` : 返回上一級目錄
  - `cd ~` : 返回用戶主目錄
  - `cd -` : 返回上一次的目錄
- `pwd` : 顯示當前工作目錄的完整路徑

#### 文件操作

- `touch <文件名>` : 創建空文件或更新文件時間戳
- `rm <文件名>` : 刪除文件
- `cp <源文件> <目標文件>` : 複製文件
- `mv <源文件> <目標文件>` : 移動文件或重命名

### 文本編輯器 vi/vim

- 進入編輯器：`vi <文件名>`
- 模式切換：
  - `i` : 插入模式（編輯文本）
  - `esc` : 返回命令模式
- 常用命令（在命令模式下）：
  - `:w` : 保存文件
  - `:q` : 退出
  - `:wq` : 保存並退出
  - `:q!` : 強制退出不保存

## 3. Git Bash 中實用技巧

- 雙擊選中 commitID
- 滾輪點擊粘貼
- 使用方向鍵瀏覽命令歷史
- Tab 鍵自動補全
- Ctrl + R 搜索命令歷史
- `git help <命令>` 查看幫助文檔
