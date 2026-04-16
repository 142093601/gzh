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

**重要：当用户明确表示要在扣子工作流中使用时，必须严格按照以下 JSON 格式输出。每个节点的数据格式必须与扣子工作流中对应的节点类型匹配。**

### 节点 1：判断文章长度

扣子工作流中的"判断文章长度"节点需要接收结构化 JSON，用于判断文章属于长文/中等/短文，从而决定配图数量和排版策略。

```json
{
  "title": "文章主标题",
  "subtitle": "副标题（可选）",
  "word_count": 1500,
  "length_category": "medium",
  "sections": [
    {
      "section_id": 1,
      "title": "第一部分小标题",
      "word_count": 400,
      "content_summary": "本段核心内容一句话概括"
    },
    {
      "section_id": 2,
      "title": "第二部分小标题",
      "word_count": 500,
      "content_summary": "本段核心内容一句话概括"
    }
  ],
  "total_sections": 2,
  "hook_type": "数据震撼型",
  "color_scheme": "A",
  "template": "standard"
}
```

**字段说明**：
- `length_category`: "short"(<800字) | "medium"(800-2000字) | "long"(>2000字)
- `hook_type`: 见 hooks.md，必须是 10 种之一
- `color_scheme`: "A"|"B"|"C"|"D"，对应 layout.md 配色方案
- `template`: "standard"|"data"|"story"|"hotspot"

### 节点 2：循环（正文配图循环）

扣子工作流的"循环"节点需要一个数组来迭代，每项包含配图位置和 prompt。

```json
{
  "illustrations": [
    {
      "id": 1,
      "position": "cover",
      "position_desc": "文章封面图",
      "prompt": "A clean, modern editorial illustration for a tech article. Minimal flat design with geometric shapes. Color palette: deep blue (#1a1a2e), white, coral accent (#e94560). Abstract representation of artificial intelligence. No text, no watermark. 16:9 ratio, high quality.",
      "size": "1472x832",
      "aspect_ratio": "16:9"
    },
    {
      "id": 2,
      "position": "after_section_1",
      "position_desc": "第一部分结束后",
      "prompt": "Editorial illustration, flat design style, depicting a person analyzing data on multiple screens. Color scheme matching article: #1a1a2e and #667eea. Clean, minimal, modern. No text overlay. Suitable for mobile reading.",
      "size": "1024x1024",
      "aspect_ratio": "1:1"
    },
    {
      "id": 3,
      "position": "after_section_2",
      "position_desc": "第二部分结束后",
      "prompt": "Minimalist character illustration, modern editorial style. A team collaborating around a digital whiteboard with charts. Soft color palette, clean lines. No text, no watermark. Square format.",
      "size": "1024x1024",
      "aspect_ratio": "1:1"
    }
  ],
  "total_count": 3
}
```

**配图数量规则**：
- short（<800字）：1 张封面 + 1 张正文 = 2 张
- medium（800-2000字）：1 张封面 + 2-3 张正文 = 3-4 张
- long（>2000字）：1 张封面 + 每 500-800 字 1 张正文

### 节点 3：正文配图

每个配图节点处理单张图片的生成，输入为循环数组中的单个 item。

```json
{
  "image_request": {
    "prompt": "Editorial illustration, flat design style, depicting...",
    "size": "1024x1024",
    "position": "after_section_1",
    "fallback_placeholder": "<!-- ILLUSTRATION_2 -->"
  }
}
```

### 节点 4：排版并输出（最终 HTML 输出）

扣子工作流的"排版并输出"节点接收完整文章数据，输出可直接粘贴到公众号编辑器的 HTML 片段。

```json
{
  "output_format": "html",
  "html_content": "<div style=\"margin:0 0 24px;\"><img src=\"{{COVER_URL}}\" style=\"width:100%;border-radius:12px;display:block;margin:0 0 20px;\" /><h2 style=\"font-size:22px;font-weight:800;color:#1B1464;line-height:1.4;margin:0 0 12px;letter-spacing:1px;padding:0 4px;\">文章主标题</h2><div style=\"padding:0 4px;\"><span style=\"font-size:12px;color:#8B8BA7;\">作者名</span><span style=\"font-size:12px;color:#C8C8D8;margin:0 6px;\">·</span><span style=\"font-size:12px;color:#8B8BA7;\">2026年4月16日</span></div></div>\\n<div style=\"background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px;margin:0 0 28px;\"><p style=\"font-size:15px;line-height:1.8;color:#4A4A6A;margin:0;\">导语内容，hook句，50字以内...</p></div>\\n<div style=\"margin:36px 0 20px;\"><span style=\"display:inline-block;width:28px;height:28px;line-height:28px;text-align:center;background:linear-gradient(135deg,#6C63FF,#8B7CF6);color:#fff;font-size:13px;font-weight:700;border-radius:50%;vertical-align:middle;margin-right:10px;\">1</span><span style=\"font-size:18px;font-weight:700;color:#1B1464;vertical-align:middle;\">第一部分小标题</span></div><div style=\"height:2px;background:linear-gradient(90deg,#6C63FF,transparent);margin:0 0 20px;border-radius:1px;\"></div>\\n<p style=\"font-size:15px;line-height:1.8;color:#3f3f3f;margin:0 0 1.5em;letter-spacing:0.5px;\">正文段落内容...</p>\\n<div style=\"margin:20px 0;\"><img src=\"{{ILLUSTRATION_2_URL}}\" style=\"width:100%;border-radius:12px;display:block;box-shadow:0 4px 16px rgba(108,99,255,0.1);\" /></div>\\n<p style=\"font-size:15px;line-height:1.8;color:#3f3f3f;margin:0 0 1.5em;\">更多正文...</p>\\n<div style=\"background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px;margin:24px 0;\"><p style=\"font-size:15px;line-height:1.8;color:#4A4A6A;margin:0;font-style:italic;\">金句或重点引用内容</p></div>\\n<div style=\"text-align:center;margin:32px 0;\"><span style=\"display:block;height:1px;background:linear-gradient(90deg,transparent,#E8E6F0 30%,#6C63FF 50%,#E8E6F0 70%,transparent);\"></span><span style=\"display:block;margin:12px auto 0;font-size:14px;color:#C8C8D8;letter-spacing:8px;\">✦ ✦ ✦</span></div>\\n<div style=\"background:linear-gradient(135deg,#1B1464,#2D2A5E);border-radius:12px;padding:28px 24px;text-align:center;margin:32px 0;\"><p style=\"font-size:16px;font-weight:700;color:#fff;margin:0 0 8px;letter-spacing:1px;\">觉得有用？</p><p style=\"font-size:14px;color:rgba(255,255,255,0.8);margin:0 0 16px;\">点赞 + 在看，让更多人看到 ❤️</p><div style=\"display:inline-block;background:#6C63FF;color:#fff;font-size:14px;font-weight:600;padding:10px 28px;border-radius:24px;\">立即关注 →</div></div>",
  "image_slots": [
    {
      "slot_id": "ILLUSTRATION_2",
      "position_after": "第一部分小标题",
      "description": "第一部分配图占位符"
    }
  ],
  "cover_image_prompt": "A clean, modern editorial illustration...",
  "metadata": {
    "title": "文章主标题",
    "word_count": 1500,
    "section_count": 2,
    "image_count": 3,
    "color_scheme": "A"
  }
}
```

**HTML 输出规则（必须遵守）**：

1. **所有样式必须内联**：公众号编辑器不支持 `<style>` 标签或外部 CSS。详细模板和组件参见 `references/layout.md`
2. **配图使用占位符**：用 `{{ILLUSTRATION_N_URL}}` 占位，扣子工作流中由图像流节点替换为实际 URL
3. **标题区域**：封面图 `border-radius:12px` + 大标题 `font-size:22px;font-weight:800;color:#1B1464` + 作者行用 `inline-block` 拼接
4. **导语**：用渐变背景卡片 `background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px`
5. **章节标题**：编号圆形 `background:linear-gradient(135deg,#6C63FF,#8B7CF6);border-radius:50%` + 标题文字 + 下方渐变装饰线 `background:linear-gradient(90deg,#6C63FF,transparent)`
6. **正文**：`<p>` 用 `font-size:15px;line-height:1.8;color:#3f3f3f;letter-spacing:0.5px`（行高从 1.75 提升到 1.8）
7. **金句引用**：渐变背景卡片 + 左色条 + `font-style:italic`（不要用 `<blockquote>`，改用 `<div>` 包裹 `<p>`）
8. **数字高亮**：独立渐变卡片 `background:linear-gradient(135deg,#6C63FF,#8B7CF6);border-radius:12px;padding:24px;text-align:center` 数字 `font-size:36px;color:#fff`
9. **信息卡片**：浅底 + 边框 `background:#F5F3FF;border:1px solid #E8E6F0;border-radius:12px;padding:20px 24px`
10. **分割线**：渐变线 + 居中符号 ✦ ✦ ✦（不要用 `<hr>`）
11. **配图**：`border-radius:12px;box-shadow:0 4px 16px rgba(108,99,255,0.1)` 增加层次感
12. **CTA**：深色渐变圆角卡片 `background:linear-gradient(135deg,#1B1464,#2D2A5E);border-radius:12px;padding:28px 24px;text-align:center`
13. **尾部**：`— THE END —` + 底部渐变装饰线
14. **圆角统一**：全文所有圆角组件统一 `12px`
15. **禁止 `display:flex`**：微信中不稳定，全部用 `display:inline-block` + `vertical-align`

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
