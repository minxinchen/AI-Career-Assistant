# AI Career Assistant - API 設計文檔

## 📋 API 總覽

### Base URL
```
開發環境: http://localhost:3000/api
生產環境: https://api.ai-career-assistant.com/api
```

### 通用回應格式
```javascript
{
  "success": true,
  "data": { /* 實際數據 */ },
  "message": "操作成功",
  "timestamp": "2025-01-01T12:00:00.000Z",
  "requestId": "uuid-string"
}

// 錯誤回應
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "錯誤描述",
    "details": { /* 錯誤詳細信息 */ }
  },
  "timestamp": "2025-01-01T12:00:00.000Z",
  "requestId": "uuid-string"
}
```

## 🔐 認證與安全

### API Key 認證 (可選)
```http
Authorization: Bearer your-api-key
Content-Type: application/json
```

### 請求限制
- **上傳檔案大小**: 最大 10MB
- **請求頻率**: 每15分鐘最多10次請求
- **並發限制**: 同時最多3個處理請求

## 📤 檔案處理 API

### 1. 檔案上傳
**端點**: `POST /api/file/upload`

**請求格式**:
```http
POST /api/file/upload
Content-Type: multipart/form-data

Form Data:
- file: [二進制檔案] (必填)
- userId: string (可選，用於追蹤)
```

**成功回應**:
```javascript
{
  "success": true,
  "data": {
    "fileId": "file_abc123",
    "jobId": "job_xyz789",
    "status": "processing",
    "estimatedTime": 8
  },
  "message": "檔案上傳成功，開始處理"
}
```

**錯誤代碼**:
- `FILE_TOO_LARGE`: 檔案超過大小限制
- `UNSUPPORTED_FORMAT`: 不支援的檔案格式
- `MALICIOUS_CONTENT`: 檔案包含可疑內容
- `PROCESSING_LIMIT`: 超過並發處理限制

### 2. 處理狀態查詢
**端點**: `GET /api/processing/{jobId}`

**成功回應**:
```javascript
{
  "success": true,
  "data": {
    "jobId": "job_xyz789",
    "status": "processing", // processing, completed, failed
    "progress": 65,
    "currentStep": "job_matching",
    "estimatedTimeRemaining": 3,
    "steps": {
      "file_parsing": "completed",
      "ai_analysis": "completed", 
      "job_search": "processing",
      "recommendation": "pending"
    }
  }
}
```

### 3. 處理結果獲取
**端點**: `GET /api/result/{jobId}`

**成功回應**:
```javascript
{
  "success": true,
  "data": {
    "jobId": "job_xyz789",
    "status": "completed",
    "result": {
      "resume_analysis": { /* 履歷分析結果 */ },
      "job_recommendations": [ /* 職缺推薦列表 */ ],
      "suggestions": [ /* 改進建議 */ ]
    },
    "processedAt": "2025-01-01T12:05:30.000Z",
    "processingTime": 8.5
  }
}
```

## 🤖 AI 分析 API

### 1. 履歷分析結果
**數據結構**:
```javascript
{
  "resume_analysis": {
    "basic_info": {
      "name": "王小明",
      "email": "wang@example.com", 
      "phone": "[HIDDEN]",
      "location": "台北市"
    },
    "education": [
      {
        "degree": "學士",
        "major": "資訊工程",
        "school": "台灣大學",
        "graduationYear": 2020,
        "gpa": 3.8
      }
    ],
    "experience": [
      {
        "company": "科技公司A",
        "position": "軟體工程師",
        "duration": "2020-2023",
        "years": 3,
        "responsibilities": ["前端開發", "API設計"],
        "achievements": ["提升系統效能30%", "獲得年度最佳員工"]
      }
    ],
    "skills": {
      "technical": [
        {"name": "JavaScript", "level": "高級", "years": 3},
        {"name": "React", "level": "中級", "years": 2}
      ],
      "soft": ["團隊合作", "專案管理", "問題解決"],
      "languages": [
        {"language": "中文", "level": "母語"},
        {"language": "英文", "level": "中高級"}
      ]
    },
    "total_experience": 3,
    "career_level": "中級",
    "has_photo": true
  }
}
```

### 2. AI 洞察分析
```javascript
{
  "ai_insights": {
    "strengths": [
      {
        "category": "技術能力",
        "description": "具備完整的前端開發技能組合",
        "evidence": ["JavaScript高級程度", "React框架經驗", "實際專案經驗"]
      },
      {
        "category": "學習能力", 
        "description": "能夠快速學習新技術並應用到工作中",
        "evidence": ["短時間內掌握多項技術", "持續的技能提升軌跡"]
      }
    ],
    "areas_for_improvement": [
      {
        "category": "後端技能",
        "description": "缺乏後端開發經驗，限制了全端發展",
        "suggestions": ["學習Node.js或Python", "嘗試全端專案開發"]
      }
    ],
    "career_suggestions": [
      {
        "term": "短期 (6個月)",
        "goals": ["深化React技能", "學習TypeScript"],
        "actions": ["參與開源專案", "完成相關認證"]
      },
      {
        "term": "中期 (1-2年)",
        "goals": ["成為全端開發者", "獲得技術領導經驗"],
        "actions": ["學習後端技術", "主導小型專案"]
      }
    ],
    "salary_prediction": {
      "current_range": "60-80萬",
      "potential_range": "80-120萬", 
      "factors": ["技能提升", "經驗累積", "市場需求"]
    }
  }
}
```

## 💼 職缺推薦 API

### 1. 職缺推薦結果
```javascript
{
  "job_recommendations": {
    "skill_matched": [
      {
        "id": "job_001",
        "title": "前端工程師",
        "company": "創新科技股份有限公司",
        "location": "台北市信義區",
        "salary": {
          "min": 700000,
          "max": 1000000,
          "currency": "TWD",
          "period": "年薪"
        },
        "requirements": [
          "JavaScript 3年以上經驗",
          "React 框架熟練",
          "響應式網頁設計"
        ],
        "match_score": 92,
        "match_reasons": [
          "技能高度匹配 (JavaScript, React)",
          "年資符合要求 (3年)",
          "地點偏好匹配"
        ],
        "job_url": "https://www.104.com.tw/job/xxx",
        "source": "104人力銀行",
        "posted_date": "2025-01-01",
        "application_count": 45
      }
    ],
    "experience_matched": [
      {
        "id": "job_002", 
        "title": "資深軟體工程師",
        "company": "金融科技公司",
        "match_score": 78,
        "cross_domain_potential": true,
        "transition_difficulty": "中等",
        "required_skills_gap": ["金融知識", "後端開發"]
      }
    ],
    "growth_potential": [
      {
        "id": "job_003",
        "title": "產品經理",
        "company": "電商平台",
        "match_score": 65,
        "growth_reasons": [
          "技術背景有利於產品開發",
          "具備跨團隊合作經驗",
          "市場需求成長中"
        ],
        "skill_requirements": ["產品規劃", "數據分析", "使用者研究"]
      }
    ],
    "summary": {
      "total_jobs_found": 10,
      "skill_matched_count": 3,
      "experience_matched_count": 3, 
      "growth_potential_count": 4,
      "average_match_score": 81.5,
      "search_keywords": ["前端工程師", "JavaScript", "React"],
      "market_insights": {
        "demand_level": "高",
        "competition_level": "中等",
        "trending_skills": ["TypeScript", "Vue.js", "Node.js"]
      }
    }
  }
}
```

### 2. 市場分析數據
```javascript
{
  "market_analysis": {
    "industry_trends": [
      {
        "skill": "React",
        "demand_change": "+15%",
        "salary_trend": "+8%",
        "job_count": 1250
      }
    ],
    "location_analysis": {
      "台北市": {
        "job_count": 3200,
        "avg_salary": 850000,
        "competition_level": "高"
      },
      "新竹市": {
        "job_count": 890,
        "avg_salary": 900000,
        "competition_level": "中等"  
      }
    },
    "career_progression": {
      "next_level": "資深前端工程師",
      "typical_timeline": "2-3年",
      "required_skills": ["架構設計", "團隊領導", "效能優化"],
      "salary_increase": "20-40%"
    }
  }
}
```

## 🔍 職缺搜尋 API

### 1. 自定義搜尋
**端點**: `POST /api/jobs/search`

**請求參數**:
```javascript
{
  "keywords": ["前端工程師", "React"],
  "location": "台北市",
  "salary_range": {
    "min": 600000,
    "max": 1200000
  },
  "experience_level": "中級",
  "company_size": ["中型企業", "大型企業"],
  "job_type": "全職",
  "remote_work": false,
  "limit": 20
}
```

### 2. 搜尋結果
```javascript
{
  "success": true,
  "data": {
    "jobs": [ /* 職缺列表 */ ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 156,
      "hasNext": true
    },
    "filters_applied": {
      "keywords": ["前端工程師", "React"],
      "location": "台北市",
      "salary_range": {"min": 600000, "max": 1200000}
    },
    "search_meta": {
      "search_time": 2.3,
      "sources": ["104", "LinkedIn", "518", "小雞上工"],
      "cache_hit": false
    }
  }
}
```

## 📊 統計分析 API

### 1. 處理統計
**端點**: `GET /api/stats/processing`

**成功回應**:
```javascript
{
  "success": true,
  "data": {
    "daily_stats": {
      "total_uploads": 45,
      "successful_processing": 42,
      "failed_processing": 3,
      "average_processing_time": 7.8,
      "success_rate": 93.3
    },
    "current_load": {
      "active_jobs": 2,
      "queue_length": 0,
      "available_slots": 1
    },
    "performance_metrics": {
      "avg_response_time": 6.5,
      "p95_response_time": 9.2,
      "error_rate": 2.1
    }
  }
}
```

## ⚠️ 錯誤處理

### 常見錯誤代碼

| 錯誤代碼 | HTTP狀態 | 描述 | 解決方法 |
|----------|----------|------|----------|
| `FILE_TOO_LARGE` | 413 | 檔案超過10MB限制 | 壓縮檔案或選擇較小檔案 |
| `UNSUPPORTED_FORMAT` | 400 | 不支援的檔案格式 | 使用PDF或Word格式 |
| `PROCESSING_LIMIT` | 429 | 超過並發處理限制 | 稍後重試 |
| `RATE_LIMIT_EXCEEDED` | 429 | 超過請求頻率限制 | 15分鐘後重試 |
| `JOB_NOT_FOUND` | 404 | 找不到指定的處理任務 | 檢查jobId是否正確 |
| `PROCESSING_FAILED` | 500 | 處理過程中發生錯誤 | 重新上傳或聯繫支援 |
| `API_KEY_INVALID` | 401 | API密鑰無效 | 檢查API密鑰設定 |

### 錯誤回應範例
```javascript
{
  "success": false,
  "error": {
    "code": "FILE_TOO_LARGE",
    "message": "上傳的檔案大小超過10MB限制",
    "details": {
      "file_size": 12582912,
      "max_size": 10485760,
      "file_name": "resume.pdf"
    }
  },
  "timestamp": "2025-01-01T12:00:00.000Z",
  "requestId": "req_abc123"
}
```

## 🔧 開發工具

### 1. API測試
```bash
# 上傳履歷檔案
curl -X POST \
  http://localhost:3000/api/file/upload \
  -H 'Content-Type: multipart/form-data' \
  -F 'file=@/path/to/resume.pdf' \
  -F 'userId=test_user'

# 查詢處理狀態  
curl -X GET \
  http://localhost:3000/api/processing/job_xyz789

# 獲取結果
curl -X GET \
  http://localhost:3000/api/result/job_xyz789
```

### 2. SDK 支援 (計劃中)
```javascript
// Node.js SDK 範例
const CareerAssistant = require('ai-career-assistant-sdk');

const client = new CareerAssistant({
  apiKey: 'your-api-key',
  baseURL: 'https://api.ai-career-assistant.com'
});

// 上傳並分析履歷
const result = await client.analyzeResume('./resume.pdf');
console.log(result.jobRecommendations);
```

## 📝 變更日誌

### v1.0.0 (2025-01-01)
- 初始API設計
- 基礎檔案上傳功能
- 履歷分析API
- 職缺推薦API
- 錯誤處理機制

---

**API版本**: v1.0  
**最後更新**: 2025-01-01  
**API負責人**: AI Development Team