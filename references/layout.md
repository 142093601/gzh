# 公众号视觉排版设计规范 v2.0

**核心原则：排版即内容。好的排版让读者"先想看"，再"看得下去"。**

本规范提供 5 套完整 HTML 排版模板 + 14 个可复用视觉组件，所有样式内联，可直接用于公众号编辑器和扣子工作流。

---

## 零、微信公众号 CSS 兼容性速查

| 属性 | 支持 | 说明 |
|------|------|------|
| `border-radius` | ✅ | 推荐 4-16px |
| `box-shadow` | ✅ | 增加层次感 |
| `background: linear-gradient()` | ✅ | 标题、卡片背景必备 |
| `background-image` + `background-size` | ✅ | 可做纹理/渐变 |
| `text-align` | ✅ | 居左/居中/居右 |
| `display: inline-block` | ✅ | 标签、按钮 |
| `display: flex` | ⚠️ | 不稳定，避免 |
| `display: grid` | ❌ | 不支持 |
| `position: absolute/relative` | ⚠️ | 不可靠 |
| `::before / ::after` | ❌ | 不支持伪元素 |
| `<style>` 块 | ❌ | 必须全部内联 |
| `opacity` | ✅ | 可用 |

**结论：`border-radius` + `box-shadow` + `linear-gradient` + 精细间距 = 足够做出高级感。**

---

## 一、字体层级系统

| 元素 | 字号 | 字重 | 颜色 | 行高 | 字间距 |
|------|------|------|------|------|--------|
| 文章大标题 | 22px | Bold 800 | 见配色方案 | 1.4 | 1px |
| 章节标题 | 18px | Bold 700 | 见配色方案 | 1.4 | 0.5px |
| 子标题 | 16px | SemiBold 600 | #2d3748 | 1.5 | 0.5px |
| 正文 | 15px | Regular 400 | #3f3f3f | 1.8 | 0.5px |
| 引用/金句 | 15px | Regular 400 | 见组件 | 1.8 | 0.3px |
| 辅助文字 | 12-13px | Regular 400 | #a0aec0 | 1.5 | 0 |

**字体选择**：中文系统默认（苹方/微软雅黑），英文高亮可用 `font-family: -apple-system, "Helvetica Neue"`

---

## 二、间距系统

| 项目 | 数值 | 说明 |
|------|------|------|
| 行高 | 1.8 | 正文必须 1.8，文艺调性可到 2.0 |
| 段间距 | 1.5em | 段落之间呼吸感 |
| 页面左右内边距 | 16px | 移动端核心宽度 |
| 图片上下间距 | 20px | 图片与文字 |
| 章节间距 | 36px | 小标题前后 |
| 组件内边距 | 20px | 卡片、引用块内部 |

---

## 三、配色方案

### 方案 A：深蓝科技感（科技、财经、商业、AI）

| 角色 | 色值 | 用途 |
|------|------|------|
| 主色 | #1B1464 | 大标题 |
| 强调色 | #6C63FF | 装饰线、标签、按钮 |
| 高亮 | #FF6B6B | 关键数字、重点 |
| 正文 | #3f3f3f | 正文文字 |
| 辅助 | #8B8BA7 | 注释、辅助文字 |
| 浅底 | #F5F3FF | 引用块、卡片背景 |
| 分割线 | #E8E6F0 | 分割线、边框 |

### 方案 B：暖橙活力感（职场、成长、生活方式）

| 角色 | 色值 | 用途 |
|------|------|------|
| 主色 | #2D2D2D | 大标题 |
| 强调色 | #FF6B35 | 装饰线、标签、按钮 |
| 高亮 | #FFD93D | 重点标注 |
| 正文 | #3f3f3f | 正文文字 |
| 辅助 | #8B8B8B | 注释、辅助文字 |
| 浅底 | #FFF8F0 | 引用块、卡片背景 |
| 分割线 | #F0E6D8 | 分割线、边框 |

### 方案 C：莫兰迪文艺感（情感、人文、阅读、艺术）

| 角色 | 色值 | 用途 |
|------|------|------|
| 主色 | #2C2C2C | 大标题 |
| 强调色 | #9B8B7A | 装饰线、标签 |
| 高亮 | #C0392B | 金句、重点 |
| 正文 | #4A4A4A | 正文文字 |
| 辅助 | #999999 | 注释、辅助文字 |
| 浅底 | #FAF8F5 | 引用块、卡片背景 |
| 分割线 | #E8E0D8 | 分割线、边框 |

### 方案 D：薄荷清新感（健康、教育、女性、母婴）

| 角色 | 色值 | 用途 |
|------|------|------|
| 主色 | #1A535C | 大标题 |
| 强调色 | #4ECDC4 | 装饰线、标签 |
| 高亮 | #FF6B6B | 关键数字、重点 |
| 正文 | #3f3f3f | 正文文字 |
| 辅助 | #7B8B8B | 注释、辅助文字 |
| 浅底 | #F0FFF4 | 引用块、卡片背景 |
| 分割线 | #D4EDE9 | 分割线、边框 |

### 方案 E：暗夜高级感（潮流、设计、摄影、品牌）

| 角色 | 色值 | 用途 |
|------|------|------|
| 主色 | #F5F5F5 | 大标题（浅色字） |
| 强调色 | #C9A96E | 装饰线、标签、高亮 |
| 高亮 | #E8D5B5 | 重点 |
| 深底 | #1A1A2E | 卡片、引用块背景 |
| 辅助 | #888899 | 注释 |
| 正文 | #D0D0D0 | 深底场景正文 |
| 分割线 | #333355 | 分割线、边框 |

**配色铁律**：全文不超过 3 种彩色（不含黑白灰）。彩色只用于标签、高亮、引用块背景。

---

## 四、视觉组件库

以下组件使用方案 A 配色演示，实际使用时按第三节的色值替换表替换。

### 组件 1：文章头图 + 标题

```html
<div style="margin:0 0 24px;">
  <img src="{{COVER_URL}}" style="width:100%;max-width:100%;border-radius:12px;display:block;margin:0 0 20px;height:auto;" />
  <h2 style="font-size:22px;font-weight:800;color:#1B1464;line-height:1.4;margin:0 0 12px;letter-spacing:1px;padding:0 4px;">
    文章主标题
  </h2>
  <div style="padding:0 4px;">
    <span style="font-size:12px;color:#8B8BA7;">作者名</span>
    <span style="font-size:12px;color:#C8C8D8;margin:0 6px;">·</span>
    <span style="font-size:12px;color:#8B8BA7;">2026年4月16日</span>
  </div>
</div>
```

### 组件 2：导语/引言（渐变底 + 左色条）

```html
<div style="background:linear-gradient(135deg,#F5F3FF 0%,#EDE9FE 100%);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px;margin:0 0 28px;">
  <p style="font-size:15px;line-height:1.8;color:#4A4A6A;margin:0;">
    导语内容，50-80字。用悬念、数据或反常识观点抓住读者。
  </p>
</div>
```

### 组件 3：章节标题（编号圆形 + 渐变装饰线）

```html
<div style="margin:36px 0 20px;">
  <span style="display:inline-block;width:28px;height:28px;line-height:28px;text-align:center;background:linear-gradient(135deg,#6C63FF,#8B7CF6);color:#fff;font-size:13px;font-weight:700;border-radius:50%;vertical-align:middle;margin-right:10px;">1</span>
  <span style="font-size:18px;font-weight:700;color:#1B1464;vertical-align:middle;">章节标题</span>
</div>
<div style="height:2px;background:linear-gradient(90deg,#6C63FF,transparent);margin:0 0 20px;border-radius:1px;"></div>
```

### 组件 4：正文段落

```html
<p style="font-size:15px;line-height:1.8;color:#3f3f3f;margin:0 0 1.5em;letter-spacing:0.5px;">
  正文内容。每段3-5行。善用短句节奏。
</p>
```

### 组件 5：金句引用块（渐变背景 + 左色条）

```html
<div style="background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px;margin:24px 0;">
  <p style="font-size:15px;line-height:1.8;color:#4A4A6A;margin:0;font-style:italic;">
    "真正的高手，不是什么都会，而是知道什么不该做。"
  </p>
</div>
```

### 组件 6：数字高亮卡片

```html
<div style="background:linear-gradient(135deg,#6C63FF,#8B7CF6);border-radius:12px;padding:24px;text-align:center;margin:24px 0;">
  <p style="font-size:36px;font-weight:800;color:#fff;margin:0 0 4px;letter-spacing:2px;line-height:1;">95%</p>
  <p style="font-size:13px;color:rgba(255,255,255,0.8);margin:0;">用户满意度</p>
</div>
```

### 组件 7：信息卡片（要点/Tips）

```html
<div style="background:#F5F3FF;border:1px solid #E8E6F0;border-radius:12px;padding:20px 24px;margin:24px 0;">
  <p style="font-size:14px;font-weight:700;color:#6C63FF;margin:0 0 12px;">💡 要点提示</p>
  <p style="font-size:15px;line-height:1.8;color:#3f3f3f;margin:0 0 10px;">• 第一个要点</p>
  <p style="font-size:15px;line-height:1.8;color:#3f3f3f;margin:0 0 10px;">• 第二个要点</p>
  <p style="font-size:15px;line-height:1.8;color:#3f3f3f;margin:0;">• 第三个要点</p>
</div>
```

### 组件 8：对比卡片（深色表头 + 斑马纹）

```html
<div style="margin:24px 0;border-radius:12px;overflow:hidden;border:1px solid #E8E6F0;">
  <div style="background:linear-gradient(135deg,#1B1464,#2D2A5E);padding:12px 20px;">
    <span style="font-size:14px;font-weight:700;color:#fff;">对比维度</span>
  </div>
  <div style="padding:14px 20px;background:#fff;">
    <span style="font-size:14px;color:#6C63FF;font-weight:600;">方案A：</span>
    <span style="font-size:14px;color:#3f3f3f;">具体描述</span>
  </div>
  <div style="padding:14px 20px;background:#F9F8FF;">
    <span style="font-size:14px;color:#6C63FF;font-weight:600;">方案B：</span>
    <span style="font-size:14px;color:#3f3f3f;">具体描述</span>
  </div>
</div>
```

### 组件 9：分割线（渐变线 + 符号）

```html
<div style="text-align:center;margin:32px 0;">
  <span style="display:block;height:1px;background:linear-gradient(90deg,transparent,#E8E6F0 30%,#6C63FF 50%,#E8E6F0 70%,transparent);"></span>
  <span style="display:block;margin:12px auto 0;font-size:14px;color:#C8C8D8;letter-spacing:8px;">✦ ✦ ✦</span>
</div>
```

### 组件 10：CTA 行动号召

```html
<div style="background:linear-gradient(135deg,#1B1464,#2D2A5E);border-radius:12px;padding:28px 24px;text-align:center;margin:32px 0;">
  <p style="font-size:16px;font-weight:700;color:#fff;margin:0 0 8px;letter-spacing:1px;">觉得有用？</p>
  <p style="font-size:14px;color:rgba(255,255,255,0.8);margin:0 0 16px;">点赞 + 在看，让更多人看到 ❤️</p>
  <div style="display:inline-block;background:#6C63FF;color:#fff;font-size:14px;font-weight:600;padding:10px 28px;border-radius:24px;">立即关注 →</div>
</div>
```

### 组件 11：标签/分类

```html
<span style="display:inline-block;background:linear-gradient(135deg,#6C63FF,#8B7CF6);color:#fff;font-size:12px;font-weight:600;padding:4px 14px;border-radius:20px;letter-spacing:1px;margin-right:8px;">科技</span>
```

### 组件 12：配图（圆角 + 阴影 + 排版保护）

```html
<div style="margin:24px 0;text-align:center;">
  <img src="{{IMAGE_URL}}" style="width:100%;max-width:100%;border-radius:12px;display:inline-block;box-shadow:0 4px 16px rgba(108,99,255,0.1);height:auto;" />
  <p style="font-size:12px;color:#8B8BA7;text-align:center;margin:10px 0 0;">图片说明</p>
</div>
```

**注意事项**：
- 外层 `div` 的 `text-align:center` + 内层 `img` 的 `display:inline-block` 是微信公众号最稳定的图片居中方案
- `max-width:100%` 防止图片溢出
- `height:auto` 保持比例不变形
- 不要在图片容器内使用 `float` 或 `flex`
- 图片前后必须有段落分隔，不要紧贴标题/分割线

### 组件 13：编号步骤

```html
<div style="margin:24px 0;">
  <div style="margin-bottom:16px;">
    <span style="display:inline-block;width:24px;height:24px;line-height:24px;text-align:center;background:#6C63FF;color:#fff;font-size:12px;font-weight:700;border-radius:50%;vertical-align:top;margin-right:12px;">1</span>
    <span style="font-size:15px;line-height:1.8;color:#3f3f3f;">第一步操作内容</span>
  </div>
  <div style="margin-bottom:16px;">
    <span style="display:inline-block;width:24px;height:24px;line-height:24px;text-align:center;background:#6C63FF;color:#fff;font-size:12px;font-weight:700;border-radius:50%;vertical-align:top;margin-right:12px;">2</span>
    <span style="font-size:15px;line-height:1.8;color:#3f3f3f;">第二步操作内容</span>
  </div>
</div>
```

### 组件 14：文末尾部

```html
<div style="text-align:center;margin:36px 0 20px;">
  <span style="font-size:18px;color:#C8C8D8;letter-spacing:6px;">— THE END —</span>
</div>
<div style="height:3px;background:linear-gradient(90deg,transparent,#6C63FF 20%,#8B7CF6 50%,#6C63FF 80%,transparent);border-radius:2px;"></div>
```

---

## 五、完整文章模板

### 模板 A：标准图文型（最通用）

```html
<div style="margin:0 0 24px;">
  <img src="{{COVER_URL}}" style="width:100%;max-width:100%;border-radius:12px;display:block;margin:0 0 20px;height:auto;" />
  <h2 style="font-size:22px;font-weight:800;color:#1B1464;line-height:1.4;margin:0 0 12px;letter-spacing:1px;padding:0 4px;">
    文章主标题
  </h2>
  <div style="padding:0 4px;">
    <span style="font-size:12px;color:#8B8BA7;">作者名</span>
    <span style="font-size:12px;color:#C8C8D8;margin:0 6px;">·</span>
    <span style="font-size:12px;color:#8B8BA7;">2026年4月16日</span>
  </div>
</div>

<div style="background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px;margin:0 0 28px;">
  <p style="font-size:15px;line-height:1.8;color:#4A4A6A;margin:0;">导语内容</p>
</div>

<div style="margin:36px 0 20px;">
  <span style="display:inline-block;width:28px;height:28px;line-height:28px;text-align:center;background:linear-gradient(135deg,#6C63FF,#8B7CF6);color:#fff;font-size:13px;font-weight:700;border-radius:50%;vertical-align:middle;margin-right:10px;">1</span>
  <span style="font-size:18px;font-weight:700;color:#1B1464;vertical-align:middle;">第一部分</span>
</div>
<div style="height:2px;background:linear-gradient(90deg,#6C63FF,transparent);margin:0 0 20px;border-radius:1px;"></div>

<p style="font-size:15px;line-height:1.8;color:#3f3f3f;margin:0 0 1.5em;letter-spacing:0.5px;">正文段落...</p>

<div style="margin:24px 0;text-align:center;">
  <img src="{{IMAGE_URL}}" style="width:100%;max-width:100%;border-radius:12px;display:inline-block;box-shadow:0 4px 16px rgba(108,99,255,0.1);height:auto;" />
</div>

<div style="background:linear-gradient(135deg,#F5F3FF,#EDE9FE);border-left:4px solid #6C63FF;border-radius:0 12px 12px 0;padding:20px 24px;margin:24px 0;">
  <p style="font-size:15px;line-height:1.8;color:#4A4A6A;margin:0;font-style:italic;">"金句内容"</p>
</div>

<div style="text-align:center;margin:32px 0;">
  <span style="display:block;height:1px;background:linear-gradient(90deg,transparent,#E8E6F0 30%,#6C63FF 50%,#E8E6F0 70%,transparent);"></span>
  <span style="display:block;margin:12px auto 0;font-size:14px;color:#C8C8D8;letter-spacing:8px;">✦ ✦ ✦</span>
</div>

<div style="background:linear-gradient(135deg,#1B1464,#2D2A5E);border-radius:12px;padding:28px 24px;text-align:center;margin:32px 0;">
  <p style="font-size:16px;font-weight:700;color:#fff;margin:0 0 8px;">觉得有用？</p>
  <p style="font-size:14px;color:rgba(255,255,255,0.8);margin:0 0 16px;">点赞 + 在看 ❤️</p>
  <div style="display:inline-block;background:#6C63FF;color:#fff;font-size:14px;font-weight:600;padding:10px 28px;border-radius:24px;">立即关注 →</div>
</div>

<div style="text-align:center;margin:36px 0 20px;">
  <span style="font-size:18px;color:#C8C8D8;letter-spacing:6px;">— THE END —</span>
</div>
<div style="height:3px;background:linear-gradient(90deg,transparent,#6C63FF 20%,#8B7CF6 50%,#6C63FF 80%,transparent);border-radius:2px;"></div>
```

### 模板 B：数据驱动型（财经/分析类）

```html
<div style="margin:0 0 24px;padding:0 4px;">
  <h2 style="font-size:22px;font-weight:800;color:#1B1464;line-height:1.4;margin:0 0 12px;letter-spacing:1px;">
    2026年Q1经济数据解读
  </h2>
  <span style="font-size:12px;color:#8B8BA7;">数据分析团队</span>
  <span style="font-size:12px;color:#C8C8D8;margin:0 6px;">·</span>
  <span style="font-size:12px;color:#8B8BA7;">2026年4月</span>
</div>

<div style="background:linear-gradient(135deg,#6C63FF,#8B7CF6);border-radius:12px;padding:24px;text-align:center;margin:0 0 12px;">
  <p style="font-size:36px;font-weight:800;color:#fff;margin:0 0 4px;letter-spacing:2px;line-height:1;">5.3%</p>
  <p style="font-size:13px;color:rgba(255,255,255,0.8);margin:0;">GDP 同比增长</p>
</div>
<div style="display:inline-block;width:48%;vertical-align:top;margin-right:3%;">
  <div style="background:#F5F3FF;border:1px solid #E8E6F0;border-radius:12px;padding:20px;text-align:center;">
    <p style="font-size:28px;font-weight:800;color:#6C63FF;margin:0 0 4px;line-height:1;">12.8%</p>
    <p style="font-size:12px;color:#8B8BA7;margin:0;">消费增长</p>
  </div>
</div>
<div style="display:inline-block;width:48%;vertical-align:top;">
  <div style="background:#FFF5F5;border:1px solid #FFE0E0;border-radius:12px;padding:20px;text-align:center;">
    <p style="font-size:28px;font-weight:800;color:#FF6B6B;margin:0 0 4px;line-height:1;">-2.1%</p>
    <p style="font-size:12px;color:#8B8BA7;margin:0;">出口波动</p>
  </div>
</div>

<p style="font-size:15px;line-height:1.8;color:#3f3f3f;margin:24px 0 1.5em;">
  高亮数据：<span style="font-size:20px;font-weight:800;color:#6C63FF;">5.3%</span> 的增速背后...
</p>
```

### 模板 C：故事型（情感/人物类）

```html
<div style="margin:0 0 24px;">
  <img src="{{COVER_URL}}" style="width:100%;max-width:100%;border-radius:16px;display:block;margin:0 0 24px;height:auto;" />
</div>
<div style="text-align:center;margin:0 0 20px;">
  <h2 style="font-size:22px;font-weight:800;color:#2C2C2C;line-height:1.5;margin:0 0 16px;">
    那个凌晨三点还在改PPT的人<br/>后来怎么样了
  </h2>
  <div style="width:40px;height:2px;background:#9B8B7A;margin:0 auto 16px;border-radius:1px;"></div>
  <span style="font-size:12px;color:#999;">故事 · 约 8 分钟</span>
</div>
<div style="text-align:center;padding:20px 24px;margin:0 0 28px;">
  <p style="font-size:15px;line-height:2.0;color:#666;margin:0;font-style:italic;">
    "有些故事，只有经历过的人才懂。"
  </p>
</div>
<p style="font-size:15px;line-height:2.0;color:#4A4A4A;margin:0 0 2em;letter-spacing:0.5px;">
  故事正文。行高2.0增加沉浸感。
</p>
<div style="text-align:center;padding:24px 20px;margin:28px 0;">
  <p style="font-size:15px;line-height:2.0;color:#9B8B7A;margin:0;font-style:italic;">
    "生活不是等待暴风雨过去，<br/>而是学会在雨中起舞。"
  </p>
</div>
```

### 模板 D：暗夜高级感（设计/潮流/品牌）

```html
<div style="background:linear-gradient(180deg,#1A1A2E,#16213E);border-radius:16px;padding:28px 24px;margin:0 0 24px;">
  <div style="margin:0 0 16px;">
    <span style="display:inline-block;background:linear-gradient(135deg,#C9A96E,#E8D5B5);color:#1A1A2E;font-size:11px;font-weight:700;padding:3px 12px;border-radius:20px;letter-spacing:1px;">精选</span>
  </div>
  <h2 style="font-size:22px;font-weight:800;color:#F5F5F5;line-height:1.4;margin:0 0 12px;letter-spacing:1px;">
    设计的本质：少即是多
  </h2>
  <span style="font-size:12px;color:#888899;">设计实验室</span>
  <span style="font-size:12px;color:#555566;margin:0 6px;">·</span>
  <span style="font-size:12px;color:#888899;">2026年4月</span>
</div>
<div style="background:#1A1A2E;border-radius:12px;padding:24px;margin:0 0 16px;">
  <p style="font-size:15px;line-height:1.8;color:#D0D0D0;margin:0 0 1.5em;">正文...</p>
</div>
<div style="background:rgba(201,169,110,0.08);border-left:3px solid #C9A96E;border-radius:0 12px 12px 0;padding:20px 24px;margin:24px 0;">
  <p style="font-size:15px;line-height:1.8;color:#E8D5B5;margin:0;font-style:italic;">
    "设计不是装饰，是解决问题的最优雅方式。"
  </p>
</div>
```

---

## 六、配图规范与 AI 提示词

### 配图位置

| 位置 | 类型 | 尺寸 | 说明 |
|------|------|------|------|
| 封面 | 主视觉 | 900×500px | 第一印象 |
| 正文 | 场景图 | 全宽 | 每 500-800 字一张 |
| 情绪处 | 氛围图 | 85% 宽度居中 | 圆角 16px |
| 数据 | 信息图 | 全宽 | 复杂数据可视化 |

### AI 配图 Prompt

**科技类（方案A）**：
```
A clean modern editorial illustration, minimal flat design with geometric shapes. Color: navy (#1B1464), white, violet (#6C63FF). Abstract [主题]. No text, no watermark. 16:9, soft gradient background.
```

**文艺类（方案C）**：
```
A warm soft-toned editorial illustration, watercolor style. Color: cream, dusty rose, warm brown (#9B8B7A). Abstract [主题]. No text, no watermark. Gentle mood, 16:9.
```

**暗夜类（方案E）**：
```
A luxurious dark editorial illustration, geometric abstract on dark navy (#1A1A2E) with gold (#C9A96E) accents. Minimal high-end aesthetic. [主题]. No text, no watermark. 16:9, dramatic lighting.
```

**正文场景图**：
```
Editorial illustration, flat design, [场景描述]. Colors: [主色] + [强调色]. Clean minimal modern, soft shadows. No text. Square format, mobile-friendly.
```

---

## 七、扣子工作流输出规则

### 必须遵守

1. **所有样式内联** — 无 `<style>` 块
2. **配图占位符** — `{{ILLUSTRATION_N_URL}}` 由图像流替换
3. **系统字体** — 不自定义
4. **间距精确** — 所有 margin/padding 用具体值
5. **圆角统一** — 同文统一 12px
6. **避免 flex** — 用 inline-block 替代

### 配色替换表

| 方案 | 强调色 | 浅底 | 深底 | 金句色 | 边框色 | 主色 |
|------|--------|------|------|--------|--------|------|
| A | #6C63FF | #F5F3FF | #1B1464 | #4A4A6A | #E8E6F0 | #1B1464 |
| B | #FF6B35 | #FFF8F0 | #2D2D2D | #5A4A3A | #F0E6D8 | #2D2D2D |
| C | #9B8B7A | #FAF8F5 | #2C2C2C | #6A5A4A | #E8E0D8 | #2C2C2C |
| D | #4ECDC4 | #F0FFF4 | #1A535C | #3A5A5A | #D4EDE9 | #1A535C |
| E | #C9A96E | #1A1A2E | #0D0D1A | #E8D5B5 | #333355 | #F5F5F5 |

---

## 八、排版自检

### 视觉

- [ ] 全文不超过 3 种彩色
- [ ] 圆角半径统一
- [ ] 引用块样式统一
- [ ] 配图风格统一
- [ ] 分割线风格统一
- [ ] 章节编号样式一致
- [ ] 字号层级清晰
- [ ] 手机预览字号和间距舒适
- [ ] 封面高清 + 圆角 + 阴影
- [ ] CTA 醒目、对比度足够

### 技术

- [ ] 所有样式内联
- [ ] 无 display:flex（用 inline-block）
- [ ] 渐变语法正确
- [ ] 占位符格式正确
- [ ] HTML 标签正确闭合
- [ ] JSON 中引号转义正确
