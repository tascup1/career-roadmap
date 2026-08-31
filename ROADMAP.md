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

## 一、前端補強

### 短期優先(3-6 個月,投報率最高)

- [ ] Vitest 單元測試 — 挑一個現有專案的元件/composable 補測試
- [ ] Playwright e2e 測試 — 針對一個完整 user flow(如 login / withdrawal)寫一組 e2e
- [ ] Core Web Vitals / Lighthouse — 對現有專案跑一次分析,寫下 3 個可改善點並實際改

### 中期

- [ ] React 基礎 — 能看懂、能寫一個小專案(不需要精通,面試能聊即可)
- [ ] 無障礙(a11y) — WCAG 基本規範、ARIA attribute,挑一個頁面做無障礙檢查
- [ ] Build 工具設定能力 — 自己從零設定一次 Vite/webpack config,理解每個選項的作用
- [ ] GraphQL — 了解與 REST 的差異,寫一個小 demo(query + mutation)

---

## 二、DevOps 補強

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
