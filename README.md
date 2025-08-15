# AI Career Assistant 智能求職幫手

> 基於 AI 技術的履歷分析與職缺匹配平台

## 📋 專案概述

AI Career Assistant 是一個智能求職輔助平台，能夠自動分析用戶履歷、提取關鍵信息，並匹配推薦合適的職缺機會。結合自然語言處理、職缺搜尋和機器學習技術，為求職者提供個性化的職涯建議。

### ✨ 核心功能

- **📄 履歷解析**: 支援PDF、Word格式，自動提取學歷、經歷、技能
- **👤 人像識別**: 檢測履歷中的個人照片
- **🔍 智能匹配**: 基於專長和年資的職缺推薦
- **🌐 多平台搜尋**: 整合LinkedIn、104人力銀行、518熊讚、小雞上工
- **🤖 AI分析**: 深度履歷分析與職涯建議
- **⚡ 高效處理**: 10秒內完成完整分析流程

### 🎯 產品特色

- **零存檔設計**: 保護用戶隱私，處理完畢即刪除
- **RAG增強搜尋**: 結合搜尋引擎提升匹配準確度  
- **分層推薦**: 專長匹配 + 年資匹配 + 潛力推薦
- **即時分析**: 支援最多3人同時使用

## 🏗️ 技術架構

### 核心技術棧 (2025更新)
- **後端**: Python 3.11+ (FastAPI)
- **前端**: React 18+ / Next.js 14+ (TypeScript)
- **工作流引擎**: n8n (Node.js)
- **AI 整合**: Google Gemini Multi-Agent 架構
- **容器化**: Docker + Docker Compose

### Multi-Agent AI 系統
- **Agent Router**: 智能路由與負載均衡
- **Career Advice Agent**: 職涯諮詢專家
- **Resume Analysis Agent**: 履歷分析專家
- **Interview Prep Agent**: 面試準備教練
- **Emotional Support Agent**: 情感支持專家

### 工作流自動化 (n8n)
- **履歷生成工作流**: AI 驅動的個人化履歷生成
- **求職信生成工作流**: 針對特定職位的求職信
- **面試準備工作流**: STAR 方法答案生成與模擬面試
- **智能推薦工作流**: 職位與技能推薦系統

### 資料層
- **主資料庫**: PostgreSQL 15+
- **快取系統**: Redis
- **檔案存儲**: AWS S3 / Google Cloud Storage
- **監控**: Prometheus + Grafana
- **日誌**: ELK Stack

## 📁 專案結構

```
AI-Career-Assistant/
├── .ai-rules/                                # AI 助手規則與文檔
│   ├── product.md                           # 產品願景與核心價值
│   ├── tech.md                             # 技術棧與依賴管理
│   ├── structure.md                        # 目錄結構與命名規則
│   └── architecture.md                     # 架構決策記錄
├── docs/                                    # 完整實作規劃文檔
│   ├── requirements.md                     # EARS 格式功能需求
│   ├── design.md                          # 詳細技術設計規格  
│   ├── tasks.md                           # 35 個開發任務計劃
│   ├── architecture.md                    # 系統架構與 Mermaid 圖表
│   ├── PRD-Enhancement-v3.0.md            # 最新產品需求文檔
│   ├── n8n-technical-reference.md         # n8n 技術參考文檔
│   ├── n8n-workflow-config.json           # n8n 工作流配置
│   └── 📚 教學文檔系列/                    # SuperClaude教學體系
│       ├── 教學文檔導航手冊.md              # 🧭 學習路徑導航
│       ├── 教學文檔-階段二架構重構.md       # 📘 技術深度學習
│       ├── AI求職助手改善教學指南.md        # 📗 實戰改善指南  
│       └── 外行友好的AI開發流程說明.md      # 📙 非技術人員友好
├── backend/                                # Python FastAPI 後端
│   ├── app/
│   │   ├── api/                           # API 路由
│   │   ├── core/                          # 核心配置
│   │   ├── models/                        # 數據模型
│   │   ├── services/                      # 業務邏輯
│   │   └── agents/                        # AI Agent 模組
│   ├── tests/
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/                               # React/Next.js 前端
│   ├── src/
│   │   ├── components/                    # UI 組件
│   │   ├── pages/                         # 頁面
│   │   ├── hooks/                         # React Hooks
│   │   └── utils/                         # 工具函數
│   ├── public/
│   ├── package.json
│   └── Dockerfile
├── n8n/                                   # n8n 工作流
│   ├── workflows/                         # 工作流定義
│   ├── custom-nodes/                     # 自定義節點
│   └── docker-compose.yml
├── specs/                                 # 功能規格文檔
│   └── features/
│       └── resume-collection/             # 模組化履歷收集系統
│           ├── requirements.md
│           ├── design.md
│           └── tasks.md
├── scripts/                               # 部署腳本
├── tests/                                 # 整合測試
└── docker-compose.yml                    # 整體服務編排
```

## 🚀 快速開始

### 環境要求
- Python >= 3.11
- Node.js >= 18.0
- Docker & Docker Compose
- Redis
- PostgreSQL 15+
- Git

### 快速啟動 (Docker)

1. **克隆專案**
```bash
git clone https://github.com/minxinchen/AI-Career-Assistant.git
cd AI-Career-Assistant
```

2. **一鍵啟動所有服務**
```bash
docker-compose up --build
```

3. **訪問應用**
- 前端應用: http://localhost:3000
- 後端 API: http://localhost:8000
- n8n 工作流: http://localhost:5678
- 監控面板: http://localhost:3001

### 本地開發設置

1. **後端服務 (FastAPI)**
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload
```

2. **前端應用 (Next.js)**
```bash
cd frontend
npm install
npm run dev
```

3. **n8n 工作流引擎**
```bash
cd n8n
docker-compose up n8n
```

### 環境變數配置

創建 `.env` 檔案：
```env
# AI 服務配置
GEMINI_API_KEY=your_gemini_api_key

# 資料庫配置
DATABASE_URL=postgresql://user:password@localhost:5432/ai_career_db
REDIS_URL=redis://localhost:6379

# n8n 配置
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=your_password

# 應用配置
API_BASE_URL=http://localhost:8000
FRONTEND_URL=http://localhost:3000
```

## 📊 開發路線圖 (2025 更新)

### 🎯 三階段開發計劃 (6 個月)

#### 🥉 **MVP 階段** (Month 1-2) - 核心功能驗證
- [x] **專案初始化**: Monorepo 結構 + Docker 開發環境
- [x] **資料庫架構**: PostgreSQL + Redis 基礎配置  
- [x] **API 服務**: FastAPI 基礎架構 + 健康檢查
- [ ] **用戶系統**: JWT 認證 + 個人資料管理
- [ ] **文件處理**: PDF 解析 + 雲端存儲
- [ ] **基礎 AI**: Gemini API 整合 + 聊天介面
- [ ] **履歷分析**: AI 驅動分析 + 改善建議
- [ ] **MVP 部署**: 測試環境 + 整合測試

#### 🥈 **Beta 階段** (Month 3-4) - Multi-Agent 整合
- [ ] **Agent Router**: 智能路由 + 負載均衡
- [ ] **專業 Agents**: 4 個專業 AI Agent 開發
- [ ] **Context 管理**: 對話上下文 + 持久化
- [ ] **n8n 整合**: 工作流引擎 + 基礎連接
- [ ] **履歷生成**: AI 驅動模板生成工作流
- [ ] **求職信 & 面試**: 個人化內容生成
- [ ] **敏感話題**: 就業空白期等智能處理
- [ ] **智能推薦**: 職位 + 技能推薦系統
- [ ] **前端優化**: PWA + 響應式重構
- [ ] **分析儀表板**: 職涯進度可視化

#### 🥇 **Production 階段** (Month 5-6) - 優化與部署
- [ ] **性能優化**: 資料庫 + API + 前端效能提升
- [ ] **安全強化**: OWASP 合規 + 資料加密
- [ ] **合規檢查**: GDPR + 隱私權政策
- [ ] **監控系統**: Prometheus + Grafana + 告警
- [ ] **CI/CD 優化**: 藍綠部署 + 自動回滾
- [ ] **備份災援**: 自動備份 + 災難復原
- [ ] **生產環境**: Kubernetes + SSL + CDN
- [ ] **上線部署**: 全面測試 + 正式發布
- [ ] **運維監控**: 持續監控 + 用戶反饋

### 📈 關鍵里程碑
- **M1** (Month 2): MVP 功能完整，50 並發用戶
- **M2** (Month 4): Multi-Agent 系統，200 並發用戶  
- **M3** (Month 6): 生產就緒，1000 並發用戶

### 🎨 創新特色
- **Sub-Agent 協作**: steering-architect + strategic-planner + prd-writer
- **EARS 格式**: Event-Action-Response-Stimulus 結構化需求
- **模組化設計**: 履歷收集系統可獨立移除
- **敏感話題處理**: 同理心 AI 回應機制
- **n8n + Gemini**: 無代碼工作流 + 多模態 AI

## 🛠️ API 文檔

### 用戶認證
```typescript
POST /api/v1/auth/register
POST /api/v1/auth/login
GET /api/v1/users/profile
```

### 文件處理
```typescript
POST /api/v1/documents/upload
GET /api/v1/documents/{id}/analyze
POST /api/v1/documents/{id}/improve
```

### AI 聊天
```typescript
POST /api/v1/chat/conversations
POST /api/v1/chat/conversations/{id}/messages
WebSocket /ws/chat/{conversationId}
```

### n8n 工作流
```typescript
POST /api/v1/workflows/execute
GET /api/v1/workflows/executions/{id}
GET /api/v1/workflows/templates
```

詳細 API 設計規格請參考：
- 📋 [requirements.md](docs/requirements.md) - EARS 格式功能需求
- 🏗️ [design.md](docs/design.md) - 完整技術設計規格
- 📊 [tasks.md](docs/tasks.md) - 35 個開發任務計劃

## 🔒 隱私與安全

### 資料保護
- **端到端加密**: TLS 1.3 傳輸 + AES-256 儲存加密
- **GDPR 合規**: 資料可攜權、被遺忘權、資料最小化
- **敏感話題保護**: 就業空白期等資訊選擇性分享
- **審計日誌**: 完整操作記錄 (保留 90 天)

### 存取控制
- **JWT + OAuth 2.0**: 多層身份驗證
- **RBAC 權限管理**: 角色基礎存取控制
- **API 速率限制**: 防 DDoS 攻擊與濫用
- **輸入驗證**: 防 SQL 注入、XSS、CSRF

### 安全監控
- **即時告警**: 異常行為自動偵測
- **滲透測試**: 定期安全掃描
- **零信任架構**: 最小權限原則

## 📈 效能指標 (目標)

### 性能指標
- **API 回應時間**: < 200ms (95% 請求)
- **AI 對話回應**: < 3 秒 (95% 情況)  
- **履歷解析時間**: < 10 秒 (5MB 檔案)
- **並發用戶**: > 1000 人同時在線

### 可靠性指標
- **系統可用性**: > 99.9%
- **錯誤率**: < 0.1%
- **資料完整性**: 100%
- **備份恢復**: RTO < 4 小時, RPO < 1 小時

### 品質指標  
- **履歷解析準確率**: > 95%
- **AI 回應品質**: > 85 分 (人工評估)
- **用戶滿意度**: > 85%
- **推薦成功率**: > 70%

## 🤝 貢獻指南

歡迎提交 Issues 和 Pull Requests！

1. Fork 此專案
2. 創建您的功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交您的修改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 開啟一個 Pull Request

## 📚 教學資源

### 🎓 SuperClaude教學體系

本項目特別提供完整的教學文檔系列，適合不同背景的學習者：

#### 🧭 開始您的學習之旅
📖 **[教學文檔導航手冊](docs/教學文檔導航手冊.md)**
- 根據您的背景選擇最適合的學習路徑
- 技術深度、實戰改善、基礎理解、商業價值四大路徑
- 完整的學習資源和進階建議

#### 📘 技術專業深度學習路徑
📖 **[教學文檔-階段二架構重構](docs/教學文檔-階段二架構重構.md)**
- **適合**: 軟體工程師、系統架構師、技術主管
- **內容**: 微服務架構設計、性能優化實戰、安全加固方案
- **時間**: 6-8小時深度學習 + 實踐項目

#### 📗 產品改善實戰路徑  
📖 **[AI求職助手改善教學指南](docs/AI求職助手改善教學指南.md)**
- **適合**: 產品經理、項目經理、QA工程師、創業者
- **內容**: 問題診斷框架、用戶體驗優化、數據驅動決策
- **時間**: 4-6小時學習 + 改善項目實施

#### 📙 非技術人員友好路徑
📖 **[外行友好的AI開發流程說明](docs/外行友好的AI開發流程說明.md)**
- **適合**: 老闆、投資人、行銷人員、一般用戶
- **內容**: 用生活化比喻解釋AI系統、商業模式分析、投資價值評估
- **時間**: 2-3小時輕鬆學習

### 🔍 專案文檔 (2025 完整實作規劃)

#### 📋 核心規劃文檔
基於三件套 sub-agents 協作的完整實作規劃：

- 📋 **[requirements.md](docs/requirements.md)**: EARS 格式功能需求 (10+10 需求項目)
- 🏗️ **[design.md](docs/design.md)**: 詳細技術設計規格 (API+資料模型+Multi-Agent)
- 📊 **[tasks.md](docs/tasks.md)**: 35 個開發任務計劃 (MVP→Beta→Production)
- 🔧 **[architecture.md](docs/architecture.md)**: 系統架構與 3 個 Mermaid 圖表

#### 🤖 標準化文檔 (.ai-rules)
- 🎯 **[product.md](.ai-rules/product.md)**: 產品願景與核心價值
- ⚙️ **[tech.md](.ai-rules/tech.md)**: 技術棧與依賴管理  
- 📁 **[structure.md](.ai-rules/structure.md)**: 目錄結構與命名規則

#### 📚 技術參考文檔
- 🔗 **[n8n-technical-reference.md](docs/n8n-technical-reference.md)**: n8n 完整技術參考 (15,000+ tokens)
- ⚡ **[n8n-workflow-config.json](docs/n8n-workflow-config.json)**: n8n Multi-Agent 工作流配置
- 📈 **[PRD-Enhancement-v3.0.md](docs/PRD-Enhancement-v3.0.md)**: 最新產品需求文檔

#### 🏗️ 模組化規格
- 📦 **[specs/features/resume-collection/](specs/features/resume-collection/)**: 可獨立移除的履歷收集系統

## 📄 授權

本專案採用 MIT 授權 - 詳見 [LICENSE](LICENSE) 檔案

## 📞 聯絡方式

- **作者**: minxinchen
- **專案網址**: https://github.com/minxinchen/AI-Career-Assista
- **問題回報**: [Issues](https://github.com/minxinchen/AI-Career-Assista/issues)

---

*這是一個教學專案，展示人機協作開發的完整流程*