---
name: humanize
description: |
  AI内容人性化检测与改进指导。用于检测文本中的AI生成特征（机械感、套话、过度正式、缺乏细节等），
  并给出评分和改进建议，帮助内容更自然、更像人写的。适用于：用户完成文本创作后评估、AI生成内容优化、
  内容审核场景。当用户需要：检测文本是否像AI生成、让AI生成的内容更自然、给内容进行人性化评分时触发。
metadata:
  {
    "openclaw": {
      "category": "content-generation",
      "tags": ["AI检测", "文本优化", "人性化", "内容质量"],
      "version": "1.0.0"
    }
  }
---

# Humanize Text - AI内容人性化检测

## 核心功能

1. **AI特征检测** - 15个检测维度，识别文本中的AI生成痕迹
2. **动态评分系统** - 0-100分，根据场景自动调整权重
3. **自动场景判断** - 根据上下文自动识别20+种用户角色
4. **改进建议** - 具体、可执行的优化方向

## 检测维度（15个）

| 序号 | 维度 | 英文名 | AI特征表现 |
|------|------|--------|-----------|
| 1 | 句式复杂度 | complexity | 从句过多、句子过长 |
| 2 | 词汇密度 | vocabulary | 抽象名词多、缺口语词 |
| 3 | 情感波动 | emotion | 语气平稳、缺感叹词 |
| 4 | 细节密度 | detail | 缺乏具体例子/数字 |
| 5 | 模式化开头/结尾 | pattern | "首先""总之"类套话 |
| 6 | 突发性 | burstiness | 句子长度过于均匀 |
| 7 | 套话密度 | cliche | "赋能""闭环"类黑话 |
| 8 | 过度礼貌 | over_polite | 过于客套 |
| 9 | 确定性过高 | over_certain | 缺乏"可能""也许" |
| 10 | 逻辑过于完美 | over_perfect | 缺乏思维跳跃 |
| 11 | 重复表达 | repetition | 近义句反复出现 |
| 12 | 格式痕迹 | format | Markdown过于工整 |
| 13 | 主观缺乏 | subjectivity | 缺乏个人立场 |
| 14 | 例子泛化 | generalization | "比如"但无真实案例 |
| 15 | 结尾套路 | ending | "希望对您有帮助" |

## 场景权重配置（21场景 × 15维度）

### 1. social（社交媒体：朋友圈、小红书）
```json
{
  "complexity": 0.05, "vocabulary": 0.05, "emotion": 0.15,
  "detail": 0.10, "pattern": 0.15, "burstiness": 0.10,
  "cliche": 0.10, "over_polite": 0.05, "over_certain": 0.05,
  "over_perfect": 0.05, "repetition": 0.05, "format": 0.02,
  "subjectivity": 0.03, "generalization": 0.02, "ending": 0.03
}
```

### 2. professional（专业文章：博客、攻略、教程）
```json
{
  "complexity": 0.10, "vocabulary": 0.15, "emotion": 0.02,
  "detail": 0.20, "pattern": 0.05, "burstiness": 0.03,
  "cliche": 0.08, "over_polite": 0.02, "over_certain": 0.05,
  "over_perfect": 0.10, "repetition": 0.05, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.05, "ending": 0.05
}
```

### 3. work（工作话术：商务、邮件、对接）
```json
{
  "complexity": 0.05, "vocabulary": 0.10, "emotion": 0.20,
  "detail": 0.10, "pattern": 0.10, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.15, "over_certain": 0.05,
  "over_perfect": 0.03, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.03, "ending": 0.05
}
```

### 4. casual（日常闲聊）
```json
{
  "complexity": 0.05, "vocabulary": 0.05, "emotion": 0.20,
  "detail": 0.10, "pattern": 0.15, "burstiness": 0.20,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.05,
  "over_perfect": 0.02, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.03
}
```

### 5. education（论文、作业、笔记）
```json
{
  "complexity": 0.15, "vocabulary": 0.20, "emotion": 0.02,
  "detail": 0.10, "pattern": 0.03, "burstiness": 0.02,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.08,
  "over_perfect": 0.15, "repetition": 0.03, "format": 0.03,
  "subjectivity": 0.05, "generalization": 0.05, "ending": 0.02
}
```

### 6. ecommerce（商品描述、买家秀）
```json
{
  "complexity": 0.02, "vocabulary": 0.05, "emotion": 0.20,
  "detail": 0.25, "pattern": 0.10, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.05, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.03, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.10, "ending": 0.03
}
```

### 7. medical（医疗问诊、健康建议）
```json
{
  "complexity": 0.08, "vocabulary": 0.20, "emotion": 0.05,
  "detail": 0.15, "pattern": 0.03, "burstiness": 0.02,
  "cliche": 0.03, "over_polite": 0.05, "over_certain": 0.15,
  "over_perfect": 0.10, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.02, "generalization": 0.05, "ending": 0.02
}
```

### 8. legal（合同、协议）
```json
{
  "complexity": 0.08, "vocabulary": 0.30, "emotion": 0.00,
  "detail": 0.20, "pattern": 0.02, "burstiness": 0.01,
  "cliche": 0.05, "over_polite": 0.01, "over_certain": 0.10,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.00
}
```

### 9. finance（金融报告、投资分析）
```json
{
  "complexity": 0.08, "vocabulary": 0.25, "emotion": 0.02,
  "detail": 0.20, "pattern": 0.05, "burstiness": 0.02,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.08,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.03,
  "subjectivity": 0.01, "generalization": 0.02, "ending": 0.00
}
```

### 10. media（新闻稿、采访稿）
```json
{
  "complexity": 0.08, "vocabulary": 0.10, "emotion": 0.10,
  "detail": 0.20, "pattern": 0.15, "burstiness": 0.05,
  "cliche": 0.03, "over_polite": 0.02, "over_certain": 0.03,
  "over_perfect": 0.08, "repetition": 0.03, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.06
}
```

### 11. hr（招聘JD、员工手册）
```json
{
  "complexity": 0.08, "vocabulary": 0.15, "emotion": 0.02,
  "detail": 0.15, "pattern": 0.25, "burstiness": 0.02,
  "cliche": 0.08, "over_polite": 0.02, "over_certain": 0.02,
  "over_perfect": 0.05, "repetition": 0.03, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.08, "ending": 0.03
}
```

### 12. food（菜单、食谱、餐厅评价）
```json
{
  "complexity": 0.05, "vocabulary": 0.05, "emotion": 0.08,
  "detail": 0.30, "pattern": 0.10, "burstiness": 0.10,
  "cliche": 0.02, "over_polite": 0.02, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.05, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.10, "ending": 0.03
}
```

### 13. travel（行程安排、景点介绍）
```json
{
  "complexity": 0.05, "vocabulary": 0.08, "emotion": 0.15,
  "detail": 0.30, "pattern": 0.08, "burstiness": 0.05,
  "cliche": 0.03, "over_polite": 0.03, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.02, "format": 0.03,
  "subjectivity": 0.00, "generalization": 0.10, "ending": 0.03
}
```

### 14. realestate（房源描述）
```json
{
  "complexity": 0.05, "vocabulary": 0.15, "emotion": 0.08,
  "detail": 0.30, "pattern": 0.12, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.03, "over_certain": 0.02,
  "over_perfect": 0.02, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.08, "ending": 0.03
}
```

### 15. customer_service（客服答复、FAQ）
```json
{
  "complexity": 0.02, "vocabulary": 0.05, "emotion": 0.25,
  "detail": 0.15, "pattern": 0.10, "burstiness": 0.03,
  "cliche": 0.05, "over_polite": 0.20, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.02, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.03, "ending": 0.03
}
```

### 16. tech_doc（技术文档、API注释）
```json
{
  "complexity": 0.15, "vocabulary": 0.30, "emotion": 0.02,
  "detail": 0.10, "pattern": 0.05, "burstiness": 0.02,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.05,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.05,
  "subjectivity": 0.00, "generalization": 0.02, "ending": 0.00
}
```

### 17. entertainment（娱乐、八卦、影评）
```json
{
  "complexity": 0.03, "vocabulary": 0.05, "emotion": 0.30,
  "detail": 0.10, "pattern": 0.05, "burstiness": 0.15,
  "cliche": 0.02, "over_polite": 0.00, "over_certain": 0.02,
  "over_perfect": 0.02, "repetition": 0.01, "format": 0.00,
  "subjectivity": 0.15, "generalization": 0.05, "ending": 0.05
}
```

### 18. writing（小说、故事、散文）
```json
{
  "complexity": 0.05, "vocabulary": 0.08, "emotion": 0.25,
  "detail": 0.20, "pattern": 0.02, "burstiness": 0.20,
  "cliche": 0.02, "over_polite": 0.00, "over_certain": 0.02,
  "over_perfect": 0.03, "repetition": 0.01, "format": 0.00,
  "subjectivity": 0.08, "generalization": 0.02, "ending": 0.02
}
```

### 19. marketing（营销文案、广告）
```json
{
  "complexity": 0.05, "vocabulary": 0.08, "emotion": 0.30,
  "detail": 0.15, "pattern": 0.15, "burstiness": 0.05,
  "cliche": 0.05, "over_polite": 0.02, "over_certain": 0.00,
  "over_perfect": 0.02, "repetition": 0.01, "format": 0.02,
  "subjectivity": 0.00, "generalization": 0.05, "ending": 0.05
}
```

### 20. formal（官方声明、公文）
```json
{
  "complexity": 0.10, "vocabulary": 0.30, "emotion": 0.00,
  "detail": 0.10, "pattern": 0.08, "burstiness": 0.00,
  "cliche": 0.03, "over_polite": 0.00, "over_certain": 0.15,
  "over_perfect": 0.15, "repetition": 0.02, "format": 0.03,
  "subjectivity": 0.02, "generalization": 0.02, "ending": 0.00
}
```

### 21. default（通用）
```json
{
  "complexity": 0.08, "vocabulary": 0.12, "emotion": 0.10,
  "detail": 0.12, "pattern": 0.10, "burstiness": 0.06,
  "cliche": 0.08, "over_polite": 0.05, "over_certain": 0.05,
  "over_perfect": 0.06, "repetition": 0.04, "format": 0.03,
  "subjectivity": 0.03, "generalization": 0.04, "ending": 0.04
}
```

## 自动场景判断

**从对话上下文判断：**

1. **检测平台/用途关键词**：
   - social: 朋友圈、小红书、微博、抖音、分享、发个
   - professional: 文章、博客、攻略、教程、分析、报告
   - work: 客户、话术、方案、商务、邮件、对接
   - education: 论文、作业、笔记、学术、研究
   - ecommerce: 商品、店铺、买家、优惠、销量
   - medical: 症状、治疗、医生、健康、问诊
   - legal: 合同、协议、条款、条款、依法
   - finance: 投资、收益、股票、基金、财报
   - hr: 招聘、面试、薪资、员工、JD
   - food: 菜谱、餐厅、好吃、做法、食材
   - travel: 旅游、行程、酒店、景点、机票
   - realestate: 房子、房源、平米、户型、房价
   - customer_service: 客服、问题、回复、解决
   - tech_doc: 文档、API、代码、开发、接口
   - entertainment: 电影、明星、八卦、好看
   - writing: 故事、小说、散文、写作
   - marketing: 推广、引流、转化、活动
   - formal: 声明、公告、官方、公示

2. **检测文本特征**：
   - 文本长度 > 1000字 → education/finance/legal
   - 含emoji/表情 → social/food/entertainment
   - 含"请问""谢谢""麻烦" → work/customer_service
   - 含代码块 → tech_doc
   - 含价格/数字密集 → ecommerce/finance/realestate
   - 有问句+答句结构 → customer_service/medical

### 自定义权重

用户可手动指定场景：
```
"帮我检测下这篇，场景用work模式"
"用legal模式看看这段合同"
```

## 评分算法

```
AI得分 = Σ(维度分 × 权重) / Σ(权重) × 100
```

**评分对照：**
- 90-100: 明显AI生成
- 70-89: 较大AI痕迹
- 50-69: 部分AI特征
- 30-49: 较像人类
- 0-29: 非常人类

## 输出格式

```markdown
## AI检测报告

**AI评分**: XX/100 (等级)
**检测场景**: social (自动判断/手动指定)

### 特征标签
- [标签1]
- [标签2]

### 问题点
1. 问题描述

### 改进建议
1. 具体建议
```

## 改进建议库

根据检测到的特征，给出对应建议：

| 特征 | 建议 |
|------|------|
| 句式过长 | 拆分成短句，增加节奏感 |
| 词汇太正式 | 替换为口语化表达 |
| 缺乏情感 | 加入语气词、感叹 |
| 没有细节 | 添加具体例子或个人经历 |
| 模式化开头 | 换个自然切入方式 |
| 过于完美 | 适当留瑕疵，更真实 |
| 套话过多 | 少用"赋能""闭环"，用直白话 |
| 过度礼貌 | 去掉客套话，像正常人说话 |
| 确定性过高 | 加点"可能""也许""不确定" |
| 逻辑过完美 | 偶尔"跑题"一下，加思维跳跃 |
| 重复表达 | 删掉重复内容 |
| 格式工整 | 减少标题层级，混用列表 |
| 主观缺乏 | 加个人看法："我觉得..." |
| 例子空泛 | 给出真实例子，不要"比如..." |
| 结尾套路 | 去掉"希望对您有帮助" |

## 使用场景

**触发时机：**
- 用户完成文本创作后
- 检测到用户请求"优化这段文字"
- 内容需要审核时
- 用户指定场景（如"用work模式检测"）

**示例用户请求：**
- "帮我看看这篇像不像AI写的"
- "这段话太官方了，怎么改自然点"
- "检测下这个文案有没有AI味"
- "用legal模式检测下这段合同"
- "帮我检测下这篇电商文案"

---

## Agent集成指南

### 推荐的集成方式

**方式1：透明处理（推荐）**

用户无感知，Agent自动完成检测和优化：

```
用户：帮我写个深圳遛娃攻略

Agent内部流程：
1. 生成内容（原始）
2. 自动调用Skill检测
3. 如果AI评分 > 60，自动优化
4. 返回优化后的结果

用户感知：只看到一个自然、像人写的结果
```

**方式2：轻度提示**

自动检测但给用户知情权：

```
用户：帮我写个深圳遛娃攻略

Agent：
[返回优化后的内容]

---
上周带娃去了深圳科技馆（新馆），真的惊艳到了！...
---

✓ 已自动优化为更自然的表达 [查看详情]
```

**方式3：用户主动触发**

用户明确要求检测时才展示报告：

```
用户：优化下这段文字
→ 返回优化后内容 + "查看AI评分"链接

用户：查看AI评分
→ 展示完整检测报告
```

### 代码集成示例

```python
# 伪代码示例
def generate_with_humanize(prompt):
    # 1. 生成原始内容
    content = llm.generate(prompt)
    
    # 2. 自动检测
    scene = detect_scene(prompt)  # 自动判断场景
    weights = get_weights(scene)   # 获取权重
    score = detect(content, weights)  # 检测打分
    
    # 3. 如果需要优化
    if score > 60:
        content = optimize(content, scene)
    
    # 4. 返回结果（可选：附带提示）
    return {
        "content": content,
        "optimized": score > 60,
        "score": score  # 可选返回
    }
```

### 配置建议

- **默认启用透明模式**：AI生成后自动Humanize
- **AI评分阈值**：>60分自动优化，<30分直接返回
- **提示信息**：可配置是否展示"已优化"提示
- **用户可选**：提供开关让用户选择是否自动优化