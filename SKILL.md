---
name: wechat-article
description: |
  公众号文章构思与设计助手。当用户需要策划、构思、设计微信公众号文章时使用此技能。
  触发场景：用户提到公众号、微信文章、推文、文章选题、文章大纲、文章排版、爆款文章、
  文章标题优化、封面设计思路、文章结构、扣子工作流、AI配图等。
  NOT for：通用长文写作（非公众号场景）、学术论文、技术文档。
---

# 公众号文章设计

协助用户从选题到成稿的全流程公众号文章策划。支持扣子（Coze）工作流自动排版输出。

## 工作流程

根据用户需求，灵活执行以下步骤中的相关部分：

### 1. 选题定位

向用户确认（如未提供）：
- **账号定位**：领域、目标读者、调性（专业/轻松/犀利/温情）
- **文章目标**：涨粉？转化？品牌曝光？用户教育？
- **当前热点**：是否有想蹭的热点或话题

给出 2-3 个选题方向建议，每个包含：
- 标题（主标题+副标题）
- 切入角度
- 预估受众吸引力（⭐1-5）

选题时可参考 [references/styles.md](references/styles.md) 中各领域头部账号的选题偏好。

### 2. 文章大纲

选题确定后，输出结构化大纲：

```
标题：[主标题] | [副标题]
导语：[hook句，50字以内]
├── 第一部分：[小标题] — 作用说明
├── 第二部分：[小标题] — 作用说明
├── 第三部分：[小标题] — 作用说明
├── ...
└── 结尾：[CTA/总结/互动引导]
预估字数：xxx字
配图建议：x张（位置+内容方向）
排版方案：[从layout.md中选择配色方案和布局模板]
```

如用户指定对标账号，读取 [references/styles.md](references/styles.md) 中对应风格拆解，参考其结构特点。

### 3. 标题优化

提供 5-8 个标题备选，覆盖不同风格：
- **悬念型**：引发好奇心
- **数字型**：具体数字增强可信度
- **痛点型**：直击读者痛点
- **热点型**：蹭热度/名人
- **对比型**：制造反差

### 4. 正文撰写

按大纲展开正文，注意：
- **开头**：前 3 行决定留存，参见 [references/hooks.md](references/hooks.md) 中 10 种 hook 公式
- **段落**：每段 3-5 行，善用短句
- **小标题**：每 300-500 字一个，起承上启下作用
- **互动点**：每 800-1000 字设置一个互动锚点（提问/投票引导/金句）
- **结尾**：总结 + CTA（关注/转发/评论引导）

### 5. 视觉排版设计

读取 [references/layout.md](references/layout.md)，提供完整排版方案：

**5.1 配色方案选择**（根据账号调性匹配）
- 方案 A：深蓝科技感 → 科技、财经、商业
- 方案 B：暖橙活力感 → 职场、成长、生活方式
- 方案 C：莫兰迪文艺感 → 情感、阅读、人文
- 方案 D：薄荷清新感 → 健康、教育、女性向

**5.2 字体层级与间距** — 按 layout.md 规范输出具体 px 值

**5.3 视觉组件** — 引用块、高亮标注、分割线、标签的统一样式

**5.4 AI 配图生成**
- 确定每张配图的位置和内容方向
- 生成扣子图像流可用的英文 prompt（参考 layout.md 第六节）
- 封面图 prompt + 正文插图 prompt 分开输出

**5.5 扣子工作流输出**
- 如果用户使用扣子工作流，按下方"扣子工作流 JSON 输出格式"输出结构化数据
- 确保所有样式内联（公众号编辑器不支持外部 CSS）

### 6. 发布前自检

文章完成后，引导用户使用 [references/checklist.md](references/checklist.md) 逐项检查。优先执行"快速自检版"（5 项），全部通过后再做完整版。

## 常用文章结构模板

### 模板 A：问题-方案型
> 痛点引入 → 分析原因 → 解决方案（分步骤） → 总结 + CTA

### 模板 B：清单/盘点型
> 引言 → 条目1 → 条目2 → ... → 条目N → 总结推荐 + CTA

### 模板 C：故事驱动型
> 故事开头 → 转折/冲突 → 启发/方法论 → 升华主题 + CTA

### 模板 D：热点解读型
> 热点引入 → 事件梳理 → 深度分析 → 个人观点 → 互动提问

## 扣子工作流 JSON 输出格式

**重要：当用户明确表示要在扣子工作流中使用时，必须严格按照以下 JSON 格式输出。**

### 输出架构（2 个节点）

扣子工作流推荐用 **2 个节点** 完成文章生成 + 配图：

```
[AI 大模型节点] → 生成文章 JSON（含 html_content + image_prompts）
         ↓
[图像流节点]    → 读取 image_prompts，生成图片，回填到 html_content
         ↓
[输出]          → 带图片的完整 HTML
```

**关键：AI 节点只生成文字（HTML + 配图 prompt），图片生成必须由扣子的「图像流」节点完成。**

### 节点 1：文章生成（AI 大模型节点）

AI 节点输出一个 JSON，包含完整的 HTML 和配图 prompt 列表：

```json
{
  "title": "文章主标题",
  "word_count": 1500,
  "length_category": "medium",
  "color_scheme": "A",
  "hook_type": "数据震撼型",

  "html_content": "<完整的 HTML 字符串，配图位置用 IMG_PLACEHOLDER_N 标记>",

  "image_prompts": [
    {
      "id": "IMG_PLACEHOLDER_1",
      "position": "封面图",
      "prompt": "A clean, modern editorial illustration for a tech article. Minimal flat design with geometric shapes. Color palette: deep blue (#1B1464), white, violet accent (#6C63FF). Abstract representation of AI technology. No text, no watermark. 16:9 ratio, high quality.",
      "size": "1472x832"
    },
    {
      "id": "IMG_PLACEHOLDER_2",
      "position": "第一部分结束后",
      "prompt": "Editorial illustration, flat design, depicting a person working efficiently with AI tools on laptop. Colors: navy (#1B1464) and violet (#6C63FF). Clean minimal modern style, soft shadows. No text. Square format, mobile-friendly.",
      "size": "1024x1024"
    },
    {
      "id": "IMG_PLACEHOLDER_3",
      "position": "第二部分结束后",
      "prompt": "Infographic-style editorial illustration showing data visualization with charts and graphs. Colors: navy (#1B1464), violet (#6C63FF), white. Minimal professional, no clutter. Square format.",
      "size": "1024x1024"
    }
  ],

  "metadata": {
    "sections": ["第一部分标题", "第二部分标题"],
    "total_images": 3,
    "template": "standard"
  }
}
```

**html_content 中配图标记的写法**：

在 HTML 中需要插入图片的位置，使用 `<img src="IMG_PLACEHOLDER_N">` 作为标记。扣子的图像流节点生成图片后，将 `IMG_PLACEHOLDER_1` 替换为实际图片 URL 即可。

示例 HTML 片段（注意配图标记）：
```html
<p>上一段正文...</p>
<img src="IMG_PLACEHOLDER_2" style="width:100%;border-radius:12px;display:block;box-shadow:0 4px 16px rgba(108,99,255,0.1);margin:20px 0;" />
<p>下一段正文...</p>
```

**配图数量规则**：
- short（<800字）：1 张封面 + 1 张正文 = 2 张
- medium（800-2000字）：1 张封面 + 2 张正文 = 3 张
- long（>2000字）：1 张封面 + 每 500-800 字 1 张正文

**配图位置策略**：
- 封面图：文章最顶部
- 正文配图：每 1-2 个章节之间插入一张
- 避免：连续两张配图、配图离相关文字太远

### 节点 2：图像流（扣子图像流节点）

用户在扣子工作流中需要配置一个图像流节点来处理正文配图。

**扣子图像流节点配置建议**：

1. **输入**：读取 `image_prompts` 数组中的 `prompt` 字段
2. **模型**：doubao-seedream 或其他扣子内置图像模型
3. **尺寸**：跟随每个 prompt 的 `size` 字段（封面 1472×832，正文 1024×1024）
4. **循环模式**：如果有多张配图，使用「批处理」或「循环」节点遍历 `image_prompts` 数组
5. **输出**：生成的图片 URL

**扣子图像流后的文本替换**：

图像流节点生成 URL 后，需要将 html_content 中的 `IMG_PLACEHOLDER_1`、`IMG_PLACEHOLDER_2` 等替换为实际 URL。在扣子中可以用「文本替换」节点或「代码」节点完成：

```
html_content = html_content.replace("IMG_PLACEHOLDER_1", "https://生成的图片URL1")
html_content = html_content.replace("IMG_PLACEHOLDER_2", "https://生成的图片URL2")
```

### 如果不使用图像流节点

如果用户暂时不配置图像流节点，html_content 中的 `<img src="IMG_PLACEHOLDER_N">` 会显示为破损图片。建议：

1. 在 AI 节点的 prompt 中加入指令："如果无法生成图片，在 IMG_PLACEHOLDER 位置输出一个优雅的装饰性文字卡片代替图片"
2. 或者：HTML 中不输出 `<img>` 标签，改用纯文字组件（信息卡片、数字卡片等）填充视觉空白

## 参考资料

- **风格范例库**：[references/styles.md](references/styles.md) — 10+ 头部账号风格拆解
- **Hook 套路库**：[references/hooks.md](references/hooks.md) — 10 种开头 hook 公式
- **视觉排版规范**：[references/layout.md](references/layout.md) — 配色方案、字体层级、间距系统、视觉组件、AI配图prompt、扣子HTML输出模板
- **发布前自检清单**：[references/checklist.md](references/checklist.md) — 7 大类 30+ 检查项

## 输出格式

默认用中文回复，结构清晰。大纲和标题部分使用列表格式方便用户直接使用。正文部分用自然段落，附带排版标记建议。

当用户使用扣子工作流时，严格按照上方"扣子工作流 JSON 输出格式"输出各节点所需的结构化 JSON 数据。确保：
1. JSON 格式严格合法，无语法错误
2. 字段名称与扣子工作流节点变量名一致
3. 数值类型正确（word_count 为数字而非字符串）
4. HTML 内容中的引号使用转义 `\"`
