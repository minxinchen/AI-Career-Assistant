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
├── docs/                    # 專案文檔
│   ├── PRD.md              # 產品需求文檔
│   ├── API-Design.md       # API設計文檔
│   ├── Architecture.md     # 系統架構文檔
│   └── Development-Log.md  # 開發歷程記錄
├── frontend/               # 前端應用
│   ├── src/
│   ├── public/
│   └── package.json
├── backend/                # 後端服務
│   ├── src/
│   ├── config/
│   └── package.json
├── ai-services/            # AI分析服務
│   ├── resume-parser/
│   ├── job-matcher/
│   └── requirements.txt
├── scripts/                # 部署腳本
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

## 📝 開發歷程

本專案從需求分析到技術規劃的完整歷程記錄在 [Development-Log.md](docs/Development-Log.md) 中，包括：

- 用戶需求收集與分析
- 技術選型決策過程  
- 系統架構設計演進
- 風險評估與應對策略
- 實施計劃制定

## 📄 授權

本專案採用 MIT 授權 - 詳見 [LICENSE](LICENSE) 檔案

## 📞 聯絡方式

- **作者**: minxinchen
- **專案網址**: https://github.com/minxinchen/AI-Career-Assista
- **問題回報**: [Issues](https://github.com/minxinchen/AI-Career-Assista/issues)

---

*這是一個教學專案，展示人機協作開發的完整流程*