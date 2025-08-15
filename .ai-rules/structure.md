---
title: Project Structure & Conventions
description: "Directory layout, naming conventions, module boundaries."
inclusion: always
Status: DRAFT
Spec-Version: v0
Last-Approved:
---
# AI Career Assistant - 結構與約定

## 目錄樹
```
AI-Career-Assistant/
├── .ai-rules/                 # AI 助手規則與文檔
│   ├── product.md
│   ├── tech.md
│   ├── structure.md
│   └── architecture.md
├── backend/                   # Python FastAPI 後端
│   ├── app/
│   │   ├── api/              # API 路由
│   │   ├── core/             # 核心配置
│   │   ├── models/           # 數據模型
│   │   ├── services/         # 業務邏輯
│   │   └── agents/           # AI Agent 模組
│   ├── tests/
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/                  # React/Next.js 前端
│   ├── src/
│   │   ├── components/       # UI 組件
│   │   ├── pages/           # 頁面
│   │   ├── hooks/           # React Hooks
│   │   └── utils/           # 工具函數
│   ├── public/
│   ├── package.json
│   └── Dockerfile
├── n8n/                      # n8n 工作流
│   ├── workflows/           # 工作流定義
│   ├── custom-nodes/        # 自定義節點
│   └── docker-compose.yml
├── docs/                     # 專案文檔
│   ├── PRD-Enhancement-v3.0.md
│   ├── n8n-technical-reference.md
│   └── api/                 # API 文檔
├── scripts/                  # 部署腳本
├── tests/                    # 整合測試
└── docker-compose.yml       # 整體服務編排
```

## 模組邊界
### 後端模組
- **API Layer** (`backend/app/api/`): REST API 端點，路由定義
- **Service Layer** (`backend/app/services/`): 業務邏輯處理
- **Model Layer** (`backend/app/models/`): 數據模型與 ORM
- **Agent Layer** (`backend/app/agents/`): AI Agent 邏輯封裝

### 前端模組
- **Presentation** (`frontend/src/components/`): UI 組件
- **Business Logic** (`frontend/src/hooks/`): 狀態管理與 API 調用
- **Routing** (`frontend/src/pages/`): 頁面路由

### n8n 工作流模組
- **Data Processing**: 履歷解析、格式轉換
- **AI Integration**: Gemini API 調用與結果處理
- **Notification**: 用戶通知與報告發送

## 命名規則
### 檔案命名
- **Python**: `snake_case.py` (例: `resume_analyzer.py`)
- **JavaScript/TypeScript**: `camelCase.tsx` (例: `ResumeUpload.tsx`)
- **n8n Workflows**: `kebab-case.json` (例: `resume-analysis-flow.json`)

### API 端點
- **RESTful**: `/api/v1/{resource}/{action}` 
- 例: `/api/v1/resumes/analyze`, `/api/v1/users/profile`

### 資料庫表名
- **PostgreSQL**: `snake_case` (例: `user_profiles`, `analysis_results`)

### 環境變數
- **全大寫蛇形**: `AI_CAREER_DATABASE_URL`, `GEMINI_API_KEY`

## 《建議與風險》
### 高優先級
- **模組耦合度**：確保 Agent Layer 可獨立測試與替換
- **API 版本控制**：從 v1 開始，預留向下相容機制

### 中優先級
- **檔案組織**：隨功能增加，考慮按業務領域重新組織
- **命名一致性**：建立 linting 規則自動檢查命名規範