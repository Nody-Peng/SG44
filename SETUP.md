# 團隊成員設定指南

## 🚀 初次設定（第一次 Clone 專案）

### 1. Clone 專案

```bash
git clone https://github.com/your-username/SG44-wagtail.git
cd SG44-wagtail
```

### 2. 建立虛擬環境

```bash
# Windows
py -3.12 -m venv venv
venv\Scripts\activate

# Mac/Linux
python3.12 -m venv venv
source venv/bin/activate
```

### 3. 設定環境變數

```bash
# 複製環境變數範例檔案
copy .env.example .env

# 編輯 .env
notepad .env
```

**生成 SECRET_KEY：**

```bash
cd SG44
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"
```

複製輸出的字串，貼到 `.env` 的 `SECRET_KEY=` 後面。

### 4. 安裝依賴

```bash
cd SG44
pip install -r requirements.txt
```

### 5. 設定資料庫

```bash
# 執行資料庫遷移
python manage.py migrate

# 建立你的管理員帳號
python manage.py createsuperuser
```

### 6. 啟動開發伺服器

```bash
python manage.py runserver
```

訪問 http://localhost:8000/admin 測試登入

---

## 📅 每日開發流程

### 開始工作前

```bash
# 1. 啟動虛擬環境
cd D:\NCCU\SG44-wagtail
venv\Scripts\activate

# 2. 進入專案目錄
cd SG44

# 3. 更新 develop 分支
git checkout develop
git pull origin develop

# 4. 建立你的功能分支
git checkout -b feature/your-feature-name
# 例如：git checkout -b feature/news-page
```

### 開發中

```bash
# 隨時提交進度
git add .
git commit -m "Add: 描述你做了什麼"

# 例如：
# git commit -m "Add: news model and admin interface"
# git commit -m "Fix: submission form validation"
```

### 完成功能後

```bash
# 1. 確保所有變更都已提交
git status

# 2. 推送到遠端
git push origin feature/your-feature-name

# 3. 到 GitHub 建立 Pull Request
# - Base: develop
# - Compare: feature/your-feature-name
# - 請求團隊成員 Review
```

### 功能合併後

```bash
# 1. 切回 develop
git checkout develop

# 2. 更新本地 develop
git pull origin develop

# 3. 刪除已合併的功能分支
git branch -d feature/your-feature-name
```

---

## 🔧 常見操作

### 更新依賴套件

```bash
cd SG44
pip install -r requirements.txt
```

### 建立新的 App

```bash
cd SG44
python manage.py startapp app_name
```

記得在 `SG44/settings/base.py` 的 `INSTALLED_APPS` 加入新的 app

### 資料庫相關

```bash
# 建立 migration
python manage.py makemigrations

# 執行 migration
python manage.py migrate

# 查看 migration 狀態
python manage.py showmigrations

# 重置資料庫（小心使用！）
del db.sqlite3
python manage.py migrate
python manage.py createsuperuser
```

### 收集靜態檔案

```bash
python manage.py collectstatic
```

---

## ❗ 常見問題

### Q1: 虛擬環境啟動失敗

**Windows PowerShell 權限問題：**

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Q2: 遇到 Migration 衝突

```bash
# 1. 更新 develop
git checkout develop
git pull origin develop

# 2. 執行最新的 migrations
python manage.py migrate

# 3. 回到你的分支
git checkout feature/your-feature

# 4. Rebase（整合 develop 的變更）
git rebase develop

# 5. 如果有衝突，解決後繼續
git add .
git rebase --continue
```

### Q3: 忘記在哪個分支

```bash
# 查看當前分支
git branch

# 查看所有分支（包含遠端）
git branch -a
```

### Q4: 想放棄目前的變更

```bash
# 放棄所有未提交的變更（危險！）
git reset --hard HEAD

# 只放棄特定檔案的變更
git checkout -- filename.py
```

### Q5: 不小心在 develop 上開發了

```bash
# 1. 建立新分支（保留目前的變更）
git checkout -b feature/your-feature-name

# 2. 提交變更
git add .
git commit -m "Add: your changes"

# 3. 推送
git push origin feature/your-feature-name
```

### Q6: ImportError: cannot import name 'config' from 'decouple'

```bash
# 重新安裝 python-decouple
pip uninstall python-decouple
pip install python-decouple
```

### Q7: SECRET_KEY 錯誤

確認 `.env` 檔案存在且格式正確：

```env
SECRET_KEY=your-actual-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

---

## 📝 開發規範

### Commit 訊息格式

- `Add:` 新增功能
- `Fix:` 修復 Bug
- `Update:` 更新現有功能
- `Refactor:` 重構程式碼
- `Docs:` 更新文件
- `Style:` 程式碼格式調整
- `Test:` 新增或修改測試

**範例：**

```
Add: user submission form with file upload
Fix: email validation in submission model
Update: improve news page layout
Refactor: extract common template blocks
Docs: add API documentation
```

### 分支命名規範

- `feature/` - 新功能：`feature/submission-system`
- `fix/` - 修復：`fix/login-error`
- `hotfix/` - 緊急修復：`hotfix/security-patch`
- `refactor/` - 重構：`refactor/database-queries`

---

## 🆘 需要幫助？

- 查看 [README.md](README.md) 了解專案概述
- 遇到問題請在團隊群組詢問
- 或建立 GitHub Issue

---

**最後更新：2024-12-17**
