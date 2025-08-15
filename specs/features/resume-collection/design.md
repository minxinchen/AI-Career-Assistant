# 履歷收集模組架構設計
> **版本**: v1.0  
> **基於**: ACA 現有架構分析  
> **模組類型**: 獨立功能模組

## 整體架構

### 模組邊界
```
ACA 主系統
├── Core (核心，不變)
├── SkillAnalysis (現有模組)
├── ResumeCollection (新增模組) ← 本設計
└── Future Modules (履歷格式化、求職指導等)
```

### 三層架構對應
```
Components/
├── ResumeWizard.js (主要對話元件)
├── SensitiveTopicHandler.js (敏感話題處理)
├── ProgressTracker.js (進度追蹤)
└── DataReviewPanel.js (資料檢視)

Services/
├── ResumeCollectionService.js (核心邏輯)
├── ConversationEngine.js (對話流程控制)
├── SensitivityDetector.js (敏感內容檢測)
└── DataNormalizer.js (資料標準化)

Utils/
├── QuestionBank.js (問題庫)
├── ValidationRules.js (驗證規則)
└── SensitiveKeywords.js (敏感詞庫)
```

## 核心元件設計

### 1. ResumeCollectionService (主服務)
```javascript
class ResumeCollectionService {
  constructor() {
    this.conversationEngine = new ConversationEngine();
    this.sensitivityDetector = new SensitivityDetector();
    this.dataNormalizer = new DataNormalizer();
  }

  async startCollection(config = {}) {
    // 初始化收集流程
  }

  async processResponse(questionId, response) {
    // 處理用戶回應，包含敏感檢測
  }

  exportData() {
    // 輸出標準化 JSON
  }
}
```

### 2. ConversationEngine (對話引擎)
```javascript
class ConversationEngine {
  constructor() {
    this.questionBank = new QuestionBank();
    this.currentPath = [];
    this.userProfile = {};
  }

  getNextQuestion(context) {
    // 根據上下文動態選擇下一個問題
  }

  handleSensitiveResponse(response) {
    // 敏感回應的特殊處理邏輯
  }
}
```

### 3. SensitivityDetector (敏感檢測器)
```javascript
class SensitivityDetector {
  constructor() {
    this.keywords = SensitiveKeywords.load();
    this.patterns = this.initializePatterns();
  }

  analyze(text) {
    return {
      isSensitive: boolean,
      category: string, // 'unemployment', 'health', 'trauma', etc.
      confidence: number,
      suggestedResponse: string
    };
  }
}
```

## 模組介面設計

### 1. 與主系統整合
```javascript
// 主系統註冊模組
ModuleRegistry.register('resumeCollection', {
  name: 'Resume Collection',
  version: '1.0.0',
  dependencies: [], // 無依賴，完全獨立
  exports: ['ResumeCollectionService'],
  permissions: ['localStorage', 'userInput']
});

// 主系統呼叫
const resumeService = ModuleRegistry.get('resumeCollection');
const result = await resumeService.collectResume(config);
```

### 2. 與技能分析模組整合
```javascript
// 標準化資料交換格式
const resumeData = {
  personalInfo: {...},
  experience: [...],
  skills: [...], // ← 傳給技能分析模組
  education: [...],
  metadata: {
    collectionDate: string,
    sensitiveFlags: boolean,
    completeness: number
  }
};
```

### 3. 未來模組擴展介面
```javascript
// 預留介面
interface ResumeProcessor {
  process(resumeData: ResumeData): Promise<ProcessedResume>;
}

// 履歷格式化模組
class ResumeFormatter implements ResumeProcessor {
  async process(resumeData) {
    // 格式化為不同模板
  }
}

// 求職指導模組
class CareerAdvisor implements ResumeProcessor {
  async process(resumeData) {
    // 基於履歷提供建議
  }
}
```

## 敏感話題處理架構

### 處理流程
```
用戶輸入
    ↓
敏感檢測 → [是] → 同理回應生成
    ↓                    ↓
   [否]              提供選項/跳過
    ↓                    ↓
標準流程 ←────────────────┘
```

### 敏感詞庫結構
```javascript
const sensitiveCategories = {
  unemployment: {
    keywords: ['被解雇', '失業', '裁員', '資遣'],
    responses: ['這確實是一個挑戰...'],
    alternatives: ['職涯轉換期', '自我探索階段']
  },
  health: {
    keywords: ['生病', '憂鬱', '焦慮', '治療'],
    responses: ['健康是最重要的...'],
    alternatives: ['個人因素', '健康調養']
  }
  // ... 更多類別
};
```

## 資料流設計

### 收集階段資料流
```
用戶 → ResumeWizard → ConversationEngine → SensitivityDetector
                           ↓
     DataNormalizer ← ResumeCollectionService
                           ↓
                    localStorage (暫存)
```

### 輸出階段資料流
```
localStorage → DataNormalizer → 標準化 JSON → 其他模組
```

## 配置與客製化

### 模組配置
```javascript
const moduleConfig = {
  features: {
    sensitiveDetection: true,
    skipOptions: true,
    pauseResume: true
  },
  ui: {
    theme: 'empathetic',
    progressBar: true,
    estimatedTime: true
  },
  data: {
    autoSave: true,
    encryption: false, // 本地不加密
    retention: '30days'
  }
};
```

### 問題庫客製化
```javascript
// 支援動態添加問題類型
QuestionBank.addCategory('freelance', {
  questions: [...],
  sensitiveTopics: [...],
  validationRules: [...]
});
```

## 效能與最佳化

### 載入策略
- 模組按需載入（Lazy Loading）
- 問題庫分段載入
- 敏感詞庫快取

### 記憶體管理
- 完成收集後清理暫存資料
- 大型資料分頁處理
- 避免記憶體洩漏

## 測試策略

### 單元測試
- 各個 Service 獨立測試
- 敏感檢測精準度測試
- 資料驗證測試

### 整合測試
- 與主系統整合測試
- 模組啟用/停用測試
- 資料流測試

### 用戶體驗測試
- 敏感話題處理情境測試
- 不同用戶路徑測試
- 無障礙功能測試