# 求职助手 · AI 岗位匹配分析

一个**开源、免后端**的求职分析网页框架：填写求职意向（最多三个顺位）与个人经历，AI 自动完成岗位画像、匹配度分析与求职行动建议，生成完整的求职分析报告。

**在线体验：https://unim1012-netizen.github.io/Job-Offer-Assistant/**

> 本项目只提供**框架与示例**，不绑定任何平台账号与额度：
> - **示例预览**：内置一份完整示例报告，零调用、零消耗，开箱即看效果；
> - **自带模型 API**：每个使用者填入自己的 OpenAI 兼容接口 Key 后，才能为 TA 生成专属报告。

## 功能特性

- 求职意向采集：支持「有明确意向 / 还不确定」两种模式；明确意向可填三个顺位（企业类型枚举 + 意向职位），不确定意向只需填写个人经历，由 AI 给出方向建议
- 示例预览模式：内置完整示例报告（岗位画像、匹配度表格、简历/面试建议、行动计划），不调用任何接口、不消耗任何额度
- 自带模型模式：填入自己的 API Key（OpenAI 兼容）即可生成专属报告，费用由你的模型服务商按量计
- Markdown 报告渲染（表格 / 列表 / 标题 / 引用）、一键复制、桌面 / 移动响应式适配

## 工作原理

```
┌─────────────────────────────┐
│  开源网页（单文件 index.html） │
│  GitHub Pages / 任意静态托管 │
└──────────────┬──────────────┘
               │ 示例预览：读取内置示例报告（零网络请求）
               │ 自带模型：浏览器直接调用你填写的 API 地址
               ▼
┌─────────────────────────────┐
│  你自己的 OpenAI 兼容接口     │
│  OpenAI / DeepSeek / Moonshot│
│  智谱 / 豆包火山方舟 …        │
└─────────────────────────────┘
```

- **无服务器**：没有后端、没有代理、没有数据库，浏览器直连模型服务商
- **零额度依赖**：不再依赖任何人的 Coze 积分或云端配额，示例预览完全离线
- **隐私友好**：API Key 仅保存在浏览器本地（localStorage），直接发往你填写的 API 地址，不经过任何第三方服务器

## 快速开始（使用者）

1. 打开在线页面（或本地打开 `index.html`）
2. 点击顶部的「接入设置（模型方式）」，切换到**自带模型 API**
3. 填写三项配置：
   - **API 地址**：如 `https://api.openai.com/v1`（DeepSeek 为 `https://api.deepseek.com/v1`，Moonshot 为 `https://api.moonshot.cn/v1`）
   - **API Key**：你的模型服务商密钥
   - **模型名称**：如 `gpt-4o-mini`、`deepseek-chat`、`moonshot-v1-8k`
4. 点「保存配置」
5. 填写求职意向与个人经历，点击「生成求职分析报告」

> 未配置 Key 时提交会被拦截并引导至设置页；想先看效果可直接使用默认的「示例预览」模式。

## 部署到自己的 GitHub Pages

```bash
# 1. fork 或 clone 本仓库
git clone https://github.com/unim1012-netizen/Job-Offer-Assistant.git
cd Job-Offer-Assistant

# 2. 按需修改 index.html 中的文案与示例内容

# 3. 推送到你的仓库，开启 GitHub Pages（Settings → Pages → 选择 main 分支根目录）
git add index.html README.md
git commit -m "init"
git push origin main
```

也可以把这个 `index.html` 放到任意静态托管（Vercel / Netlify / Cloudflare Pages / 本地）直接使用。

## 支持的模型服务商

支持所有 OpenAI 兼容的 Chat Completions 接口：OpenAI、DeepSeek、Moonshot（月之暗面）、智谱 GLM、豆包火山方舟（需开启兼容端点）、Ollama 本地模型等。

> 提示：部分服务商（如火山方舟）默认限制浏览器跨域，可能需要使用其官方兼容代理地址或自建轻量转发；OpenAI / DeepSeek / Moonshot 等可直接在浏览器调用。

## 目录结构

```
├── index.html      # 单文件网页应用（含样式、逻辑、内置示例报告）
├── README.md       # 本说明
└── _shots/         # 本地自检截图（非交付物）
```

## 隐私与安全

- API Key 只写入浏览器 localStorage，不上传任何服务器，关闭页面后仍保留（可清除浏览器数据抹除）
- 请求直接从浏览器发往你填写的 API 地址，本项目不记录、不中转任何内容
- 纯大模型无法联网，报告中的岗位画像与匹配分析基于行业通用知识生成，不含实时在招岗位信息
