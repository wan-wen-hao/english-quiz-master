# 英语全能刷题王 - 语法优先的英语刷题工具

> English Quiz Master — 一个开源、零依赖、可直接部署到 GitHub Pages 的英语刷题工具。
> 覆盖 **初中 / 高中 / 四级 / 六级** 四个等级，共 **120 道精选题目**，以**语法结构、句型与特殊用法**为分类主线，词汇自然融入语法语境。
> v3.0.0 新增：每题**词汇解析（vocabulary）**、**全句中文翻译（sentenceTranslation）**及**阅读理解题型（passage）**。

本项目自带一份结构化题库 `data/quiz-bank.json`，可直接被任意前端项目加载，也可作为独立数据源用于教学、自测或二次开发。

---

## 设计理念：语法优先（Grammar-First）

本题库 **v2.0** 起采用"语法优先"分类法，取代旧版"词汇/语法/翻译"的分类方式。原因如下：

- **零基础学习者**最需要掌握的是**句法骨架**（be 动词、时态、从句、倒装等），而非孤立背单词。
- 词汇应**在语法语境中自然习得**：一道考查被动语态的题目会用到各种动词，但测试的是被动结构本身，而非动词词义。
- 每道题的解析都**讲解语法规则**，而不是单纯翻译单词含义。

> 简言之：**学语法结构 → 词汇自然出现 → 句型触类旁通**。

### v3.0.0 新增功能

在 v2.0 语法优先分类的基础上，v3.0.0 进行了两项重大增强：

1. **词汇解析（vocabulary）+ 全句翻译（sentenceTranslation）**：每道题都新增 `vocabulary` 字段（2-5 个核心词汇，含词性 pos 与中文 meaning）和 `sentenceTranslation` 字段（英文句子的完整中文翻译），帮助学习者在语法语境中精确定位关键词汇。
2. **阅读理解题型（passage）**：每个等级新增 3 道 passage 题，含短文（passage）、中文翻译（passageCn）、词汇列表（vocabulary）和 2-3 道子题（subQuestions），测试在语篇中的语法结构理解能力。

---

## 目录结构

```
english-quiz-master/
├── README.md              # 项目说明（本文件）
├── data/
│   └── quiz-bank.json     # 核心题库（120 题，4 个等级，按语法结构分类）
└── docs/
    └── guide.md           # 中文使用指南（含分类体系详解）
```

---

## 题库概览

题库文件：`data/quiz-bank.json`

| 等级 key | 中文名 | 前缀 | 题目数 | 语法分类主线 |
|----------|--------|------|--------|--------------|
| `junior` | 初中   | `j_` | 30 | be动词、一般现在时、现在进行时、一般过去时、there be句型、介词、疑问句、可数不可数名词、代词、常用句型 |
| `senior` | 高中   | `s_` | 30 | 定语从句、名词性从句、非谓语动词、时态综合、被动语态、虚拟语气、倒装与强调、情态动词 |
| `cet4`   | 四级   | `c4_`| 30 | 从句综合运用、非谓语进阶、虚拟进阶、倒装综合、固定搭配与介词、长难句结构分析、时态语态综合、特殊句式 |
| `cet6`   | 六级   | `c6_`| 30 | 复杂从句结构、非谓语高级用法、虚拟高阶、倒装与省略综合、学术写作句式、语法歧义与辨析、高级固定结构、翻译与句型转换 |

**每个等级 30 题，题型分布一致（v3.0.0 更新）：**

- `choice`（选择题）：10 题 — 四个选项 A/B/C/D，类似科一驾考
- `truefalse`（判断题）：6 题 — true/false 判断
- `fillblank`（填空题）：6 题
- `qa`（问答题/翻译题）：5 题
- `passage`（阅读理解题）：3 题 — 含短文及 2-3 道子题

题目在各等级内由浅入深排列；每个等级内部先按题型分块（选择→判断→填空→问答→阅读），各题型块内再按语法类别递进。

---

## 题目数据结构

每道题目都是一个 JSON 对象。不同题型字段略有差异：

### 选择题 (choice)
```json
{
  "id": "j_001",
  "type": "choice",
  "category": "be动词与主谓一致",
  "question": "Choose the correct form: She ___ a teacher in our school.",
  "questionCn": "选择正确形式：她是我们学校的一名老师。",
  "choices": ["A. am", "B. is", "C. are", "D. be"],
  "answer": "B",
  "explanation": "主语she是第三人称单数，be动词用is。be动词随主语变化：I用am，he/she/it用is，we/you/they用are。",
  "knowledgePoint": "be动词：主语为第三人称单数时用is",
  "vocabulary": [
    {"word": "teacher", "pos": "n.", "meaning": "老师"},
    {"word": "school", "pos": "n.", "meaning": "学校"},
    {"word": "she", "pos": "pron.", "meaning": "她"}
  ],
  "sentenceTranslation": "她是我们学校的一名老师。"
}
```

### 判断题 (truefalse)
```json
{
  "id": "j_014",
  "type": "truefalse",
  "category": "一般现在时",
  "question": "Judge true or false: He don't like playing football on weekends.",
  "questionCn": "判断对错：他周末不喜欢踢足球。",
  "answer": "false",
  "explanation": "错误。主语he是第三人称单数，否定句用doesn't+动词原形...",
  "knowledgePoint": "一般现在时：第三人称单数否定形式doesn't+动词原形",
  "vocabulary": [
    {"word": "football", "pos": "n.", "meaning": "足球"},
    {"word": "weekend", "pos": "n.", "meaning": "周末"}
  ],
  "sentenceTranslation": "他周末不喜欢踢足球。"
}
```

### 填空题 (fillblank)
```json
{
  "id": "j_022",
  "type": "fillblank",
  "category": "there be句型",
  "question": "Fill in the blank: There ___ two books and a pen on the desk.",
  "questionCn": "填空：桌子上有两本书和一支笔。",
  "answer": "are",
  "explanation": "there be句型遵循就近原则：be动词与最近的主语保持一致...",
  "knowledgePoint": "there be句型：就近原则判断be动词形式",
  "vocabulary": [
    {"word": "desk", "pos": "n.", "meaning": "桌子"},
    {"word": "pen", "pos": "n.", "meaning": "钢笔"}
  ],
  "sentenceTranslation": "桌子上有两本书和一支笔。"
}
```

### 问答题/翻译题 (qa)
```json
{
  "id": "j_025",
  "type": "qa",
  "category": "一般现在时",
  "question": "Translate into English: 他每天早上六点起床。",
  "questionCn": "将中文翻译成英文。",
  "answer": "He gets up at six every morning.",
  "explanation": "一般现在时表示习惯性动作。主语he是第三人称单数，动词get up需变化：get→gets...",
  "knowledgePoint": "一般现在时：第三人称单数动词变化(get→gets)+频率/时间状语",
  "vocabulary": [
    {"word": "get up", "pos": "phr.", "meaning": "起床"},
    {"word": "morning", "pos": "n.", "meaning": "早上"}
  ],
  "sentenceTranslation": "他每天早上六点起床。"
}
```

### 阅读理解题 (passage) — v3.0.0 新增
```json
{
  "id": "j_p01",
  "type": "passage",
  "category": "there be句型",
  "passage": "This is my room. There is a big bed near the window...",
  "passageCn": "这是我的房间。窗户旁边有一张大床...",
  "vocabulary": [
    {"word": "room", "pos": "n.", "meaning": "房间"},
    {"word": "window", "pos": "n.", "meaning": "窗户"},
    {"word": "cozy", "pos": "adj.", "meaning": "舒适的"}
  ],
  "subQuestions": [
    {
      "subType": "choice",
      "question": "What is near the window?",
      "questionCn": "窗户旁边有什么？",
      "choices": ["A. A small table", "B. A big bed", "C. A shelf", "D. A lamp"],
      "answer": "B",
      "explanation": "原文：'There is a big bed near the window'...",
      "knowledgePoint": "there be句型 + 方位介词near",
      "vocabulary": [{"word": "near", "pos": "prep.", "meaning": "在...旁边"}],
      "sentenceTranslation": "窗户旁边有一张大床。"
    },
    {
      "subType": "truefalse",
      "question": "True or False: There are no books in the room.",
      "questionCn": "判断：房间里没有书。",
      "answer": "false",
      "explanation": "错误。原文说'There are some books on the shelf'...",
      "knowledgePoint": "there be句型：复数形式are + 细节理解",
      "vocabulary": [{"word": "shelf", "pos": "n.", "meaning": "书架"}],
      "sentenceTranslation": "书架上有一些书。"
    }
  ]
}
```

### 字段说明

| 字段 | 适用题型 | 说明 |
|------|----------|------|
| `id` | 全部 | 全局唯一，等级前缀 + 序号，如 `j_001`、`c6_030`、`j_p01`（passage 题） |
| `type` | 全部 | `choice` / `truefalse` / `fillblank` / `qa` / `passage` |
| `category` | 全部 | **语法结构分类**（如"定语从句""虚拟语气"），非词汇分类 |
| `question` | 全部（passage 除外） | 英文题干 |
| `questionCn` | 全部（passage 除外） | 中文翻译/释义 |
| `choices` | choice | 四个选项数组（A/B/C/D） |
| `answer` | 全部（passage 除外） | 参考答案：choice 为字母；truefalse 为 `true`/`false`；fillblank/qa 为文本 |
| `explanation` | 全部（passage 除外） | 详细解析（中英混合，**讲解语法规则**，教学导向） |
| `knowledgePoint` | 全部（passage 除外） | 对应语法知识点 |
| `vocabulary` | 全部 | **v3.0.0 新增**。核心词汇数组，每项含 `word`（单词）、`pos`（词性）、`meaning`（中文释义），2-5 个 |
| `sentenceTranslation` | 全部（passage 除外） | **v3.0.0 新增**。英文句子/题干的完整中文翻译 |
| `passage` | passage | 英文短文（3-6 句） |
| `passageCn` | passage | 短文完整中文翻译 |
| `subQuestions` | passage | 子题数组（2-3 道），每道含 `subType`（`choice`/`truefalse`）、`question`、`questionCn`、`choices`/`answer`、`explanation`、`knowledgePoint`、`vocabulary`、`sentenceTranslation` |

> 注：`fillblank` / `qa` 的 `answer` 为参考答案，主观题可接受多种合理表述。
> v3.0.0 新增的 `vocabulary` 和 `sentenceTranslation` 适用于所有非 passage 题型及 passage 的子题。

---

## 功能特性

- **语法优先分类**：以语法结构、句型与特殊用法为主线，词汇在语境中自然习得。
- **四级全覆盖**：初中 → 高中 → 四级 → 六级，一站式备考。
- **五类题型**：选择题、判断题、填空题、问答题/翻译题、阅读理解题（v3.0.0 新增），训练维度全面。
- **词汇解析**：v3.0.0 新增，每题附带 2-5 个核心词汇（含词性与中文释义）。
- **全句翻译**：v3.0.0 新增，每题附带英文句子的完整中文翻译。
- **中英对照**：每题都带中文题干/释义，便于理解与精读。
- **规则导向解析**：每题解析讲解语法规则本身，而非翻译单词。
- **阅读理解**：v3.0.0 新增 passage 题型，短文+子题，测试语篇中的语法结构理解。
- **难度递进**：各等级内题目由易到难排列，适合循序刷题。
- **纯数据驱动**：题库为单一 JSON 文件，无任何运行时依赖，易于集成。
- **静态部署友好**：天然适配 GitHub Pages，无需后端服务。

---

## 如何使用

### 方式一：直接加载题库 JSON

在你的网页/项目中通过 `fetch` 加载题库即可：

```js
const res = await fetch('data/quiz-bank.json');
const bank = await res.json();

// 取初中全部题目
const juniorQuestions = bank.levels.junior.questions;

// 按语法分类筛选（如只做"定语从句"）
const relativeClauses = bank.levels.senior.questions
  .filter(q => q.category === '定语从句');

// 遍历所有等级
Object.values(bank.levels).forEach(level => {
  console.log(level.name, level.questionCount, level.questions.length);
});
```

### 方式二：部署到 GitHub Pages

1. 将本仓库推送到 GitHub。
2. 进入仓库 **Settings → Pages**。
3. 在 **Build and deployment** 中选择部署来源：
   - **Deploy from a branch**
   - Branch：`main`，文件夹：`/root`（或 `/docs`，视你的静态站点放置位置而定）
4. 保存后等待约 1 分钟，GitHub 会给出形如 `https://<用户名>.github.io/<仓库名>/` 的访问地址。
5. 你的静态页面即可通过 `fetch('data/quiz-bank.json')` 读取题库。

> 提示：若使用现代前端框架（Vite / Next 等），也可将 `quiz-bank.json` 放到 `public/` 目录随构建产物一起发布。

### 方式三：命令行快速校验题库

```bash
# 验证 JSON 是否合法并统计题目数
python3 -c "import json;d=json.load(open('data/quiz-bank.json',encoding='utf-8'));print('OK',d['meta']['totalQuestions'])"
```

更详细的使用说明（含答题流程、判分逻辑、分类体系详解）见 [`docs/guide.md`](docs/guide.md)。

---

## 本地预览（可选）

题库本身是纯数据，配合任意静态服务器即可预览：

```bash
# 在项目根目录启动一个简易静态服务器
python3 -m http.server 8080
# 浏览器访问 http://localhost:8080/data/quiz-bank.json 即可看到题库
```

---

## 二次开发建议

- **加题**：保持 `id` 唯一、遵循等级前缀规则，并维持各等级 `distribution` 分布与 `category` 语法分类主线。
- **导出**：按等级或语法分类筛选后导出为 CSV / Anki 牌组，用于背记。
- **判分**：`choice` / `truefalse` / passage 子题可自动判分；`fillblank` 建议忽略大小写与首尾空格后比较；`qa` 为主观题，建议提供参考答案与自评。
- **扩展等级**：在 `levels` 下新增 `key`，并补充对应 `questions` 数组与 `categories` 列表即可。

---

## 许可证

MIT License — 题库内容可自由用于个人学习与教学，转载请注明来源。
