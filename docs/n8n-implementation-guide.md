# n8n + Gemini 整合實施指南
**AI-Career-Assistant v3.0**

---

## 快速開始

### 1. 環境準備

#### 1.1 安裝 n8n
```bash
# 全域安裝 n8n
npm install n8n -g

# 或使用 Docker
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

#### 1.2 設定環境變數
```bash
# Google Gemini API 設定
export GOOGLE_APPLICATION_CREDENTIALS="path/to/service-account.json"
export GOOGLE_GEMINI_API_KEY="your_gemini_api_key"

# n8n 基本認證
export N8N_BASIC_AUTH_ACTIVE=true
export N8N_BASIC_AUTH_USER=admin
export N8N_BASIC_AUTH_PASSWORD=your_secure_password

# Webhook 設定
export N8N_HOST=localhost
export N8N_PORT=5678
export N8N_PROTOCOL=http

# 生產環境額外設定
export N8N_ENCRYPTION_KEY="your_32_character_encryption_key"
export DB_TYPE=postgresdb
export DB_POSTGRESDB_HOST=localhost
export DB_POSTGRESDB_PORT=5432
export DB_POSTGRESDB_DATABASE=n8n
export DB_POSTGRESDB_USER=n8n_user
export DB_POSTGRESDB_PASSWORD=n8n_password
```

#### 1.3 啟動 n8n
```bash
# 開發環境
n8n start

# 生產環境
n8n start --tunnel
```

### 2. 工作流程導入

#### 2.1 導入配置文件
1. 開啟 n8n UI：http://localhost:5678
2. 點擊左側選單「Workflows」
3. 點擊「Import from File」
4. 選擇 `n8n-workflow-config.json`
5. 確認導入成功

#### 2.2 設定 Google Gemini 認證
1. 在工作流程中選擇任一 Gemini 節點
2. 點擊「Create New Credential」
3. 選擇「Google AI (Gemini)」
4. 輸入 API Key：從 Google AI Studio 獲取
5. 測試連接確認正常

#### 2.3 設定 Webhook 端點
1. 選擇「Resume Input Webhook」節點
2. 複製 Webhook URL
3. 將 URL 配置到 API Gateway 中

### 3. API Gateway 整合

#### 3.1 觸發工作流程
```typescript
// 安裝依賴
npm install axios

// API Gateway 整合代碼
import axios from 'axios';

class N8nWorkflowService {
  private n8nBaseUrl = process.env.N8N_URL || 'http://localhost:5678';
  private webhookPath = '/webhook/resume-processing';

  async processResume(data: ResumeProcessingRequest): Promise<WorkflowResponse> {
    try {
      const response = await axios.post(
        `${this.n8nBaseUrl}${this.webhookPath}`,
        {
          ...data,
          workflow_id: this.generateWorkflowId(),
          callback_url: `${process.env.API_BASE_URL}/api/v3/n8n/callback`,
          timestamp: new Date().toISOString()
        },
        {
          headers: {
            'Content-Type': 'application/json',
          },
          timeout: 10000 // 10 秒超時
        }
      );

      return {
        workflow_id: response.data.workflow_id,
        status: 'initiated',
        message: '履歷處理已開始'
      };
    } catch (error) {
      throw new Error(`n8n 工作流程觸發失敗: ${error.message}`);
    }
  }

  private generateWorkflowId(): string {
    return `aca-${Date.now()}-${Math.random().toString(36).substr(2, 9)}`;
  }
}

// 使用範例
const workflowService = new N8nWorkflowService();

// 處理履歷
const result = await workflowService.processResume({
  input_type: 'document',
  content: 'base64_encoded_pdf_content',
  user_id: 'user_123',
  workflow_options: {
    priority: 'high',
    output_formats: ['standard', 'ats'],
    include_career_advice: true
  }
});
```

#### 3.2 回調處理
```typescript
// Express.js 回調端點
app.post('/api/v3/n8n/callback', async (req, res) => {
  try {
    const { workflow_id, status, results, error_details } = req.body;

    if (status === 'success') {
      // 儲存處理結果
      await saveWorkflowResults(workflow_id, results);
      
      // 通知前端
      io.to(workflow_id).emit('workflow_completed', {
        workflow_id,
        results,
        processing_time: results.processing_metadata?.execution_time
      });
    } else {
      // 處理錯誤
      await handleWorkflowError(workflow_id, error_details);
      
      // 通知前端錯誤
      io.to(workflow_id).emit('workflow_error', {
        workflow_id,
        error: error_details
      });
    }

    res.status(200).json({ received: true });
  } catch (error) {
    console.error('回調處理錯誤:', error);
    res.status(500).json({ error: 'Internal server error' });
  }
});
```

---

## 成本效益分析

### 傳統方案 vs n8n 方案

| 項目 | 傳統方案 | n8n 方案 | 節省比例 |
|------|----------|----------|----------|
| **處理時間** | 30 分鐘/份 | 3 分鐘/份 | 90% |
| **人力成本** | $10/份 | $0.34/份 | 96.6% |
| **準確性** | 95% (人工錯誤) | 98% (AI 一致性) | +3% |
| **可擴展性** | 線性成長 | 平行處理 | 無限 |
| **24/7 可用性** | 否 | 是 | 100% |

### ROI 計算範例
```
假設條件：
- 月處理量：1,000 份履歷
- 平均人工時薪：$20/小時
- 人工處理時間：30 分鐘/份

傳統成本：
1,000 份 × 0.5 小時 × $20 = $10,000/月

n8n 成本：
- n8n Cloud: $50/月
- Gemini API: $250/月 (1M tokens)
- 基礎設施: $42/月
- 總計: $342/月

月節省：$10,000 - $342 = $9,658
年節省：$9,658 × 12 = $115,896
ROI: 2,823%
```

---

## 監控與優化

### 關鍵效能指標 (KPIs)

#### 技術指標
```yaml
Success Rate: > 95%
  - 工作流程完成率
  - API 回應成功率
  - 資料處理準確率

Performance:
  - 平均處理時間: < 3 分鐘
  - API 回應時間: < 2 秒
  - 系統可用性: > 99.9%

Resource Usage:
  - Token 使用效率: < 1000 tokens/份
  - 記憶體使用: < 512MB/workflow
  - CPU 使用率: < 80%
```

#### 業務指標
```yaml
Quality Metrics:
  - 履歷完整度: > 90%
  - 用戶滿意度: > 4.5/5
  - 錯誤率: < 2%

Cost Efficiency:
  - 成本每份履歷: < $0.50
  - ROI: > 2000%
  - 處理速度提升: > 900%
```

### 監控設置

#### 1. n8n 內建監控
```javascript
// 工作流程執行監控
const monitorExecution = {
  execution_time: "< 5 minutes",
  success_rate: "> 95%",
  error_rate: "< 5%",
  retry_count: "< 3"
};

// 設定告警
const alertRules = {
  high_failure_rate: {
    threshold: 10, // 10% 失敗率
    action: "send_notification"
  },
  slow_execution: {
    threshold: 300, // 5 分鐘
    action: "scale_resources"
  }
};
```

#### 2. 外部監控工具
```yaml
# Prometheus 設定
- job_name: 'n8n'
  static_configs:
    - targets: ['localhost:5678']
  metrics_path: /metrics
  scrape_interval: 30s

# Grafana 儀表板
panels:
  - workflow_success_rate
  - execution_time_distribution
  - token_usage_trend
  - error_rate_by_type
```

### 效能調校指南

#### 1. Gemini Prompt 優化
```javascript
// ❌ 低效 Prompt
const inefficientPrompt = `
請詳細分析這份履歷，包含每個細節，
並提供非常詳盡的建議，包括格式、內容、
策略等各方面的完整說明...
`;

// ✅ 高效 Prompt
const efficientPrompt = `
分析履歷資料：{{resume_data}}

輸出JSON格式：
{
  "skills": {"technical": [], "soft": []},
  "experience_score": 1-10,
  "improvements": ["具體建議1", "具體建議2"]
}
`;
```

#### 2. 並行處理優化
```json
{
  "parallel_execution": {
    "formatting_agent": "可與 career_agent 並行",
    "analysis_agent": "必須在 collection_agent 之後",
    "max_concurrent": 3
  },
  "resource_allocation": {
    "memory_per_node": "256MB",
    "timeout_per_node": "120s",
    "retry_attempts": 2
  }
}
```

#### 3. 快取策略
```typescript
// Redis 快取設定
const cacheStrategy = {
  // 相似履歷內容快取
  similar_content: {
    ttl: 3600, // 1 小時
    key_pattern: "resume_analysis:{content_hash}"
  },
  
  // 技能分析快取
  skill_analysis: {
    ttl: 86400, // 24 小時
    key_pattern: "skill_category:{skill_hash}"
  },
  
  // 市場趨勢快取
  market_trends: {
    ttl: 604800, // 7 天
    key_pattern: "market_trend:{industry}:{role}"
  }
};
```

---

## 部署檢查清單

### Phase 1: 基礎設置 ✅

#### 開發環境
- [ ] n8n 本地安裝與設定
- [ ] Google Gemini API 金鑰申請
- [ ] 工作流程導入與測試
- [ ] 基本 webhook 功能驗證

#### 測試環境
- [ ] 測試資料庫設置
- [ ] API Gateway 整合測試
- [ ] 端到端流程測試
- [ ] 錯誤處理機制測試

### Phase 2: 整合測試 ✅

#### 功能測試
- [ ] 多媒體輸入測試（音頻、文檔、圖像）
- [ ] Multi-Agent 協作測試
- [ ] 並行處理效能測試
- [ ] 回調機制測試

#### 效能測試
- [ ] 負載測試（100 並發）
- [ ] 壓力測試（峰值負載）
- [ ] 記憶體洩漏檢查
- [ ] Token 使用量優化

### Phase 3: 生產部署 ✅

#### 安全性檢查
- [ ] API 金鑰安全存儲
- [ ] HTTPS 強制實施
- [ ] 輸入資料驗證
- [ ] 存取權限控制

#### 維運準備
- [ ] 監控告警設置
- [ ] 備份與災難恢復
- [ ] 文檔完善
- [ ] 團隊培訓

#### 上線驗證
- [ ] 健康檢查端點
- [ ] 灰度發布測試
- [ ] 使用者驗收測試
- [ ] 效能基準確認

---

## 故障排除

### 常見問題

#### 1. Gemini API 配額超限
```
問題：HTTP 429 - Rate limit exceeded
解決方案：
1. 檢查 API 配額使用情況
2. 實施指數退避重試
3. 考慮升級 API 方案
4. 優化 token 使用量
```

#### 2. 工作流程執行緩慢
```
問題：處理時間超過 5 分鐘
解決方案：
1. 檢查 Gemini 節點配置
2. 優化 prompt 長度
3. 增加並行處理
4. 檢查網路延遲
```

#### 3. 回調失敗
```
問題：n8n 回調無法到達 API Gateway
解決方案：
1. 檢查 callback_url 正確性
2. 確認防火牆設定
3. 驗證 webhook 端點
4. 檢查 SSL 憑證
```

### 除錯指令
```bash
# 檢查 n8n 狀態
curl http://localhost:5678/healthz

# 檢查工作流程執行歷史
n8n list executions --workflow="ACA-Resume-Processing-Workflow"

# 檢查日誌
docker logs n8n-container --tail=100

# 測試 webhook
curl -X POST http://localhost:5678/webhook/resume-processing \
  -H "Content-Type: application/json" \
  -d '{"test": true}'
```

---

## 支援與聯絡

### 技術支援
- **Email**: tech-support@aca.com
- **文檔**: https://docs.aca.com/n8n-integration
- **GitHub**: https://github.com/aca/n8n-workflows

### 更新資訊
- **文檔版本**: v3.0
- **最後更新**: 2025-01-15
- **下次檢查**: 2025-02-15

---

*此指南將隨著系統發展持續更新，請定期檢查最新版本。*