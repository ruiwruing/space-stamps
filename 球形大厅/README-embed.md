# 天问·方寸 — 球形邮票展厅 · 嵌入包

中国邮政 1951—2022 年航空航天邮票（24 套 · 81 枚单枚）的三维球形展厅组件，
可作为**任意网页的一部分**内嵌使用。

## 包内文件

| 文件 | 说明 |
|------|------|
| `stamp-sphere-embed.html` | **可嵌入组件**（约 4.1 MB，完全自包含，零外部依赖，字体除外） |
| `embed-demo.html` | **嵌入示例首页**：演示如何把展厅作为页面一个区块嵌入 |
| `README-embed.md` | 本说明 |

## 两种嵌入方式

### 方式一：iframe（推荐，最简单）

把 `stamp-sphere-embed.html` 与你的网页放在同一目录，然后：

```html
<iframe src="stamp-sphere-embed.html"
        style="width:100%; height:640px; border:0;"
        title="三维球形邮票展厅"></iframe>
```

- 组件会**自适应 iframe 尺寸**（ResizeObserver 监听容器）
- 样式、脚本、全局变量**完全隔离**，不影响宿主页面
- 档案页、加载层都收在组件内部，不会盖住宿主页面

### 方式二：内联（与宿主页面同文档）

适合需要与宿主页面共享滚动/事件的场景。打开 `stamp-sphere-embed.html`，复制三部分：

1. `<style>` 块（全部以 `.ssr-root` 作用域，令牌 `--ssr-` 前缀，不会污染你的样式）
2. 「嵌入片段」HTML（`<div class="ssr-root">…</div>`，文件中有注释标记）
3. 页面底部三个 `<script>`（three.js + 数据 + 应用逻辑）

然后用 CSS 控制容器尺寸，例如：

```css
.ssr-root { height: 640px; }   /* 默认 100vh，内联时建议覆盖 */
```

## 组件特性

- **严格 Fibonacci Sphere**：81 枚单枚邮票均匀分布在正球面
- **黑白 → 彩色**：默认黑白，鼠标悬停渐变恢复彩色
- **点击档案**：点击邮票弹出左图右文档案卡（含同套系缩略图切换）
- **拖拽旋转**（带惯性）· **滚轮推拉** · 深度分层 · 浮动动画
- 支持 `prefers-reduced-motion` 降级
- 移动端自适应

## 注意事项

- 组件约 4.1 MB（81 枚邮票 base64 内联 + three.js 内联），首次加载需下载完整文件
- 依赖 Google Fonts（Noto Serif SC / Space Mono），离线时回退系统字体
- 建议给 iframe 加 `loading="lazy"`，滚动到附近再加载
