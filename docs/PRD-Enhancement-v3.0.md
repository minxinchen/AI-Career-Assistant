# AI-Career-Assistant (ACA) v3.0 PRD
## n8n + Gemini Multi-Agent 整合版

### 版本歷史
- v1.0: 基礎對話式履歷收集
- v2.0: 增強互動體驗與個人化
- **v3.0: n8n 工作流程自動化 + Gemini Multi-Agent 架構**

---

## 1. 專案概述

### 1.1 專案目標
AI-Career-Assistant v3.0 整合 n8n 工作流程自動化引擎與 Google Gemini Multi-Agent 系統，提供：
- **多媒體履歷收集**：支援語音、文檔、圖像等多種輸入方式
- **智能工作流程**：自動化履歷處理、分析、優化流程
- **專業化代理人**：每個 Agent 專注特定領域，提升處理品質
- **成本優化**：相比傳統方案降低 90% 自動化成本

### 1.2 核心價值主張
1. **全媒體履歷收集**：音頻轉錄、文檔解析、圖像識別
2. **Multi-Agent 協作**：4 個專業 Agent 分工合作
3. **自動化工作流程**：從收集到建議全程自動化
4. **可擴展架構**：基於 n8n 的模組化設計

---

## 2. 技術架構

### 2.1 系統架構圖

```
┌─────────────────────────────────────────────────────────┐
│                    前端層 (React + TS)                    │
├─────────────────────────────────────────────────────────┤
│  對話介面  │  多媒體上傳  │  履歷預覽  │  進度追蹤      │
└─────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────┐
│              中間件層 (Node.js API Gateway)               │
├─────────────────────────────────────────────────────────┤
│  認證授權  │  資料驗證  │  n8n 觸發  │  結果聚合      │
└─────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────┐
│                n8n 工作流程自動化層                       │
├─────────────────────────────────────────────────────────┤
│                    Multi-Agent 系統                     │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────│
│  │履歷收集Agent│ │內容分析Agent│ │格式化Agent  │ │職涯 │
│  │(Gemini)    │ │(Gemini)    │ │(Gemini)    │ │建議 │
│  │- 音頻轉錄   │ │- 技能抽取   │ │- 格式標準化 │ │Agent│
│  │- 文檔解析   │ │- 經歷評估   │ │- 多版本生成 │ │(Gem)│
│  │- 圖像識別   │ │- 競爭力分析 │ │- ATS相容性  │ │     │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────│
└─────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────┐
│                    資料存儲層                            │
├─────────────────────────────────────────────────────────┤
│  PostgreSQL  │  Redis Cache  │  File Storage  │  Vector DB │
└─────────────────────────────────────────────────────────┘
```

### 2.2 核心技術棧

**前端技術**
- React 18 + TypeScript
- TailwindCSS + Headless UI
- React Query (資料管理)
- Zustand (狀態管理)

**後端技術**
- Node.js + Express (API Gateway)
- n8n (工作流程自動化)
- Google Gemini (Multi-Agent AI)
- PostgreSQL (主資料庫)
- Redis (快取與會話)

**整合技術**
- n8n Webhooks (工作流程觸發)
- Google Gemini API (AI 處理)
- Socket.io (即時通訊)
- Bull Queue (任務佇列)

---

## 3. Multi-Agent 系統設計

### 3.1 Agent 架構

#### 3.1.1 履歷收集 Agent
**職責**：多媒體輸入處理與資料抽取

**n8n 工作流程**：
```
Webhook觸發 → 檔案類型判斷 → 
├─ 音頻檔 → Google Speech-to-Text → Gemini語音分析
├─ PDF/Word → 文檔解析 → Gemini文本抽取  
├─ 圖像檔 → Google Vision API → Gemini圖像理解
└─ 純文字 → 直接傳遞 → Gemini結構化處理
```

**Gemini Prompt 範例**：
```
你是履歷收集專家。請從以下輸入中抽取履歷資訊：
輸入類型：{input_type}
內容：{content}

請以JSON格式輸出：
{
  "personal_info": {...},
  "work_experience": [...],
  "education": [...],
  "skills": [...],
  "confidence_score": 0.95
}
```

#### 3.1.2 內容分析 Agent
**職責**：深度分析與智能建議

**n8n 工作流程**：
```
接收結構化資料 → 技能分類 → 經歷評估 → 
市場分析 → 競爭力評分 → 改善建議生成
```

**核心功能**：
- 技能標準化與分類
- 工作經歷完整性檢查
- 產業趨勢對照分析
- 薪資水平預測

#### 3.1.3 格式化 Agent
**職責**：履歷優化與多版本生成

**n8n 工作流程**：
```
接收分析結果 → 模板選擇 → 內容優化 → 
ATS相容性檢查 → 多版本生成 → PDF輸出
```

**輸出格式**：
- 標準履歷版本
- ATS 優化版本
- 創意產業版本
- 技術職位版本

#### 3.1.4 職涯建議 Agent
**職責**：策略規劃與發展建議

**n8n 工作流程**：
```
整合所有分析 → 職涯路徑規劃 → 技能缺口分析 → 
學習資源推薦 → 求職策略建議 → 時程規劃
```

### 3.2 Agent 協作機制

**工作流程編排**：
```
用戶輸入 → 履歷收集Agent → 內容分析Agent → 
格式化Agent → 職涯建議Agent → 結果整合 → 用戶反饋
```

**並行處理**：
- 格式化與職涯建議可並行執行
- 使用 n8n 的 Split/Merge 節點管理並行流程
- Redis 作為 Agent 間的資料交換中心

---

## 4. API 設計

### 4.1 核心 API 端點

#### 4.1.1 履歷處理 API
```typescript
// 啟動履歷處理工作流程
POST /api/v3/resume/process
{
  "input_type": "audio|document|image|text",
  "content": "base64_encoded_content | text_content",
  "user_id": "string",
  "workflow_options": {
    "priority": "high|normal|low",
    "output_formats": ["standard", "ats", "creative"],
    "include_career_advice": boolean
  }
}

Response:
{
  "workflow_id": "uuid",
  "status": "initiated",
  "estimated_completion": "2024-01-15T10:30:00Z",
  "tracking_url": "/api/v3/workflow/{workflow_id}/status"
}
```

#### 4.1.2 工作流程狀態 API
```typescript
// 查詢工作流程狀態
GET /api/v3/workflow/{workflow_id}/status

Response:
{
  "workflow_id": "uuid",
  "status": "running|completed|failed",
  "progress": {
    "collection_agent": "completed",
    "analysis_agent": "running", 
    "formatting_agent": "pending",
    "career_agent": "pending"
  },
  "current_step": "內容分析中...",
  "completion_percentage": 45,
  "estimated_remaining": "00:02:30"
}
```

#### 4.1.3 結果獲取 API
```typescript
// 獲取處理結果
GET /api/v3/workflow/{workflow_id}/results

Response:
{
  "workflow_id": "uuid",
  "results": {
    "structured_resume": {...},
    "analysis_report": {...},
    "formatted_versions": [
      {
        "type": "standard",
        "pdf_url": "string",
        "content": {...}
      }
    ],
    "career_advice": {...}
  },
  "processing_time": "00:03:45",
  "tokens_used": 2450
}
```

### 4.2 n8n Webhook 整合

#### 4.2.1 工作流程觸發
```typescript
// API Gateway 觸發 n8n 工作流程
const triggerWorkflow = async (workflowData) => {
  const response = await fetch(`${N8N_URL}/webhook/resume-processing`, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${N8N_API_KEY}`
    },
    body: JSON.stringify({
      ...workflowData,
      callback_url: `${API_BASE_URL}/api/v3/n8n/callback`,
      workflow_id: generateUUID()
    })
  });
  return response.json();
};
```

#### 4.2.2 結果回調處理
```typescript
// n8n 完成後回調
POST /api/v3/n8n/callback
{
  "workflow_id": "uuid",
  "status": "success|error",
  "results": {...},
  "error_details": "string",
  "execution_time": "00:03:45"
}
```

---

## 5. 實施計劃

### 5.1 Phase 1: 基礎整合 (4 週)
**Week 1-2: n8n 環境建置**
- [ ] n8n 服務器部署與配置
- [ ] Google Gemini API 整合
- [ ] 基礎 webhook 設定
- [ ] 資料庫 schema 調整

**Week 3-4: 核心 Agent 開發**
- [ ] 履歷收集 Agent 工作流程
- [ ] 內容分析 Agent 基礎邏輯
- [ ] API Gateway 調整
- [ ] 前端多媒體上傳介面

### 5.2 Phase 2: Multi-Agent 系統 (6 週)
**Week 5-7: Agent 完整開發**
- [ ] 4 個 Agent 完整工作流程
- [ ] Agent 間協作機制
- [ ] 並行處理優化
- [ ] 錯誤處理與重試邏輯

**Week 8-10: 整合測試**
- [ ] End-to-end 工作流程測試
- [ ] 效能優化與調校
- [ ] 使用者介面整合
- [ ] 即時狀態更新

### 5.3 Phase 3: 優化與上線 (4 週)
**Week 11-12: 效能優化**
- [ ] n8n 工作流程優化
- [ ] Gemini token 使用優化
- [ ] 快取策略實施
- [ ] 監控與告警設定

**Week 13-14: 部署與上線**
- [ ] 生產環境部署
- [ ] 使用者測試與回饋
- [ ] 文檔完善
- [ ] 營運準備

---

## 6. 成本分析

### 6.1 n8n 成本優勢
**傳統方案 vs n8n 方案**：
- 其他平台：100k 任務 ≈ $500+/月
- n8n 方案：100k 任務 ≈ $50/月
- **成本節省：90%**

### 6.2 詳細成本估算
```
服務項目              月使用量      單價        月成本
─────────────────────────────────────────────
n8n Cloud             10k workflows  $50/月      $50
Google Gemini API     1M tokens      $0.00025/token  $250  
檔案存儲              100GB          $0.02/GB    $2
PostgreSQL 託管       小型實例       $25/月      $25
Redis 託管            小型實例       $15/月      $15
─────────────────────────────────────────────
總計                                             $342/月
```

**ROI 分析**：
- 傳統人工處理：每份履歷 30 分鐘 × $20/小時 = $10/份
- AI 自動化處理：每份履歷成本約 $0.34
- **成本節省：96.6%**

---

## 7. 技術風險與緩解

### 7.1 主要風險
1. **n8n 服務穩定性**
   - 緩解：設置備援機制與健康檢查
   - 監控：99.9% uptime 目標

2. **Gemini API 限制**
   - 緩解：實施智能重試與降級機制
   - 監控：token 使用量追蹤

3. **工作流程複雜性**
   - 緩解：模組化設計與充分測試
   - 監控：執行時間與成功率追蹤

### 7.2 監控策略
```typescript
// 工作流程監控
const monitorWorkflow = {
  execution_time: "< 5 minutes",
  success_rate: "> 95%",
  token_efficiency: "< 1000 tokens/resume",
  cost_per_resume: "< $0.50"
};
```

---

## 8. 成功指標

### 8.1 技術指標
- 履歷處理成功率：> 95%
- 平均處理時間：< 3 分鐘
- 系統可用性：> 99.9%
- Token 效率：< 1000 tokens/份履歷

### 8.2 業務指標
- 用戶滿意度：> 4.5/5
- 履歷品質提升：> 30%
- 處理成本降低：> 90%
- 新功能採用率：> 70%

### 8.3 使用者體驗指標
- 多媒體上傳成功率：> 98%
- 即時狀態更新延遲：< 2 秒
- 結果生成準確度：> 92%
- 介面回應時間：< 1 秒

---

## 9. 後續發展

### 9.1 v3.1 計劃功能
- AI 面試練習 Agent
- 求職市場即時分析
- 個人品牌建議 Agent
- LinkedIn 自動化整合

### 9.2 v4.0 願景
- 完整職涯生態系統
- 企業端招聘整合
- AI 職涯導師系統
- 全球化多語言支援

---

*最後更新：2025-01-15*
*文檔版本：v3.0*
*作者：AI-Career-Assistant 開發團隊*