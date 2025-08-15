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

### 前端技術棧
- **框架**: React.js + Ant Design
- **狀態管理**: Redux
- **檔案上傳**: react-dropzone
- **HTTP客戶端**: Axios

### 後端技術棧
- **運行環境**: Node.js
- **框架**: Express.js
- **並發控制**: Redis + Bull Queue
- **檔案處理**: Multer

### AI/ML 技術
- **LLM**: OpenAI GPT-4 API / Claude API
- **OCR**: Google Cloud Vision API
- **人像識別**: OpenCV / AWS Rekognition
- **中文NLP**: jieba分詞 + CKIP Transformers
- **RAG框架**: LangChain
- **向量數據庫**: Pinecone

### 職缺數據源
- **官方API**: 104人力銀行 API
- **網頁爬蟲**: Puppeteer + Selenium
- **搜尋增強**: Google Custom Search API

## 📁 專案結構

```
AI-Career-Assistant/
├── docs/                                      # 專案文檔
│   ├── PRD.md                                # 產品需求文檔
│   ├── API-Design.md                         # API設計文檔
│   ├── Architecture.md                       # 系統架構文檔
│   ├── Development-Log.md                    # 開發歷程記錄
│   ├── Stage1-System-Assessment.md           # 階段一系統評估
│   └── 📚 教學文檔系列/                       # SuperClaude教學體系
│       ├── 教學文檔導航手冊.md                 # 🧭 學習路徑導航
│       ├── 教學文檔-階段二架構重構.md          # 📘 技術深度學習
│       ├── AI求職助手改善教學指南.md           # 📗 實戰改善指南  
│       └── 外行友好的AI開發流程說明.md         # 📙 非技術人員友好
├── frontend/                                 # 前端應用
│   ├── src/
│   ├── public/
│   └── package.json
├── backend/                                  # 後端服務
│   ├── src/
│   ├── config/
│   └── package.json
├── ai-services/                              # AI分析服務
│   ├── resume-parser/
│   ├── job-matcher/
│   └── requirements.txt
├── scripts/                                  # 部署腳本
└── README.md
```

## 🚀 快速開始

### 環境要求
- Node.js >= 16.0
- Python >= 3.8
- Redis
- Git

### 安裝步驟

1. **克隆專案**
```bash
git clone https://github.com/minxinchen/AI-Career-Assista.git
cd AI-Career-Assistant
```

2. **前端設置**
```bash
cd frontend
npm install
npm start
```

3. **後端設置**
```bash
cd backend
npm install
npm run dev
```

4. **AI服務設置**
```bash
cd ai-services
pip install -r requirements.txt
python app.py
```

### 環境變數配置

創建 `.env` 檔案：
```env
OPENAI_API_KEY=your_openai_key
GOOGLE_VISION_API_KEY=your_google_key
REDIS_URL=redis://localhost:6379
PORT=3000
```

## 📊 開發進度

### 開發階段 (8週計劃)

- [ ] **Phase 1**: 基礎建設 (Week 1-2)
  - [ ] 前端框架搭建
  - [ ] 後端API建立
  - [ ] 檔案上傳功能
  - [ ] Redis系統配置

- [ ] **Phase 2**: 履歷解析核心 (Week 3-4)
  - [ ] PDF/Word解析
  - [ ] OCR文字識別
  - [ ] 人像檢測
  - [ ] 並發控制機制

- [ ] **Phase 3**: AI分析與職缺搜尋 (Week 5-6)
  - [ ] LLM分析整合
  - [ ] 職缺平台API開發
  - [ ] RAG搜尋系統
  - [ ] 匹配算法實現

- [ ] **Phase 4**: 整合與優化 (Week 7-8)
  - [ ] 前後端整合
  - [ ] 效能優化
  - [ ] 全流程測試
  - [ ] 部署上線

### 里程碑
- **M1** (Week 2): 檔案上傳功能完成
- **M2** (Week 4): 履歷解析準確率>85%
- **M3** (Week 6): 10個職缺推薦功能完成
- **M4** (Week 8): 完整流程<10秒響應

## 🛠️ API 文檔

### 履歷上傳
```
POST /api/upload
Content-Type: multipart/form-data

參數: file (PDF/Word檔案)
回應: 處理狀態與工作ID
```

### 分析結果
```
GET /api/analysis/{jobId}

回應: {
  "resume_analysis": {...},
  "job_recommendations": [...],
  "suggestions": [...]
}
```

詳細API文檔請參考 [API-Design.md](docs/API-Design.md)

## 🔒 隱私與安全

- **零存檔政策**: 履歷檔案處理完畢後立即刪除
- **HTTPS加密**: 所有數據傳輸均使用SSL加密
- **API限流**: 防止濫用，保護系統穩定性
- **數據脫敏**: 敏感信息在處理過程中進行遮罩

## 📈 效能指標

- **響應時間**: < 10秒完整流程
- **並發處理**: 最多3個同時請求
- **解析準確率**: > 85%
- **系統可用性**: > 99%

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

### 🔍 項目文檔
本專案從需求分析到技術規劃的完整歷程記錄：

- 📋 **[產品需求文檔](docs/PRD.md)**: 詳細的功能需求和用戶故事
- 🏗️ **[系統架構文檔](docs/Architecture.md)**: 完整的技術架構設計
- 📊 **[階段一系統評估](docs/Stage1-System-Assessment.md)**: 專業的系統分析報告
- 🚀 **[開發歷程記錄](docs/Development-Log.md)**: 開發過程的詳細記錄

## 📄 授權

本專案採用 MIT 授權 - 詳見 [LICENSE](LICENSE) 檔案

## 📞 聯絡方式

- **作者**: minxinchen
- **專案網址**: https://github.com/minxinchen/AI-Career-Assista
- **問題回報**: [Issues](https://github.com/minxinchen/AI-Career-Assista/issues)

---

*這是一個教學專案，展示人機協作開發的完整流程*