# Git 基礎操作

## 配置管理 (git config)

- `git config --list` : 查看所有配置信息
- `git config user.name` : 查看用戶名
- `git config user.email` : 查看用戶信箱
- `git config --global user.name "你的名字"` : 設置全局用戶名
- `git config --global user.email "你的信箱"` : 設置全局信箱

> 提示：
>
> - 使用 `q` 鍵退出配置信息查看界面
> - `--global` 參數表示全局設置，會影響所有倉庫
> - 省略 `--global` 則只影響當前倉庫
> - 設置保存在 `~/.gitconfig`（全局）或 `.git/config`（當前倉庫）

## 倉庫初始化 (git init)

- `git init` : 初始化 git
- `git init --bare` : 創建裸倉庫，通常用於服務器端

## 文件管理

### git add

- `git add <檔案名>` : 把檔案名加到暫存區
- `git add .` : 把未存到暫存區的檔案都加到暫存
- `git add -u` : 只加入已追蹤的文件

### git status

- `git status` : 查看當前狀態確定是否加入到了暫存區
- `git status -s` : 以簡潔方式顯示狀態

### git commit

- `git commit` : 把暫存區檔案推送到本地倉庫 repos
- `git commit -m '<訊息>'` : 寫入推送訊息
- `git commit -am '<訊息>'` : 跳過暫存區直接提交（僅對已追蹤文件有效）

## 日誌和版本控制

### git log

```bash
# 常用組合
git log --pretty=oneline --abbrev-commit

# 可用選項
--all            # 顯示所有分支
--pretty=oneline # 將提交信息顯示為一行
--abbrev-commit  # 使得輸出的 commitid 更簡短
--graph         # 以圖的形式顯示
-p              # 顯示每次提交的內容差異
```

### git reset

- `git reset --hard <commitID>` : 完全重置（危險操作，會丟失所有未提交的更改）
- `git reset --soft <commitID>` : 只重置 HEAD，保留暫存區和工作目錄的修改
- `git reset --mixed <commitID>` : （默認）重置 HEAD 和暫存區，保留工作目錄的修改

> 注意：
>
> - commitID 可以使用 git log 查看
> - 使用 HEAD^ 表示上一個版本，HEAD^^ 表示上上個版本

### git reflog

- `git reflog` : 查看所有操作歷史，包括已刪除的提交記錄

## 版本回退

### git reset vs git revert

兩者都可以用來撤銷更改，但使用方式和影響範圍不同：

#### git reset

- 直接移除指定的提交
- 會改變提交歷史
- 適用於尚未推送到遠程的提交
- 三種模式：
  - `--soft`: 只重置 HEAD
  - `--mixed`: 重置 HEAD 和暫存區（默認）
  - `--hard`: 重置 HEAD、暫存區和工作目錄

```bash
# 回到指定提交
git reset --hard <commitID>

# 回退一個版本
git reset --hard HEAD^
```

#### git revert

- 創建新的提交來撤銷之前的修改
- 不改變提交歷史
- 適用於已推送到遠程的提交
- 更安全的回退方式

```bash
# 撤銷指定的提交
git revert <commitID>

# 撤銷多個提交
git revert <commitID1>..<commitID2>

# 只撤銷但不自動提交
git revert -n <commitID>
```

### 使用場景比較

1. git reset 適用於：

   - 本地開發時的版本回退
   - 清理本地提交歷史
   - 需要完全移除某些提交時

2. git revert 適用於：
   - 已推送到遠程的提交回退
   - 團隊協作中的版本回退
   - 需要保留完整歷史記錄時

> 注意：
>
> - git reset 會改變提交歷史，不要用於已推送的提交
> - git revert 會產生新的提交，適合用於共享分支

## 忽略文件配置

### .gitignore

用於指定 Git 應該忽略的文件和目錄

```bash
# 忽略所有 .log 文件
*.log

# 忽略 node_modules 目錄
node_modules/

# 忽略特定文件
config.ini

# 忽略目錄下所有文件
build/

# 但不忽略特定文件
!build/important.txt
```

> 提示：如果文件已被追蹤，需要先取消追蹤：`git rm --cached <file>`

## 文件恢復

### git restore

- `git restore <文件名>` : 恢復文件修改
- `git restore --staged <文件名>` : 取消暫存

### git clean

- `git clean -n` : 預覽要刪除的文件
- `git clean -f` : 強制刪除未追蹤的文件
- `git clean -d` : 刪除未追蹤的目錄
- `git clean -x` : 刪除被忽略的文件

## 差異比較

### git diff

- `git diff` : 查看工作區與暫存區的差異
- `git diff --staged` : 查看暫存區與最後一次提交的差異
- `git diff <commit1> <commit2>` : 比較兩個提交之間的差異
- `git diff <branch1> <branch2>` : 比較兩個分支之間的差異

## 暫時存儲 (git stash)

### 基本用法

- `git stash` : 暫時存儲當前工作目錄的修改
- `git stash save "描述文字"` : 存儲時添加描述信息
- `git stash list` : 查看所有暫存的修改
- `git stash pop` : 恢復最近一次暫存的修改，並刪除該暫存
- `git stash apply` : 恢復最近一次暫存的修改，但保留暫存
- `git stash drop` : 刪除最近一次的暫存
- `git stash clear` : 清除所有暫存

### 進階操作

- `git stash show` : 查看最近一次暫存的內容
- `git stash show -p` : 查看最近一次暫存的詳細差異
- `git stash apply stash@{n}` : 恢復指定的暫存
- `git stash drop stash@{n}` : 刪除指定的暫存
- `git stash branch <分支名>` : 基於暫存創建新分支

### 使用場景

1. 需要臨時切換分支處理其他任務
2. 當前工作未完成但需要先提交其他修改
3. 想要在不同分支重用某些修改

> 提示：
>
> - stash 操作只會存儲已追蹤的文件修改
> - 使用 `git stash -u` 可以同時存儲未追蹤的文件
> - 使用 `git stash -a` 可以存儲所有文件（包括被忽略的文件）
