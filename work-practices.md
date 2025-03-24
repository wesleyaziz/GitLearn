# 工作實務

## 1. 提交規範

### 提交信息格式化

```bash
<type>(<scope>): <subject>

<body>
<footer>
```

- type: feat(新功能), fix(修復), docs(文檔), style(格式), refactor(重構), test(測試), chore(建構)
- scope: 影響範圍
- subject: 簡短描述
- body: 詳細描述
- footer: 關閉 issue 等

## 2. 日常工作流程

### 開始新任務前

- 確保本地 develop 分支同步最新代碼
- 從 develop 創建新的功能分支
- 遵循分支命名規範

### 開發過程中

- 經常性小批量提交
- 定期與 develop 分支同步
- 保持提交信息清晰

### 完成功能後

- 進行代碼自測
- 整理提交歷史（如需要）
- 提交 Pull Request/Merge Request

## 3. Code Review 規範

### 檢查項目

- 代碼邏輯
- 命名規範
- 性能影響
- 安全隱患
- 測試覆蓋

### Review 流程

- 提供清晰的變更說明
- 及時回應評審意見
- 修改後重新提交

## 4. 版本發布流程

### 準備階段

- 確認所有功能已完成
- 進行完整測試
- 更新版本號和更新日誌

### 發布階段

- 創建 release 分支
- 進行最後測試和修復
- 合併到 master/main
- 打標籤發布

### 發布後

- 部署監控
- 準備回滾方案
- 同步回 develop 分支
