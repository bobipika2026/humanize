---
name: humanize
description: |
  AI内容人性化检测与改进指导。用于检测文本中的AI生成特征（机械感、套话、过度正式、缺乏细节等），
  并给出评分和改进建议，帮助内容更自然、更像人写的。适用于：用户完成文本创作后评估、AI生成内容优化、
  内容审核场景。当用户需要：检测文本是否像AI生成、让AI生成的内容更自然、给内容进行人性化评分时触发。
  /en AI content humanization detection and optimization guide. Detects AI-generated features (mechanical feel, clichés, overly formal, lack of details), provides scores and improvement suggestions to make content more natural and human-like. Use when: detecting if text is AI-generated, making AI content more natural, scoring content humanization.
metadata:
  {
    "openclaw": {
      "category": "content-generation",
      "tags": ["AI检测", "文本优化", "人性化", "内容质量", "AI detection", "text optimization", "humanization"],
      "version": "1.0.0"
    }
  }
---

# Humanize - AI内容人性化检测 / AI Content Humanization Detection

## 核心功能 / Core Features

1. **AI特征检测** - 15个检测维度，识别文本中的AI生成痕迹
   /en **AI Feature Detection** - 15 dimensions to identify AI-generated traces

2. **动态评分系统** - 0-100分，根据场景自动调整权重
   /en **Dynamic Scoring System** - 0-100 score with automatic scene-based weight adjustment

3. **自动场景判断** - 根据上下文自动识别21种用户角色
   /en **Automatic Scene Detection** - Auto-identifies 21 user scenarios from context

4. **改进建议** - 具体、可执行的优化方向
   /en **Improvement Suggestions** - Specific, actionable optimization directions

---

## 检测维度（15个） / Detection Dimensions (15)

| 序号 | 维度 | 英文名 | AI特征表现 / AI Characteristic |
|------|------|--------|------------------------------|
| 1 | 句式复杂度 | complexity | 从句过多、句子过长 / Overly complex sentences |
| 2 | 词汇密度 | vocabulary | 抽象名词多、缺口语词 / Too many abstract nouns |
| 3 | 情感波动 | emotion | 语气平稳、缺感叹词 / Flat emotion, lacks exclamations |
| 4 | 细节密度 | detail | 缺乏具体例子/数字 / Lacks specific examples/numbers |
| 5 | 模式化开头/结尾 | pattern | "首先""总之"类套话 / Clichés like "First", "In conclusion" |
| 6 | 突发性 | burstiness | 句子长度过于均匀 / Too uniform sentence length |
| 7 | 套话密度 | cliche | "赋能""闭环"类黑话 / Buzzwords like "empower", "loop" |
| 8 | 过度礼貌 | over_polite | 过于客套 / Excessively polite |
| 9 | 确定性过高 | over_certain | 缺乏"可能""也许" / Lacks "maybe", "probably" |
| 10 | 逻辑过于完美 | over_perfect | 缺乏思维跳跃 / Lacks natural thought jumps |
| 11 | 重复表达 | repetition | 近义句反复出现 / Repetitive expressions |
| 12 | 格式痕迹 | format | Markdown过于工整 / Overly neat Markdown |
| 13 | 主观缺乏 | subjectivity | 缺乏个人立场 / Lacks personal opinion |
| 14 | 例子泛化 | generalization | "比如"但无真实案例 / "For example" but no real case |
| 15 | 结尾套路 | ending | "希望对您有帮助" / Cliché endings like "Hope helps" |

---

## 场景权重配置（21场景 × 15维度）/ Scene Weights (21 × 15)

### 1. social（社交媒体 / Social Media）
```json
{
  "complexity": 0.05, "vocabulary": 0.05, "emotion": 0.15,
  "detail": 0.10, "pattern": 0.15, "burstiness": 0.10,
  "cliche": 0.10, "over_polite": 0.05, "over_certain": 0.05,
  "over_perfect": 0.05, "repetition": 0.05, "format": 0.02,
  "subjectivity": 0.03, "generalization": 0.02, "ending": 0.03
}
```

### 2. professional（专业文章 / Professional Articles）
```json
{
  "complexity": 0.10, "vocabulary": 0.15, "emotion": 0.02,
  "detail": 0.20, "pattern": 0.05, "burstiness": 0.03,
  "cliche": 0.08, "over_polite": 0.02, "over_certain": 0.05,
  "over_perfect": 0.10, "repetition": 0.05, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.05, "ending": 0.05
}
```

### 3. work（工作话术 / Work Communication）
```json
{
  "complexity": 0.05, "vocabulary": 0.10, "emotion": 0.20,
  "detail": 0.10, "pattern": 0.10, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.15, "over_certain": 0.05,
  "over_perfect": 0.03, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.03, "ending": 0.05
}
```

### 4. casual（日常闲聊 / Casual Chat）
```json
{
  "complexity": 0.05, "vocabulary": 0.05, "emotion": 0.20,
  "detail": 0.10, "pattern": 0.15, "burstiness": 0.20,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.05,
  "over_perfect": 0.02, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.03
}
```

### 5. education（论文、作业 / Education）
```json
{
  "complexity": 0.15, "vocabulary": 0.20, "emotion": 0.02,
  "detail": 0.10, "pattern": 0.03, "burstiness": 0.02,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.08,
  "over_perfect": 0.15, "repetition": 0.03, "format": 0.03,
  "subjectivity": 0.05, "generalization": 0.05, "ending": 0.02
}
```

### 6. ecommerce（商品描述 / E-commerce）
```json
{
  "complexity": 0.02, "vocabulary": 0.05, "emotion": 0.20,
  "detail": 0.25, "pattern": 0.10, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.05, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.03, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.10, "ending": 0.03
}
```

### 7. medical（医疗问诊 / Medical）
```json
{
  "complexity": 0.08, "vocabulary": 0.20, "emotion": 0.05,
  "detail": 0.15, "pattern": 0.03, "burstiness": 0.02,
  "cliche": 0.03, "over_polite": 0.05, "over_certain": 0.15,
  "over_perfect": 0.10, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.02, "generalization": 0.05, "ending": 0.02
}
```

### 8. legal（合同、协议 / Legal）
```json
{
  "complexity": 0.08, "vocabulary": 0.30, "emotion": 0.00,
  "detail": 0.20, "pattern": 0.02, "burstiness": 0.01,
  "cliche": 0.05, "over_polite": 0.01, "over_certain": 0.10,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.00
}
```

### 9. finance（金融报告 / Finance）
```json
{
  "complexity": 0.08, "vocabulary": 0.25, "emotion": 0.02,
  "detail": 0.20, "pattern": 0.05, "burstiness": 0.02,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.08,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.03,
  "subjectivity": 0.01, "generalization": 0.02, "ending": 0.00
}
```

### 10. media（新闻稿 / Media）
```json
{
  "complexity": 0.08, "vocabulary": 0.10, "emotion": 0.10,
  "detail": 0.20, "pattern": 0.15, "burstiness": 0.05,
  "cliche": 0.03, "over_polite": 0.02, "over_certain": 0.03,
  "over_perfect": 0.08, "repetition": 0.03, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.06
}
```

### 11. hr（招聘JD / HR）
```json
{
  "complexity": 0.08, "vocabulary": 0.15, "emotion": 0.02,
  "detail": 0.15, "pattern": 0.25, "burstiness": 0.02,
  "cliche": 0.08, "over_polite": 0.02, "over_certain": 0.02,
  "over_perfect": 0.05, "repetition": 0.03, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.08, "ending": 0.03
}
```

### 12. food（美食 / Food）
```json
{
  "complexity": 0.05, "vocabulary": 0.05, "emotion": 0.08,
  "detail": 0.30, "pattern": 0.10, "burstiness": 0.10,
  "cliche": 0.02, "over_polite": 0.02, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.05, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.10, "ending": 0.03
}
```

### 13. travel（旅行 / Travel）
```json
{
  "complexity": 0.05, "vocabulary": 0.08, "emotion": 0.15,
  "detail": 0.30, "pattern": 0.08, "burstiness": 0.05,
  "cliche": 0.03, "over_polite": 0.03, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.02, "format": 0.03,
  "subjectivity": 0.00, "generalization": 0.10, "ending": 0.03
}
```

### 14. realestate（房产 / Real Estate）
```json
{
  "complexity": 0.05, "vocabulary": 0.15, "emotion": 0.08,
  "detail": 0.30, "pattern": 0.12, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.03, "over_certain": 0.02,
  "over_perfect": 0.02, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.08, "ending": 0.03
}
```

### 15. customer_service（客服 / Customer Service）
```json
{
  "complexity": 0.02, "vocabulary": 0.05, "emotion": 0.25,
  "detail": 0.15, "pattern": 0.10, "burstiness": 0.03,
  "cliche": 0.05, "over_polite": 0.20, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.03, "ending": 0.03
}
```

### 16. tech_doc（技术文档 / Tech Doc）
```json
{
  "complexity": 0.15, "vocabulary": 0.30, "emotion": 0.02,
  "detail": 0.10, "pattern": 0.05, "burstiness": 0.02,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.05,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.05,
  "subjectivity": 0.00, "generalization": 0.02, "ending": 0.00
}
```

### 17. entertainment（娱乐 / Entertainment）
```json
{
  "complexity": 0.03, "vocabulary": 0.05, "emotion": 0.30,
  "detail": 0.10, "pattern": 0.05, "burstiness": 0.15,
  "cliche": 0.02, "over_polite": 0.00, "over_certain": 0.02,
  "over_perfect": 0.02, "repetition": 0.01, "format": 0.00,
  "subjectivity": 0.15, "generalization": 0.05, "ending": 0.05
}
```

### 18. writing（文学创作 / Creative Writing）
```json
{
  "complexity": 0.05, "vocabulary": 0.08, "emotion": 0.25,
  "detail": 0.20, "pattern": 0.02, "burstiness": 0.20,
  "cliche": 0.02, "over_polite": 0.00, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.01, "format": 0.00,
  "subjectivity": 0.08, "generalization": 0.02, "ending": 0.02
}
```

### 19. marketing（营销 / Marketing）
```json
{
  "complexity": 0.05, "vocabulary": 0.08, "emotion": 0.30,
  "detail": 0.15, "pattern": 0.15, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.00,
  "over_perfect": 0.02, "repetition": 0.01, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.05, "ending": 0.05
}
```

### 20. formal（官方声明 / Formal）
```json
{
  "complexity": 0.10, "vocabulary": 0.30, "emotion": 0.00,
  "detail": 0.10, "pattern": 0.08, "burstiness": 0.00,
  "cliche": 0.03, "over_polite": 0.00, "over_certain": 0.15,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.00
}
```

### 21. default（通用 / Default）
```json
{
  "complexity": 0.08, "vocabulary": 0.12, "emotion": 0.10,
  "detail": 0.12, "pattern": 0.10, "burstiness": 0.06,
  "cliche": 0.08, "over_polite": 0.05, "over_certain": 0.05,
  "over_perfect": 0.06, "repetition": 0.04, "format": 0.03,
  "subjectivity": 0.03, "generalization": 0.04, "ending": 0.04
}
```

---

## 自动场景判断 / Automatic Scene Detection

### 关键词匹配 / Keyword Matching

| 场景 / Scene | 关键词 / Keywords |
|-------------|------------------|
| social | 朋友圈、小红书、微博、抖音、分享 / WeChat, Xiaohongshu, Weibo, Douyin, share |
| professional | 文章、博客、攻略、教程、分析 / article, blog, guide, tutorial, analysis |
| work | 客户、话术、方案、商务、邮件 / client, script, proposal, business, email |
| education | 论文、作业、笔记、学术 / paper, homework, notes, academic |
| ecommerce | 商品、店铺、买家、优惠 / product, store, buyer, deal |
| medical | 症状、治疗、医生、健康 / symptom, treatment, doctor, health |
| legal | 合同、协议、条款 / contract, agreement, terms |
| finance | 投资、收益、股票、基金 / investment, return, stock, fund |
| hr | 招聘、面试、薪资 / recruitment, interview, salary |
| food | 菜谱、餐厅、好吃 / recipe, restaurant, delicious |
| travel | 旅游、行程、酒店、景点 / travel, itinerary, hotel, attraction |
| realestate | 房子、房源、平米、户型 / house, listing, sqm, layout |
| customer_service | 客服、问题、回复 / support, issue, reply |
| tech_doc | 文档、API、代码 / doc, API, code |
| entertainment | 电影、明星、八卦 / movie, star, gossip |
| writing | 故事、小说、散文 / story, novel, essay |
| marketing | 推广、引流、活动 / promotion, traffic, campaign |
| formal | 声明、公告、官方 / statement, announcement, official |

### 文本特征检测 / Text Feature Detection

- 文本长度 > 1000字 → education/finance/legal
- 含emoji/表情 → social/food/entertainment
- 含"请问""谢谢" → work/customer_service
- 含代码块 → tech_doc
- 含价格/数字密集 → ecommerce/finance/realestate
- 有问句+答句结构 → customer_service/medical

---

## 评分算法 / Scoring Algorithm

```
AI得分 = Σ(维度分 × 权重) / Σ(权重) × 100
/en AI Score = Σ(dimension_score × weight) / Σ(weight) × 100
```

### 评分对照 / Score Reference

| 分数 / Score | 等级 / Level | 描述 / Description |
|-------------|--------------|-------------------|
| 90-100 | 明显AI生成 / Clearly AI | 浓重的AI特征 / Strong AI features |
| 70-89 | 较大AI痕迹 / Significant AI | 明显AI风格 / Noticeable AI style |
| 50-69 | 部分AI特征 / Partial AI | 混合特征 / Mixed features |
| 30-49 | 较像人类 / Mostly Human | 较自然的表达 / Relatively natural |
| 0-29 | 非常人类 / Very Human | 非常像人写 / Very human-like |

---

## 输出格式 / Output Format

```markdown
## AI检测报告 / AI Detection Report

**AI评分 / AI Score**: XX/100 (等级 / Level)
**检测场景 / Scene**: social (自动判断 / 自动检测)

### 特征标签 / Feature Tags
- [标签1 / Tag 1]
- [标签2 / Tag 2]

### 问题点 / Issues
1. 问题描述 / Issue description

### 改进建议 / Suggestions
1. 具体建议 / Specific suggestion
```

---

## 改进建议库 / Improvement Library

| 特征 / Feature | 建议 / Suggestion |
|---------------|------------------|
| 句式过长 / Long sentences | 拆分成短句，增加节奏感 / Split into short sentences |
| 词汇太正式 / Too formal | 替换为口语化表达 / Use colloquial expressions |
| 缺乏情感 / No emotion | 加入语气词、感叹 / Add exclamations |
| 没有细节 / No details | 添加具体例子 / Add specific examples |
| 模式化开头 / Cliché opening | 换个自然切入方式 / Use natural opening |
| 过于完美 / Too perfect | 适当留瑕疵，更真实 / Add some imperfections |
| 套话过多 / Too many clichés | 少用黑话，用直白话 / Use plain language |
| 过度礼貌 / Overly polite | 去掉客套话 / Remove formalities |
| 确定性过高 / Over certain | 加点"可能""也许" / Add uncertainty |
| 逻辑过完美 / Too logical | 偶尔跑题 / Add tangents |
| 重复表达 / Repetitive | 删掉重复内容 / Remove repetition |
| 格式工整 / Too neat | 减少标题层级 / Reduce heading levels |
| 主观缺乏 / No subjectivity | 加个人看法 / Add personal opinion |
| 例子空泛 / Vague examples | 给出真实例子 / Give real examples |
| 结尾套路 / Cliché ending | 去掉套路结尾 / Remove cliché endings |

---

## Agent集成指南 / Agent Integration Guide

### 方式1：透明处理（推荐）/ Method 1: Transparent (Recommended)

用户无感知，Agent自动完成检测和优化：

```
用户：帮我写个深圳遛娃攻略
User: Help me write a Shenzhen parent-child travel guide

Agent内部流程 / Internal flow:
1. 生成内容（原始）/ Generate original content
2. 自动调用Skill检测 / Auto-call Skill for detection
3. 如果AI评分 > 60，自动优化 / If AI score > 60, auto-optimize
4. 返回优化后的结果 / Return optimized result

用户感知：只看到一个自然、像人写的结果
User perception: Only sees a natural, human-like result
```

### 方式2：轻度提示 / Method 2: Light Prompt

```
用户：帮我写个深圳遛娃攻略
User: Help me write a Shenzhen parent-child travel guide

Agent返回优化后的内容，并附带提示
Agent returns optimized content with a hint

---
上周带娃去了深圳科技馆（新馆），真的惊艳到了！...
---

✓ 已自动优化为更自然的表达 [查看详情]
✓ Auto-optimized to natural expression [View details]
```

### 方式3：用户主动触发 / Method 3: User-Triggered

```
用户：优化下这段文字
User: Optimize this text
→ 返回优化后内容 + "查看AI评分"链接
→ Return optimized content + "View AI score" link

用户：查看AI评分
User: View AI score
→ 展示完整检测报告
→ Show complete detection report
```

### 配置建议 / Configuration

- **默认启用透明模式** / Enable transparent mode by default
- **AI评分阈值** / AI score threshold: >60分自动优化 / auto-optimize, <30分直接返回 / return directly
- **提示信息** / Prompt: 可配置是否展示"已优化"提示 / configurable "optimized" hint
- **用户可选** / User option: 提供开关让用户选择是否自动优化 / provide toggle for auto-optimize

---

## 使用示例 / Usage Examples

**触发时机 / When to trigger:**
- 用户完成文本创作后 / After user completes text creation
- 检测到用户请求"优化这段文字" / When user requests "optimize this text"
- 内容需要审核时 / When content needs review

**示例用户请求 / Example requests:**
- "帮我看看这篇像不像AI写的" / "Check if this looks AI-written"
- "这段话太官方了，怎么改自然点" / "This is too formal, how to make it natural"
- "检测下这个文案有没有AI味" / "Check if this copy has AI smell"
- "用legal模式检测下这段合同" / "Detect this contract with legal mode"
- "帮我检测下这篇电商文案" / "Check this e-commerce copy"

---

## 技术细节 / Technical Details

- **检测维度数 / Detection dimensions**: 15
- **场景数量 / Scenes**: 21
- **权重配置 / Weight config**: JSON格式 / JSON format
- **版本 / Version**: 1.0.0
- **分类 / Category**: content-generation
- **标签 / Tags**: AI检测, 文本优化, 人性化 / AI detection, text optimization, humanization