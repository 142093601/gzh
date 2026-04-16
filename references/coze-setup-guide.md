# 扣子工作流配图配置指南

## 你的工作流现状

```
开始 → 大模型1 → 图像流1 → 代码1 → 文本处理1 → 直接输出1 → 结束
```

**问题**：图像流1 只生成了封面图，正文没有配图。

## 方案 A：完整配图（推荐，需改工作流）

### 步骤 1：修改大模型1 节点

编辑大模型1 的「人设与回复逻辑」（System Prompt），在末尾追加以下内容：

```
【重要：输出格式要求】

你必须严格按照以下 JSON 格式输出，不要输出任何其他内容：

{
  "html": "完整的HTML文章，封面图用<img src=\"IMG_0\">标记，正文配图用<img src=\"IMG_1\">、<img src=\"IMG_2\">标记",
  "prompts": [
    {"id": "IMG_0", "prompt": "封面图英文提示词，16:9，no text no watermark", "size": "1472x832"},
    {"id": "IMG_1", "prompt": "正文配图1英文提示词，1:1，no text no watermark", "size": "1024x1024"},
    {"id": "IMG_2", "prompt": "正文配图2英文提示词，1:1，no text no watermark", "size": "1024x1024"}
  ]
}

配图数量：
- 800字以下：封面+1张正文=2张
- 800-2000字：封面+2张正文=3张
- 2000字以上：封面+每500字1张

HTML排版规范：
- 所有样式内联，不用<style>
- 封面图border-radius:12px
- 章节标题：编号圆形(gradient背景)+渐变装饰线
- 金句：渐变背景卡片(左色条+圆角)
- 配图：border-radius:12px + box-shadow
- 分割线：渐变线 + ✦ ✦ ✦ 符号
- CTA：深色渐变圆角卡片
- 数字高亮：独立渐变卡片
- 信息卡片：浅底+边框+圆角12px
- 禁止使用display:flex（微信不兼容）
```

### 步骤 2：修改大模型1 输出变量名

将大模型1 的输出变量从 `output` 改为 `llm_json`（点击输出变量名可编辑）。

### 步骤 3：在图像流1 前加一个「代码」节点

在大模型1 和 图像流1 之间插入一个「代码」节点：

**节点名称**：解析prompt列表

**输入变量**：
- `llm_json` = `{{大模型1.llm_json}}`

**Python 代码**：
```python
import json

async def main(args: Args) -> Output:
    raw = args.params.get("llm_json", "")
    try:
        data = json.loads(raw)
        html = data.get("html", raw)
        prompts = data.get("prompts", [])
    except:
        html = raw
        prompts = []
    
    # 提取第一个prompt给图像流用
    first_prompt = ""
    if prompts:
        first_prompt = prompts[0].get("prompt", "")
    
    # 将prompts列表转为JSON字符串，供下游使用
    return {
        "html": html,
        "first_prompt": first_prompt,
        "prompts_json": json.dumps(prompts, ensure_ascii=False),
        "prompts_count": len(prompts)
    }
```

**输出变量**：
- `html`（文本）
- `first_prompt`（文本）
- `prompts_json`（文本）
- `prompts_count`（数字）

### 步骤 4：修改图像流1 节点

- **输入**：从 `{{大模型1.output}}` 改为 `{{解析prompt列表.first_prompt}}`
- **提示词输入**：从 `{{大模型1.output}}` 改为 `{{解析prompt列表.first_prompt}}`
- 其他保持不变

### 步骤 5：在图像流1 后面加一个「代码」节点（合并图片URL）

**节点名称**：合并图片

**输入变量**：
- `html` = `{{解析prompt列表.html}}`
- `cover_url` = `{{代码1.image_url}}` （即当前代码1的输出）
- `prompts_json` = `{{解析prompt列表.prompts_json}}`

**Python 代码**：
```python
import json
import re

async def main(args: Args) -> Output:
    html = args.params.get("html", "")
    cover_url = args.params.get("cover_url", "")
    prompts_json = args.params.get("prompts_json", "[]")
    
    try:
        prompts = json.loads(prompts_json)
    except:
        prompts = []
    
    # 第一张图（封面）用图像流生成的URL
    if cover_url and prompts:
        first_id = prompts[0].get("id", "IMG_0")
        html = html.replace(f'src="{first_id}"', f'src="{cover_url}"')
    
    # 其余配图占位符：用带提示词的渐变文字卡片代替
    # （如果没配多个图像流节点，用这个优雅降级方案）
    for item in prompts[1:]:
        pid = item.get("id", "")
        desc = item.get("desc", item.get("prompt", "")[:30])
        if pid and pid in html:
            # 用一个好看的视觉卡片替代图片
            card = (
                f'<div style="background:linear-gradient(135deg,#F5F3FF,#EDE9FE);'
                f'border:1px solid #E8E6F0;border-radius:12px;padding:24px;text-align:center;margin:20px 0;">'
                f'<p style="font-size:14px;color:#6C63FF;font-weight:600;margin:0 0 8px;">🎨</p>'
                f'<p style="font-size:13px;color:#8B8BA7;margin:0;">{desc}</p></div>'
            )
            html = html.replace(f'<img src="{pid}"', f'{card}<!-- replaced:{pid} --><div style="display:none"><img src="REMOVED')
    
    # 清理所有残留的IMG占位符img标签（替换为装饰卡片）
    def replace_placeholder(match):
        pid = match.group(1)
        # 查找对应的prompt描述
        desc = "配图"
        for p in prompts:
            if p.get("id") == pid:
                desc = p.get("prompt", "")[:40]
                break
        return (
            f'<div style="background:linear-gradient(135deg,#F5F3FF,#EDE9FE);'
            f'border:1px solid #E8E6F0;border-radius:12px;padding:24px;text-align:center;margin:24px 0;">'
            f'<p style="font-size:24px;margin:0 0 8px;">🎨</p>'
            f'<p style="font-size:13px;color:#8B8BA7;margin:0;line-height:1.6;">{desc}</p></div>'
        )
    html = re.sub(r'<img[^>]*src="(IMG_\d+)"[^>]*/?>', replace_placeholder, html)
    # 清理残留的display:none容器
    html = re.sub(r'<div style="display:none">[^<]*</div>', '', html)
    
    return {"final_html": html}
```

**输出变量**：
- `final_html`（文本）

### 步骤 6：修改文本处理1 节点

将输入变量改为：
- 之前可能是 `{{大模型1.output}}` + `{{代码1.image_url}}`
- 改为只输出 `{{合并图片.final_html}}`

如果文本处理1 是用来拼接 HTML 和图片的，现在不需要了，因为「合并图片」节点已经完成了。可以直接删掉文本处理1，把「合并图片」连到「直接输出1」。

### 最终工作流

```
开始 → 大模型1 → 解析prompt列表 → 图像流1 → 代码1 → 合并图片 → 直接输出1 → 结束
```

---

## 方案 B：纯文字视觉组件（最简单）

如果你不想改工作流节点，只需要改大模型1 的 System Prompt。

在人设与回复逻辑中追加：

```
【输出格式要求】

直接输出完整的 HTML 文章代码，不要用 JSON 包裹。

配图要求：
- 封面图：正常使用 <img> 标签（图像流会生成封面）
- 正文插图：不要用 <img> 标签，改用以下视觉组件替代：

🎨 插图位置用装饰卡片替代：
<div style="background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border:1px solid #E8E6F0;border-radius:12px;padding:24px;text-align:center;margin:24px 0;">
  <p style="font-size:28px;margin:0 0 8px;">📊</p>
  <p style="font-size:13px;color:#8B8BA7;margin:0;">（此处为配图位置：数据可视化）</p>
</div>

用以下组件丰富视觉：
- 数字高亮卡片（渐变背景+大号数字）
- 信息要点卡片（浅底+边框+要点列表）
- 金句引用卡片（渐变底+左色条+斜体）
- 步骤卡片（编号+文字）

HTML排版规范同上（内联样式、圆角12px、渐变、阴影等）。
```

这样改完，工作流完全不用动，只是正文里没有真正的图片，但会有好看的视觉组件填充。
