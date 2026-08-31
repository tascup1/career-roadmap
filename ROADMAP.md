# Career Roadmap — Frontend → Frontend/DevOps → Platform Engineer

> 建立日期:2026-08-31
> 目標:近期往「前端為主、DevOps 加分」的職缺移動,長期往「Platform Engineer / SRE」方向發展。
> 用法:每完成一項打勾 `- [x]`,並在對應章節下方補一行日期 + 心得/連結,當作學習紀錄。

## 現況盤點(2026-08-31)

已具備、面試可以直接講的實戰經驗:

- Vue 2 / Vue 3、Pinia 狀態管理
- Astro SSR/SPA 混合渲染(view-transition、persisted island、hydration mismatch 排錯)
- TypeScript(型別設計、enum、interface 拆分)
- Monorepo 工具鏈(pnpm workspace、共用 package 拆分)
- 金流 / 身分驗證前端實戰(KYC、OTP、deposit/withdrawal 流程)
- i18n、多租戶(tenancy)架構設計
- Kubernetes 部署觸發(既有 pipeline)、per-project pod 架構經驗
- Kong API gateway 使用經驗(path 分流)

---

## 🎯 整體優先順序建議(前端 + DevOps 合併排序)

> 你的定位是「近期前端為主、DevOps 加分」,所以排序邏輯是:**先補「面試必考、你本來會但生疏」的東西(投入小、回報快)**,**再補「完全不會的新技能」**,**最後才是需要長時間堆的 DevOps 深水區**。

| 順位 | 項目 | 為什麼排這裡 |
|---|---|---|
| 🔴 1 | Vue 底層原理 + 面試題庫 | 你天天在用,只是「講得出原理」跟「會用」是兩回事;複習成本最低、面試 CP 值最高 |
| 🔴 2 | JavaScript 底層原理(event loop / closure / prototype / this) | 跟 Vue 底層同一類「用不到但忘了會很尷尬」,而且是**所有前端面試的地基題**,沒特別列在你原本的訴求裡,但重要性不亞於 Vue 底層 |
| 🔴 3 | 瀏覽器 / 網路協議 | 你明確要的;這塊複習完可以跟 DevOps 的「網路 / gateway / TLS」知識串起來,一魚兩吃 |
| 🟡 4 | Testing(Vitest / Playwright) | 公司沒用過,完全空白,但幾乎所有中大型公司面試都會問「你們怎麼測試」——現在補這塊比臨場硬凹划算 |
| 🟡 5 | React 重新學 | 忘光了,重建成本最高,所以排在「複習類」後面;但補了能讓應徵的職缺池直接翻倍(很多公司 React-first) |
| 🟢 6 | DevOps 短期優先(K8s 手寫、CI/CD、容器化) | 你已經有 K8s 部署觸發 + Kong 的實戰經驗,這裡是「從會用到會設計」的深化,不是從零開始,ROI 也不錯 |
| 🟢 7 | DevOps 中期(IaC、雲端、證照) | 需要比較長的養成時間,適合排在把面試地基補完之後 |
| 🔵 8 | 加分項(Web Vitals / a11y / GraphQL / DSA) | 錦上添花,視你實際投的職缺再挑要不要做 |

---

## 一、前端補強

### 🔴 立即優先 — 你本來會、但底層原理生疏(面試高頻)

#### Vue 底層原理 + 常見面試題庫

- [ ] 響應式系統:Vue2 `Object.defineProperty` vs Vue3 `Proxy` 的差異、各自的限制(陣列 index 賦值偵測不到、新增屬性偵測不到)
- [ ] `ref` vs `reactive` 底層差異 — 為什麼 `ref` 要 `.value`?template 裡為什麼不用寫 `.value`(自動解包的編譯期處理)
- [ ] 依賴收集機制:`track`/`trigger`、`WeakMap<target, Map<key, Set<effect>>>` 的資料結構,講得出「改一個屬性怎麼知道要通知誰重新渲染」
- [ ] `computed` 的 lazy + cache(dirty flag)原理,跟 `watch`/`watchEffect` 的差異與各自使用時機
- [ ] Virtual DOM diff:Vue3 key-based diff(最長遞增子序列優化)vs Vue2 雙端比較;**為什麼 v-for 一定要加 key、不加會怎樣**(經典題)
- [ ] Vue3 編譯期優化:static hoisting、patchFlag、block tree — 這是 Vue3 比 Vue2 快的關鍵,常被問「Vue3 為什麼比較快」
- [ ] `nextTick` 原理(跟 microtask queue、DOM 批次更新的關係)
- [ ] `provide`/`inject` 底層、`defineProps`/`defineEmits` 這些 compiler macro 編譯後長什麼樣子
- [ ] `keep-alive` / `Teleport` 原理(你在 GS-5646 踩過 ClientTeleport 的坑,可以直接整理成面試故事,比背書更有說服力)
- [ ] SSR hydration 原理 — 這個你在 Astro/gnar 有大量實戰(hydration mismatch 排錯經驗),整理成一段可以講的故事,面試常被問「SSR 怎麼運作」

#### JavaScript 底層原理(補充項,跟 Vue 底層同等重要,但不在你原本清單裡)

- [ ] Event loop:macrotask vs microtask,`Promise`/`async-await` 的執行順序(這題幾乎每場面試都會考一段 code 讓你猜輸出順序)
- [ ] 閉包(closure)運作原理 + 常見記憶體洩漏情境
- [ ] Prototype chain、`class` 語法糖底層是什麼、`this` 的四種綁定規則 + arrow function 為什麼不綁定 `this`
- [ ] 手寫題常客:防抖(debounce)/節流(throttle)、簡易版 `Promise`、深拷貝
- [ ] `Promise.all` / `allSettled` / `race` / `any` 的差異與使用情境
- [ ] V8 記憶體管理概念(mark-and-sweep、世代回收)— 了解概念即可,不用背細節

#### 瀏覽器 / 網路協議(你明確要的)

- [ ] **經典題**:網址列輸入到畫面出現,完整走一遍 —— DNS 解析 → TCP 三次握手 → TLS 握手(https)→ HTTP request/response → HTML parse → 建 DOM/CSSOM → Render Tree → Layout → Paint → Composite → JS 執行(遇到 `<script>` 的阻塞行為、`defer`/`async` 差異)
- [ ] TCP 三次握手 / 四次揮手,為什麼是三次不是兩次
- [ ] TLS/SSL 握手流程(非對稱加密交換金鑰 → 之後用對稱加密傳輸、憑證鏈驗證)
- [ ] HTTP/1.1(隊頭阻塞)vs HTTP/2(多工複用、header 壓縮)vs HTTP/3(改用 QUIC/UDP)—— 三代差異跟各自解決的問題
- [ ] 快取機制:強快取(`Cache-Control`/`Expires`)vs 協商快取(`ETag`/`Last-Modified`),兩者怎麼配合用
- [ ] Cookie vs LocalStorage vs SessionStorage vs IndexedDB —— 容量、生命週期、是否跟著 request 送出的差異
- [ ] 同源政策(Same-Origin Policy)+ CORS 運作機制(simple request vs preflight `OPTIONS`)
- [ ] 前端資安基礎:XSS(儲存型/反射型/DOM-based)、CSRF、CSP(`Content-Security-Policy`)—— 這塊剛好能跟你 GS-8192 遇過的資安 sub-bug(source map 外洩)接起來當實戰案例
- [ ] Reflow vs Repaint 差異、為什麼改 `transform`/`opacity` 比改 `width`/`top` 便宜(渲染管線的合成層概念)

### 🟡 中期 — 目前完全不熟,需要重新建立

- [ ] Vitest 單元測試 — 挑一個現有專案的元件/composable 補測試
- [ ] Playwright e2e 測試 — 針對一個完整 user flow(如 login / withdrawal)寫一組 e2e
- [ ] React 基礎重學 —— 建議路線:
  - [ ] Function component + Hooks(`useState`/`useEffect`/`useMemo`/`useCallback`/`useRef`/`useContext`)
  - [ ] 搞懂跟 Vue 最大的心智模型差異:React 是「state 改變 → 整個 component 重新執行」,Vue 是「細粒度追蹤,只更新真的變動的部分」——這個對比本身就是很好的面試素材
  - [ ] JSX 語法、跟 Vue template 的差異
  - [ ] Reconciliation / Fiber 架構 —— 可以跟 Vue diff 放在一起記,面試常兩個一起問
  - [ ] 常見陷阱:`useEffect` 裡抓到舊值的 stale closure、依賴陣列漏寫
  - [ ] 狀態管理:知道 Redux / Zustand / Context API 的差異跟取捨(不用精通,能聊優缺點即可)
  - [ ] 實際寫一個小專案(todo app 或串一個 public API)驗證自己真的會寫,不是只看得懂

### 🔵 加分 / 依應徵職缺再決定要不要做

- [ ] Core Web Vitals / Lighthouse — 對現有專案跑一次分析,寫下 3 個可改善點並實際改
- [ ] 無障礙(a11y) — WCAG 基本規範、ARIA attribute,挑一個頁面做無障礙檢查
- [ ] Build 工具設定能力 — 自己從零設定一次 Vite/webpack config,理解每個選項的作用
- [ ] GraphQL — 了解與 REST 的差異,寫一個小 demo(query + mutation)
- [ ] 資料結構與演算法(LeetCode 風格)— 只有應徵大公司 / 外商才需要重壓,一般前端職缺 CP 值偏低,視目標公司再決定要不要投入

---

## 二、DevOps 補強

> 整體排序見最上方「🎯 整體優先順序建議」——這裡的短/中/長期是 DevOps 賽道自己的內部順序,實際安排時建議先把上面前端 🔴 立即優先做完再回來這裡。

### 短期優先(3-6 個月)

- [ ] Kubernetes object 手寫 — 自己寫 Deployment / Service / Ingress / ConfigMap / Secret,不依賴既有範本
- [ ] Kubernetes debug 實戰 — 練習用 `kubectl describe` / `logs` 排查 pod 起不來的情境(可以故意搞壞一個測試環境練習)
- [ ] CI/CD pipeline 撰寫 — 自己設計一份 `.gitlab-ci.yml` 或 GitHub Actions,包含 stage 設計 + cache 策略
- [ ] 容器化 — 自己寫一個 multi-stage Dockerfile,把一個前端 build 的 image 瘦身

### 中期

- [ ] Infrastructure as Code — Terraform 或 Pulumi 基礎,寫一份小型 IaC 專案
- [ ] 雲端基礎(擇一深:AWS / GCP / Azure) — IAM、VPC、物件儲存
- [ ] 雲端 associate 等級證照一張
- [ ] Secrets 管理 — Vault 或雲端原生 secret manager

### 長期(往 Platform Engineer 移動)

- [ ] Observability — Prometheus / Grafana 架設 + 告警規則設計
- [ ] Log 集中 — Loki 或 ELK stack
- [ ] GitOps — ArgoCD 或 Flux,理解跟「手動 kubectl apply」的差異
- [ ] Reverse proxy / Gateway 深挖 — Kong 的 route / plugin / rate-limit 機制
- [ ] CKA(Certified Kubernetes Administrator)證照

---

## 三、英文

- [ ] 技術寫作練習 — 挑幾份自己寫的中文文件翻成英文版本
- [ ] 面試英文 — 找常見 behavioral + system design 英文題,對著錄音練習
- [ ] 文件閱讀 — 養成優先讀英文官方文件(K8s / Terraform / AWS)的習慣,不等中文翻譯

---

## 學習紀錄

> 每完成一個項目,在這裡補一行:日期 + 做了什麼 + 心得/連結。

- 2026-08-31：建立這份 roadmap。

---

## Backroom 架構演進史(2026-08-31 整理)

> 給分享用的備忘,免得之後忘記脈絡。標「✅ 已查證」的是有翻 git log / commit / 檔案內容確認過;標「🗣 記憶,未查證」的是純粹憑印象、我沒有(或無法)找到 git 證據佐證,分享時請自行斟酌措辭。

### 0. 最初期 — 前後端同專案、多個獨立專案並存(🗣 記憶,未查證)

backroom 這個 git repo 誕生(2023-05)之前的年代。當時前後端是**同一份專案**,裡面會有一個專門給前端的 website 資料夾。整個 BO 由**非常多個獨立專案組成**,每個專案版本可能都不一樣。另外有一份共用 component,自己獨立成一個專案,打包後放到雲端的私有 package registry(見下方確認是 ProGet)。因為當時 Vue2 / Vue3 並存 + 各專案 Node 版本不一致,前人維護的共用 component 最後演變成**好幾種專案 package 版本並存**(不同 app 卡在不同版本,沒辦法全部升上去)。

這段沒有 git 證據可查(backroom repo 本身就是從別處把多個既有專案搬進來的那一刻才開始有記錄),完全依賴記憶,分享時建議註明是回憶轉述。

### 1. 共用元件的雲端 package registry — ProGet(✅ 已查證存在,🗣 起始時間未查證)

確認 `https://proget.higgstar.com/npm/npm-dev/` 是真實存在、被使用過的私有 npm registry(ProGet 是一款商用的私有套件管理服務,支援 npm / NuGet 等多種套件類型)。backroom repo 最早的 commit(2023-05-30)裡,`Higgs.Cs.Website` 的 `package.json` 就已經依賴 `@higgs/utils@1.2.11` 這個 scoped 私有套件 — 版號已經到 1.2.11,代表在 backroom repo 誕生前,這個共用套件就已經存在一段時間、發過不少版本。

git history 裡明確抓到的 ProGet 相關 commit 只有較晚的兩筆:
- `ce4a9252` / `1ec76e55`(2024-11-01)— 把 `registry=https://proget.higgstar.com/npm/npm-dev/` 加回根目錄 `.npmrc`
- `a89ac945` / `96ebbe26`(2025-03-28)— 移除(`alpha.chen/ref/remove-proget`)

這兩筆的時間點比「最初期」晚很多,推測是 ProGet 的 registry 設定原本沒有 commit 進這個 repo(可能放在 CI runner 或開發機的環境層級,不是 committed `.npmrc`),2024-11 那次是重新接回來、2025-03 又拔掉。**這一段落的確切起始時間跟前後脈絡,目前查不到更早的 git 證據**。

現在部分共用套件(如 `@higgs/vue-package`)改用**本地 tarball**(`file:../../../packages/store/higgs-vue-package-0.4.3.tgz`)引用,不再依賴外部 registry — 這應該是 ProGet 退場後的替代做法,但沒有逐一確認是否所有共用套件都改成這個模式。

### 2. 前後端分離 + Monorepo 化(✅ 已查證)

backroom 這個 git repo 建立於 **2023-05-29**(`b668f444`,只有一份 README)。隔天(**2023-05-30**)第二筆 commit「add operation projects」一次把三個既有專案(`Higgs.Backoffice.Workbench.Website`、`Higgs.Crm.Workbench.Website`、`Higgs.Cs.Website`)搬進來,每個底下已經有 `kto/` 子資料夾 — 證實「先全部丟進 backroom,裡面又分 sp/kto」這個階段,一開始就是**單純搬家**,把原本散落各處的獨立前端專案集中到同一個 monorepo,還沒有特別做 CI/CD 調整。

### 3. CI 補上(✅ 已查證,跟 Node 版本調整幾乎同一天)

`.gitlab-ci.yml` 是在 **2023-08-23** 才加進來的,比 monorepo 誕生晚了近 3 個月 — 確認「搬進來那一刻 CI 還沒跟上,是後來才補的」這個印象。同一天/隔天(2023-08-23~24)還有一筆「upgrade project to node 16 version」(`KTO-6041`,注意 ticket prefix 是 `KTO-`,一個比 `SP-` 更早的獨立 Jira project),兩者時間點幾乎重疊,看起來是同一波「先讓 CI 能跑起來」的工程一起做的。

### 4. Node 版本 + Element Plus — 沒有單一統一計畫,是長期陸續升級(✅ 查證「沒有單一計畫」,🗣 現況細節為記憶)

git history 裡**找不到一筆明確的「統一 Node 版本」計畫性 commit**(沒有 `.nvmrc`、沒有符合關鍵字的規劃性 commit),Element Plus 的採用也一樣,是分散在大量小 commit 裡逐步做的,沒有單一起手式時間點。這跟你的記憶吻合:「隔一段時間就慢慢升,不是一次性計畫」。目前現況(依你回憶)大概是設定 Node 16 以上都能跑;實際抽查現有幾個 app 的 `package.json` `engines` 欄位,確實還有多個 app 寫死 `>=16.0.0 <17.0.0`,但這只是 metadata 抽樣,不能代表全貌(可能有些 app 實際執行環境已經更新、只是 `engines` 欄位沒同步)。

### 5. Jira 專案 key 演進(✅ 已查證)

比記憶中更複雜,目前查到至少 4 個 prefix 前後出現過:`KTO-`(最早)→ `SP-` → `PD-`(偶爾出現)→ `GS-`(現行)。**`SP-` → `GS-` 的乾淨切換點是 2025-07-16~18**(`SP-9135` 是最後一筆 SP,`GS-450` 緊接著是第一筆 GS)。是否有經歷過「搬到 GitLab」這個階段沒有辦法確認 —— backroom repo 從最早的 commit(2023-05)開始就已經看得到 GitLab MR merge 記錄(第三筆 commit 就是一個 MR merge),代表這個 repo 從有記錄以來就已經在 GitLab 上,如果真的有「搬到 GitLab」這件事,應該是發生在 backroom repo 誕生之前、更早期分散專案的年代。

### 6. 近期 — CD 架構大改造(✅ 已查證,這幾週正在進行中的工作)

這是我們自己正在做的,不用查 git log,直接記錄:近期(2026-05 起)在做的「code merge」系列(`GS-5954` 這張大票),目標是把 backroom 各 app 內殘留的 `kto/` `sp/` 雙 codepath 合併成單一 source tree,搭配一個新的**per-project pod** 部署架構(每個 project 一個 pod,base image + artifact 疊層,Kong 依 path 分流,不再是「一個 tenant 一份獨立部署」)。子票包含 Marketing(`GS-5959`,已完成)、CS(`GS-6009`,進行中)、Backoffice(`GS-6008`)、Maintenance(`GS-6010`)。這一段是目前 CD(部署)架構的主要調整,跟前面「補 CI 讓它能跑」是完全不同層次的工程 — 前面是「有沒有」,這次是「怎麼部署得更聰明」。

---

## Backroom 完整時間軸(嚴格照日期排序,更細節版)

> 上面第一版是「主題分段」寫法,這版是純時間軸,方便照順序講故事。同樣標示 ✅(有 commit 證據)/ 🗣(記憶,查無 git 證據)。日期均為 commit 日期(`git log --date`),不是實際上線日。

| 日期 | 事件 | 證據 |
|---|---|---|
| (2023 之前) | 前後端同專案、多個獨立專案並存;共用 component 獨立成一個專案發版到 ProGet;Vue2/Vue3 + Node 版本不一致導致共用套件分裂成多個版本並存 | 🗣 記憶,無法查證(backroom repo 誕生前的歷史,不在這個 repo 的記錄範圍內) |
| 2023-05-29 | **backroom repo 誕生**(只有一份 README) | ✅ `b668f444` Initial commit |
| 2023-05-30 | 第一波搬家:`Higgs.Backoffice.Workbench.Website`、`Higgs.Crm.Workbench.Website`、`Higgs.Cs.Website` 三個既有專案整包搬進來,**已經帶著 `kto/` 資料夾**;同時新增 `.npmrc`,`@higgs/utils@1.2.11`(私有共用套件,搬進來時版號已經很成熟)已經是既有依賴 | ✅ `bcfefa4f` add operation projects |
| 2023-06-14 | **Payment 模組最早完成 kto+sp 合併**(目前查到最早的單一模組合併案例,比後來的系統性專案早了將近 3 年) | ✅ `6808ea4c` SP-2747 \| 合併KTO, SP payment project |
| 2023-08-23~24 | 補上 `.gitlab-ci.yml`(monorepo 誕生近 3 個月後才有 CI)+ 同時間一筆 Node 16 升級(`KTO-` 這個更早期的獨立 Jira project) | ✅ `.gitlab-ci.yml` 建檔 commit;`90433c70`/`780641c4` KTO-6041 upgrade to node 16 |
| 2024-11-01 | ProGet registry(`https://proget.higgstar.com/npm/npm-dev/`)被加回根目錄 `.npmrc`(推測是重新接回,不是第一次設定) | ✅ `ce4a9252`/`1ec76e55` |
| 2025-03-28 | ProGet registry 從 `.npmrc` 移除 | ✅ `a89ac945`/`96ebbe26` remove proget registry |
| 2025-07-16~18 | **Jira project key 由 SP- 切換到 GS-**(乾淨切換,`SP-9135` 是最後一筆 SP、`GS-450` 緊接著第一筆 GS);歷史上還出現過 `KTO-`(更早)、`PD-`(偶爾)兩個 prefix | ✅ ticket 序列分析 |
| **2026-02-03** | **「Deprecated KTO brand」**——一次性把 Affiliate、Audit、Crm 等多個 app 的 `kto/` 資料夾清空(git-tracked 檔案數歸零)。這是一個**獨立的品牌退場事件**,推測跟後面 GS-5954 系列不是同一件事:這裡砍掉的 KTO 應該是一個真的不再服務的品牌,跟現在還在服務中的 WB 品牌(WB 在 code 裡也長期借用 `kto` 這個資料夾命名,是命名沿用不是同一個品牌)是兩回事——這段推論沒有 100% 查證,只是目前證據最合理的解讀 | ✅ `GS-4423` Deprecated KTO brand(commit 日期);folder 現況交叉比對 |
| 2026-05-11 | **`GS-5954` 立項**——「backroom code merge & SSR PoC」,拍板 per-project pod 部署架構(base image + artifact 疊層、Kong path 分流),目標把還在服務 WB 品牌的 app(跟上面 2026-02 退場的 KTO 不同)的 `kto/sp` 合併成單一 tree | ✅ plan frontmatter `created: 2026-05-11` |
| (2026-05~06) | Marketing(`GS-5959`)完成合併,是 GS-5954 系列第一個做完的模組 | ✅ plan「已完成」列表(未逐一查 commit 日期) |
| 2026-07-30 | Backoffice(`GS-6008`)kto/sp 合併樹完成 + forward-port master | ✅ `092a267a` GS-7618 |
| 2026-08-11 | **Maintenance Workbench 直接退役**(不是合併!整包搬到 `deprecated/`,k8s/nginx 層另外處理)——這是 GS-5954 系列裡唯一一個「不合併、直接退場」的模組 | ✅ `8fef2713` GS-7621 |
| 2026-08-12 | **Backoffice 兩段式改名成 Hub**(同一天做完):先 `apps/Higgs.Backoffice.Workbench.Website` → `apps/Hub`(package 也改 `@gpp/hub-sp`),幾小時後再從 `apps/Hub/sp` → `apps/hub/generic`(理由是這包早就不是 sp 專屬 build 了——CI 本來就用 `BUILD_BRAND=sp`/`wb` 兩種參數各 build 一次同一包,folder 掛著 sp 名字反而誤導) | ✅ `42f69cac` GS-7317 rename;`cfdaa14f` GS-7895 move to apps/hub/generic(commit 訊息直接寫了改名理由) |
| 2026-08-19 | CS 模組改名:`apps/Higgs.Cs.Website/sp` → `apps/cs/generic`,package `@gpp/cs-sp` → `@gpp/cs`(GS-6009 的一部分,新架構命名規則:app 名小寫、統一叫 `generic`——跟 Hub 是同一套改名邏輯) | ✅ `bca11424` GS-6009 cs rename |
| 2026-08(進行中) | CS(`GS-6009`)kto/sp 合併工作進行中,尚未完全結束 | ✅ 這幾天我們自己在做的事,不用查 git log |
| 尚未開始 | IT-Operation(`GS-6030`)還沒動,目前查到 git 上還有 240 個 kto 檔案完整存在 | ✅ 直接檢查 git-tracked 檔案數確認 |

**額外發現,原本沒問過你、但值得記錄**:

1. 目前 `apps/` 底下同時存在舊命名(`Higgs.XXX.Workbench.Website`)跟新命名(`cs`、`hub`,小寫、底下都是 `generic` 資料夾)兩種風格並存 —— 代表新架構的搬遷是**逐一模組進行**,不是一次性重新命名全部,搬到新架構的模組才會換成新命名規則。目前只有 CS、Hub(即前 Backoffice)兩個模組換了新命名,Payment 目前還是掛著 `Higgs.Payment.Workbench.Website` 舊名,還沒被搬(原本記憶中以為 Payment 也有新命名,查證後發現沒有,修正)。
2. 有個獨立的 `deprecated/` 資料夾,專門收「合併完成後」被取代的舊 `kto/` 資料夾(整包搬過去,不是刪除),命名規則是 `<原App名>.Kto`。目前裡面有 Affiliate、Audit、Backoffice(即 Hub)、Crm、Cs、Marketing、Payment、Report 八個 `.Kto`,代表這八個模組的 kto/sp 合併都已收尾;`Maintenance` 是整包(不加 `.Kto` 後綴)被丟進 `deprecated/`,因為它是退役不是合併(呼應前面表格 2026-08-11 那筆)。
3. Kyc、RiskControl 兩個模組經查證**從頭到尾就沒有 `kto/` 資料夾**(整個 git history 都查不到),代表它們一開始就是 SP 單一租戶 app,根本不屬於「kto/sp 合併」這個故事線,不用特別去追它們的合併進度。
4. 目前唯一還沒動的是 `Higgs.It.Operation.Website`,`kto/` 底下還有 240 個檔案,對應前面表格「尚未開始」那筆(`GS-6030`)。

---

## 前台(玩家端)架構演進史 — arena → gnar

> 你的原始記憶:「一開始是 portal、brand-component、cs-component 三個組成在一起,後來用 arena 把它們丟起來一起管理,最後重構成 gnar 一個專案處理全部」。查 arena + gnar 兩個 repo 的完整 git log 後,骨架完全對上,而且挖到比記憶更細的日期跟幾個記憶沒提到的東西(下面有標)。同樣用 ✅(有 commit 證據)/ 🗣(記憶,查無證據)標示。

### 時間軸

| 日期 | 事件 | 證據 |
|---|---|---|
| 2024-07-09~10 | **arena repo 誕生**,但誕生時原名其實是 `portal`——第一個 commit 的 README 就寫「# portal」,根目錄 `package.json` 的 `"name"` 欄位到現在都還是 `"portal"`,從沒改過(GitLab 專案後來被改名成 `arena`,但這個改名是 GitLab 專案設定層級的事,git log 裡看不到確切時間點,repo 內部這兩個檔案就是沒跟著更新,算是一個活化石) | ✅ `40e2abf` Initial commit;`git remote -v` 現在指向 `.../frontend/arena.git`,但 `package.json`/`README.md` 內容仍是 `portal` |
| 2024-07-10~11 | `Higgs.Portal.Promote.Website`(推廣/活動微站,你原本沒提到的第 4 個)很早就進來了,看起來是 arena 自己原生的內容,不是後面「搬 3 個專案進來」那批 | ✅ 位於最早幾筆 commit 附近 |
| 2024-07-31 | **Portal 本體**(原專案名 `sp-portal-web`)+ **Affiliate** 同批搬進 arena,落地成 `apps/portal`、`apps/affiliate` | ✅ `5ef4e14`/`e23eede` SP-5982~5985「move project and adjust ci config」/「sp-portal-web 轉 gitlab runner」 |
| 2024-08-01 | **brand-cs-component**(你記憶中的 cs-component)搬進來,落地成 `apps/brand-cs` | ✅ `8160628` SP-5988「brand-cs-component 轉 gitlab runner」 |
| 2024-08-06 | **brand-component** 搬進來,落地成 `apps/brand` | ✅ `98f373c` SP-5986「brand-component 轉 gitlab runner」 |
| 2024-08-08 | 三個專案搬遷收尾(CI 路徑、build 變數等細節調整) | ✅ `d59a58f` SP-5987「move project into repo」 |
| 2024-08-13 | **改成你記憶中的最終名字**:`apps/brand` → `apps/brand-components`,`apps/brand-cs` → `apps/cs-components`(同一筆 commit 一次做完) | ✅ `338a097` SP-5989「rename project name」 |
| 2024-08~2026-02 | arena 以「一個 repo、四個 app(portal / affiliate / brand-components / cs-components)」的形態運作超過一年半,期間也跟著 backroom 一起經歷 Jira project key `SP-` → `GS-` 的切換 | ✅ commit 序列交叉比對(與 backroom 段落同一波切換) |
| 2026-02-05 | `Higgs.Portal.Promote.Website` 隨 **KTO 品牌退場**被移除——跟 backroom 段落記錄的 2026-02-03「Deprecated KTO brand」是**同一波跨 repo 行動**,只差 2 天,backroom 先做、arena 晚 2 天跟進 | ✅ `8dfe249` GS-4423「Deprecate KTO related code」 |
| **2025-09-12** | **gnar repo 誕生**——這件事跟上面 arena 的故事線是**平行的、不是接續的**:gnar 不是把 arena 的 code 搬過來,是**全新從零開始**,第一批 commit 就是「Portal1.5」重寫計畫(新技術棧 Astro + Vue3,取代 arena 那個舊 Vue2 portal) | ✅ `a958bcdd` Initial commit,緊接著 `GS-1684`/`GS-1681`/`GS-1676`(footer / privacy / landing page)等 Portal1.5 sub-task |
| 2025-10-09 | gnar 建立自己的共用元件系統 **`packages/boom`**(基於 Lit,支援 Vue/React/原生 JS 跨框架),整合進 portal——這概念上接手了 arena `brand-components` 的角色,但**不是搬程式碼過去,是重新造**一套 | ✅ `ec4449f6` GS-2382「initialize boom lit package and integrate to portal」 |
| 2026-04-27~06-23 | **GS-5646「Portal migration(arena → gnar)」**——把 arena portal 的功能一項項移植進 gnar 的新 Astro 殼,8 週計畫,整合分支 `alpha.chen/feat/GS-5648`,06-23 單次跟其他團隊一起上線 master(這段細節在 requirements repo 自己的 rule 檔裡有完整記錄,不用重挖) | ✅ `requirements/.claude/rules/gs5646-integration-branch.md`(rule 檔本身) |
| 2026-06-11 | gnar `packages/store` 加了一個 **`cs-umd-bridge`**——過渡期用的橋接機制,讓 gnar 頁面能暫時繼續叫 arena 那邊還沒搬過來的 CS 元件(UMD 包、只服務 SP 一個品牌),等真正的 CS 遷移完成前的權宜之計 | ✅ `307ee9f6` GS-5646「cs-umd-bridge — interim SP-only UMD tenancy serving」 |
| 2026-06-17~07-16 | arena 的 `apps/portal` 實質上凍結(最後一筆只是 lockfile 層級的東西);`brand-components` 也差不多同期停更;`cs-components` 撐到 07-16 補了一個資安修復才停 | ✅ 各 app 資料夾 `git log -1` 交叉比對 |
| **2026-08-11~08-14** | **CS-components 真正遷進 gnar**——`GS-8148`「CS 遷移至 gnar(KTO/WB)+ multi-brand 化」這個 epic,子票 GS-8209(抽成 `packages/cs`)→ GS-8213(`apps/call-center` 落地,WB CS 站上線)。這件事發生在**這個月**,幾乎是最新鮮的一塊拼圖 | ✅ `7cda08e0` GS-8209、`0c0f516b` GS-8213;`requirements/GS-8148/GS-8148-plan.md` |
| 2026-07-31 | (旁支,跟上面故事不同線但也是 gnar「處理全部」的一部分)gnar 多了 `apps/backroom-hosting`(前身叫 `backroom-pod`)——gnar 現在也負責 host **backroom(BO)** 的 pod 產物,呼應前面 backroom 段落記的 per-project pod 部署架構 | ✅ `7597bb70` GS-7893「rename backroom-pod → backroom-hosting」 |
| **現在(2026-08-31)** | gnar 目前是 `apps/portal`(玩家 portal)+ `apps/call-center`(CS 客服站)+ `apps/backroom-hosting`(BO pod 託管)+ 4 個共用 package(`boom` UI 元件 / `cs` / `kits` / `store`) | ✅ 直接 `ls apps/ packages/` |

### 跟你原本記憶對照一下,有一個修正

你說「最後重構成 gnar 一個專案處理全部了」——**目前查證下來還沒到「全部」**:arena 的 `apps/affiliate` 到 2026-07-01 都還有人在加功能(`GS-7100` 加 E-Bingo/Specialty 報表),gnar 這邊完全沒有對應的 affiliate app(只有 portal 裡一個處理推薦碼的 middleware,跟「代理後台」不是同一件事)。也查了 requirements repo 裡目前所有跟「affiliate」+「gnar」相關的票,都只是「這張票跟 arena affiliate 無程式交集」這種備註,沒看到任何遷移計畫在排。所以現況比較準確的說法是:**Portal 已完成遷移(GS-5646)、CS 剛完成遷移(GS-8148,這個月)、Affiliate 還留在 arena,沒有遷移排程**——arena 還沒能真正退役,還有一塊(affiliate)在單獨活著。

🗣 你補充:affiliate 比較特別,還沒決定好要怎麼處理,但未來高機率也會丟進 gnar(這段是你的判斷,還沒有對應的 Jira 票或 plan 文件可查證,先記錄成待驗證的方向)。
