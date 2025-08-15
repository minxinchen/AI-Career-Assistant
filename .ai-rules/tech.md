---
title: Technology Stack
description: "Tech stacks, services, runtimes, frameworks, build/test commands."
inclusion: always
Status: DRAFT
Spec-Version: v0
Last-Approved:
---
# AI Career Assistant - 技術棧

## 語言/框架
- **後端**：Python 3.11+ (FastAPI/Django)
- **前端**：React 18+ / Next.js 14+ (TypeScript)
- **工作流引擎**：n8n (Node.js)
- **AI 整合**：Google Gemini API, LangChain
- **容器化**：Docker + Docker Compose

## 依賴（主要套件）
### Python 後端
```
fastapi>=0.104.0
uvicorn>=0.24.0
pydantic>=2.5.0
sqlalchemy>=2.0.0
alembic>=1.13.0
google-generativeai>=0.3.0
langchain>=0.1.0
python-multipart>=0.0.6
python-jose>=3.3.0
bcrypt>=4.1.0
```

### Node.js (n8n)
```
n8n>=1.15.0
@n8n/nodes-base>=1.15.0
axios>=1.6.0
```

### 前端 (React/Next.js)
```
next>=14.0.0
react>=18.0.0
typescript>=5.0.0
tailwindcss>=3.3.0
@headlessui/react>=1.7.0
axios>=1.6.0
react-hook-form>=7.48.0
```

## 建置/測試命令
```bash
# 後端
pip install -r requirements.txt
pytest tests/
uvicorn main:app --reload

# 前端
npm install
npm run build
npm run test
npm run dev

# n8n
docker-compose up n8n
npm run start:n8n

# 整體部署
docker-compose up --build
make test-all
```

## 外部服務/第三方
- **AI 服務**：Google Gemini Pro API
- **資料庫**：PostgreSQL 15+ (主要), Redis (快取)
- **檔案存儲**：AWS S3 / Google Cloud Storage
- **監控**：Prometheus + Grafana
- **日誌**：ELK Stack (Elasticsearch, Logstash, Kibana)
- **認證**：OAuth 2.0 (Google, LinkedIn)

## 《建議與風險》
### 高優先級
- **API 限額管理**：Gemini API 有 RPM 限制，需實作 rate limiting
- **數據庫效能**：大量履歷分析需要查詢優化

### 中優先級
- **版本相容性**：定期更新依賴並測試相容性
- **開發環境一致性**：使用 Docker 確保環境一致