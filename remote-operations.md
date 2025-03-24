# 遠端倉庫操作

## 1. 基本配置

### SSH 金鑰配置

1. 生成 SSH 密鑰對

```bash
ssh-keygen -t rsa -C "your_email@example.com"
```

- `-t rsa`: 指定加密類型為 RSA
- `-C`: 添加註釋，通常使用郵箱
- 按 Enter 使用默認配置
- 可以設置密碼短語（passphrase）增加安全性

2. 查看公鑰內容

```bash
cat ~/.ssh/id_rsa.pub
```

- 公鑰文件：`~/.ssh/id_rsa.pub`
- 私鑰文件：`~/.ssh/id_rsa`（妥善保管，不要分享）

3. 添加到遠程平台

- GitHub: Settings > SSH and GPG keys > New SSH key
- GitLab: User Settings > SSH Keys
- 其他平台類似操作

4. 驗證配置

```bash
# GitHub
ssh -T git@github.com
# GitLab
ssh -T git@gitlab.com
```

### 遠程倉庫配置

1. 添加遠程倉庫

```bash
git remote add <簡稱> <倉庫地址>
# 例如
git remote add origin git@github.com:username/repo.git
```

2. 查看遠程倉庫

```bash
git remote -v  # 查看所有遠程倉庫
git remote show <簡稱>  # 查看特定遠程倉庫詳情
```

## 2. 遠程操作命令

### 推送和拉取

1. 推送到遠程

```bash
# 首次推送，設置上游分支
git push -u origin <分支名>

# 後續推送
git push

# 強制推送（謹慎使用）
git push -f
```

2. 從遠程拉取

```bash
# 只拉取不合併
git fetch [remote name][branch name]

# 拉取並合併
git pull [remote name][branch name]
```

### 分支管理

1. 遠程分支操作

```bash
# 查看遠程分支
git branch -r

# 刪除遠程分支
git push origin --delete <分支名>

# 跟蹤遠程分支
git checkout -b <本地分支> origin/<遠程分支>
```

2. 同步遠程更改

```bash
# 更新遠程分支信息
git fetch --prune

# 重置本地分支到遠程狀態
git reset --hard origin/<分支名>
```

## 3. 最佳實踐

1. 推送前檢查

- 確保本地代碼已完全提交
- 先拉取遠程更改避免衝突
- 在推送前進行測試

2. 安全建議

- 定期更換 SSH 密鑰
- 設置 SSH 密鑰密碼
- 不要在公共電腦保存憑證

3. 協作建議

- 經常與遠程倉庫同步
- 使用適當的分支策略
- 寫清晰的提交信息
