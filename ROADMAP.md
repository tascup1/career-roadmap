# Career Roadmap — Frontend → Frontend/DevOps → Platform Engineer

> 建立日期:2026-08-31
> 目標:近期往「前端為主、DevOps 加分」的職缺移動,長期往「Platform Engineer / SRE」方向發展。
> 用法:每完成一項打勾 `- [x]`,並在對應章節下方補一行日期 + 心得/連結,當作學習紀錄。
> 相關文件:公司專案細節 / 架構演進史 / CI-CD 流程記憶備忘,拆到另一份 [PROJECT-NOTES.md](./PROJECT-NOTES.md),本檔只放學習路線圖。

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
| 🔴 4 | 打包 / 建構工具原理(Vite/Webpack/Rollup) | 你天天用 Vite + pnpm monorepo,但多半是「會設定」而非「懂原理」;跟瀏覽器/JS 底層同一類複習題,而且能直接接上你已有的 source map 資安實戰經驗 |
| 🟡 5 | Testing(Vitest / Playwright) | 公司沒用過,完全空白,但幾乎所有中大型公司面試都會問「你們怎麼測試」——現在補這塊比臨場硬凹划算 |
| 🟡 6 | React 重新學 | 忘光了,重建成本最高,所以排在「複習類」後面;但補了能讓應徵的職缺池直接翻倍(很多公司 React-first) |
| 🟢 7 | DevOps 短期優先(K8s 手寫、CI/CD、容器化) | 你已經有 K8s 部署觸發 + Kong 的實戰經驗,這裡是「從會用到會設計」的深化,不是從零開始,ROI 也不錯 |
| 🟢 8 | DevOps 中期(IaC、雲端、證照) | 需要比較長的養成時間,適合排在把面試地基補完之後 |
| 🔵 9 | 加分項(Web Vitals / a11y / GraphQL / DSA) | 錦上添花,視你實際投的職缺再挑要不要做 |

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

#### 打包 / 建構工具原理(Bundling)

> 你有紮實的 Vite + pnpm monorepo 實戰(gnar/backroom 兩邊都是),這塊多半是「會設定、沒細想過為什麼」,補完原理投報率很高,不算從零開始。

- [ ] 模組系統:CommonJS vs ESM 的差異、為什麼只有 ESM 能做 tree-shaking(靜態分析 import/export vs `require` 是動態的)、兩者互操作(interop)常見的坑
- [ ] Tree-shaking 原理:bundler 怎麼判斷一段程式碼「沒被用到」、`package.json` 的 `sideEffects` 欄位怎麼影響判斷、為什麼 `import _ from 'lodash'` 搖不掉但 `import debounce from 'lodash/debounce'` 可以
- [ ] Code splitting:動態 `import()` 怎麼觸發自動分包、vendor chunk / common chunk 怎麼分、為什麼要這樣分(瀏覽器快取命中率)
- [ ] Module 解析演算法:bundler 怎麼從一個 import path 找到實際檔案(node_modules 逐層往上找、`package.json` 的 `main`/`module`/`exports` 欄位優先序)
- [ ] Vite 原理(你天天在用,補這塊最划算):
  - [ ] Dev server 為什麼不用整包打包 —— 直接餵瀏覽器原生 ESM、按需編譯每個被 request 到的檔案
  - [ ] `optimizeDeps` 預打包依賴在解決什麼問題(node_modules 裡的 CJS 套件轉 ESM、把幾百個小檔案的套件合併減少 request 數)
  - [ ] Production build 為什麼改用 Rollup(而不是延續 dev 模式那套 esbuild-only 策略)
  - [ ] HMR(Hot Module Replacement)大致運作原理 — 為什麼改一個 `.vue` 檔案畫面能局部更新而不整頁刷新
- [ ] Webpack 概念(即使公司用 Vite,很多公司面試還是問這個,懂原理就好不用精通設定):Loader vs Plugin 的差異、compiler/compilation/module/chunk 這幾層分別是什麼
- [ ] esbuild / SWC —— 為什麼比 Babel/tsc 快(Go/Rust 寫的、平行處理),Vite 底層怎麼用它們(dev 模式的依賴預打包、TS/JSX 轉譯)
- [ ] Bundle 分析與優化實戰:用 `rollup-plugin-visualizer`(Vite 對應版本)對現有專案跑一次,實際找出最肥的幾個依賴,想辦法瘦身
- [ ] Source map 原理 + production 正確處理方式 —— **這題你有真實故事可以講**:GS-7394 那張 sub-bug(Publicly Exposed Production Source Map)剛好是活教材,被問「source map 是什麼、production 要注意什麼」可以直接舉這個真實案例
- [ ] Monorepo 建構編排工具:Turborepo / Nx 的概念(增量建構、遠端快取、task pipeline 依賴宣告)—— 你熟 pnpm workspace,但這層編排工具鏈如果沒碰過,值得認識一下,不少公司拿這個當加分題

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
- 2026-08-31：把公司專案細節 / 架構演進史 / CI-CD 流程拆到 [PROJECT-NOTES.md](./PROJECT-NOTES.md),本檔專心放學習路線圖。
