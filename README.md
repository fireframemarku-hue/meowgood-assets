# meowgood-assets

喵谷（Meowgood）社群發佈用的**公開圖床**。存在的唯一理由：Instagram 與 Threads 的發文 API 沒有圖片直傳，只收「公開 HTTPS 直連檔案」——Meta 伺服器會自己去 cURL 那個網址。本 repo 就是那個網址的來源。

品牌產出的 SSOT 在私有的 `OES` repo；本 repo **只放已經要對外發佈的成品圖**，是發佈管線的一站，不是素材庫。

## 三條紀律

1. **推上來的東西是永久公開的。** git 歷史不會因為刪檔而消失，事後把 repo 轉私有也救不回來（快取與 fork 已經散出去）。**只放已定稿、本來就要發到社群的圖**——未過稿的草圖、含浮水印的測試版、產製中間檔，一律不進來。
2. **機敏檔案零容忍。** `.env`、token、金鑰、憑證絕不進這個 repo。`.gitignore` 已擋掉常見型式，但擋不住改過名的東西——推之前自己看一眼 `git status`。
3. **圖先壓縮再推。** repo 只會長大、刪檔不會讓它變小。每天 300 KB、一年約 110 MB；之後要瘦身得改寫 git 歷史，很痛。

## 目錄與網址對應

檔案路徑直接對應 GitHub Pages 網址，不另做映射：

```
social/{營運主體}/{該主體的落點慣例}/{檔名}
```

| 營運主體 | 路徑慣例 | 對應 OES 的落點 |
|---|---|---|
| 喵曆 `meowlendar` | `social/meowlendar/{YYYY}/{MM}/{DD}/` | `brand/meowgood/apps/meowlendar/ops/{YYYY}/{MM}/{DD}/` |
| 阿灰的書店鋼琴 `classical-piano` | `social/classical-piano/ep{NN}/` | `brand/meowgood/animation/classical-piano/ep{NN}/` |
| 雪露的花店情歌 `female-vocal-songs` | `social/female-vocal-songs/ep{NN}/` | 影片庫 `brand/meowgood/animation/female-vocal-songs/ep{NN}/` |
| 栗子的澡堂靈魂樂 `male-vocal-songs` | `social/male-vocal-songs/ep{NN}/` | 影片庫 `brand/meowgood/animation/male-vocal-songs/ep{NN}/` |
| 喵谷の故事屋 `meowgood-story` | `social/meowgood-story/{line-slug}/ep{NN}/` | 影片庫 `brand/meowgood/animation/{line-slug}/ep{NN}/` |

上面三條線的來源在**影片庫**（私有 repo `amandachen0718/meowgoodstory`）、不在 OES，逐支兩張：`thumbnail-16x9.jpg`（1280×720，供 Threads）與 `thumbnail-1x1.jpg`（1080×1080 上下黑邊，供 IG）。檔名規格的 SSOT 為 OES 的品牌營運清冊 DOC-BD-004「跨營運主體共用資源」段。

路徑刻意鏡射 OES 的落點慣例，好讓「這張圖是哪一輪的」一眼看得出來、不必查表。

取用網址（GitHub Pages，`main` 分支根目錄）：

```
https://fireframemarku-hue.github.io/meowgood-assets/social/meowlendar/2026/08/07/example.jpg
```

## 誰在用

| 消費端 | 說明 |
|---|---|
| `OES/docs/ai/tools/instagram/ig_publish.py` | IG 圖文的 `image_url`；圖需為 **JPEG** |
| `OES/docs/ai/tools/threads/threads_publish.py` | Threads 圖片貼文的 `image_url`；圖需為 **JPEG** |

Meta 對格式的要求以各該工具的 `README.md` 為準，本檔不重抄。

## 為什麼不是 Azure Blob

評估過。Azure Blob 幾乎也是免費（每月 NT$0～3），但它的價值在「到期網址＋自動刪檔」——那是為了保護**不該長期公開**的東西而存在的機制。本 repo 放的圖本來就要公開發出去，用不到那套，卻要多養一個雲端資源與一組憑證。故不採用。
