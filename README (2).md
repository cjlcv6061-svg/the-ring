# 奇環／THE RING — 線上閱讀器 + 編輯器

這個資料夾有三個檔案，全部要放進同一個 GitHub repo 的根目錄：

```
index.html      ← 給訪客看的閱讀器（靜態頁面）
edit.html        ← 給你自己用的編輯介面
episodes.json   ← 七集的內容資料（index.html 和 edit.html 都讀這個檔）
```

---

## 第一步：建立 GitHub repo 並上傳檔案

1. 登入 GitHub，右上角「+」→「New repository」
2. 取個名字，例如 `qihuan-site`，設為 **Public**（GitHub Pages 免費方案需要 Public repo），按「Create repository」
3. 進入新 repo 頁面，點「uploading an existing file」（或用網頁版的 Add file → Upload files）
4. 把這三個檔案（`index.html`、`edit.html`、`episodes.json`）一次拖進去，按「Commit changes」

---

## 第二步：開啟 GitHub Pages

1. 在 repo 頁面點上方的「Settings」
2. 左側選單找「Pages」
3. 「Source」選 **Deploy from a branch**
4. Branch 選 **main**，資料夾選 **/ (root)**，按「Save」
5. 等個 1～2 分鐘，頁面會顯示一個網址，格式類似：
   `https://你的帳號.github.io/qihuan-site/`

打開這個網址就是訪客看到的閱讀器（`index.html`）。

---

## 第三步：申請 GitHub Token（給編輯器用）

1. GitHub 右上角頭像 → Settings → 左側最下面「Developer settings」
2. 「Personal access tokens」→「Fine-grained tokens」→「Generate new token」
3. 設定：
   - Token name：隨便取，例如 `qihuan-editor`
   - Expiration：建議選 90 天或自訂（到期要重新申請）
   - Repository access：選「Only select repositories」，勾選你剛建立的那個 repo
   - Permissions → Repository permissions → 找到 **Contents**，設為 **Read and write**
4. 按「Generate token」，**立刻複製存好**（GitHub 只會顯示這一次，關掉頁面就看不到了）

---

## 第四步：使用編輯器

1. 打開 `https://你的帳號.github.io/qihuan-site/edit.html`
2. 填入：
   - **GitHub repo**：`你的帳號/qihuan-site`
   - **分支**：`main`
   - **Token**：貼上剛才複製的字串
3. 按「連接並載入內容」
4. 上方選單選你要編輯的集數，下面文字框直接改
5. 改完按「存檔並推送到 GitHub」
6. 等 30 秒到 1 分鐘，GitHub Pages 會自動重新部署，回到 `index.html` 重新整理就會看到新內容

> Token 只存在你目前這台瀏覽器（localStorage），下次打開 `edit.html` 會自動帶入，不用每次重填。要清除就按「清除已存的 Token」。

---

## 文字框編輯規則

- **一般段落**：一行打完按 Enter 換下一段，每一行就是一個段落
- **場景分隔線**：單獨一行打三個減號 `---`
- **粗體**：用兩個星號包住文字，例如 `**這是重點**`

---

## 新增 / 刪除 / 調整集數順序

連接成功後，下拉選單旁邊有幾個按鈕：

- **＋ 新增一集**：在列表最後加一筆空白集數，標籤會自動編號（第八集、第九集…），名稱先填「未命名」，自己再改
- **↑ / ↓**：把目前選到的這一集往前或往後移一位（調整在 `index.html` 導覽列上的顯示順序）
- **刪除**：把目前選到的這一集從列表移除

這幾個操作都只是**先改本機的暫存資料**，畫面上會看到變化，但實際的 GitHub repo 還沒有變更 —— 一定要按「存檔並推送到 GitHub」，這些更動才會真的生效並反映到網站上。如果中途想反悔，重新整理頁面（不要按存檔）就能恢復成 repo 上原本的狀態。

---

## 注意事項

- 這個編輯器是「方案 A」：純前端直接呼叫 GitHub API 存檔，**沒有後端伺服器、沒有帳號系統**，任何人只要拿到你的 Token 就能用你的身份改 repo 內容，所以 Token 不要分享給別人，也不要貼在公開的地方
- `edit.html` 本身雖然也會被 GitHub Pages 公開（網址任何人都打得開），但沒有你的 Token 就無法存檔，頂多只能看到空白的登入畫面
- 如果想徹底避免 `edit.html` 被陌生人看到，可以把它放進 repo 但**不要連結在 index.html 裡**，只有你自己知道網址
