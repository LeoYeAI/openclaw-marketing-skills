# openclaw-marketing-skills

[![Powered by MyClaw.ai](https://img.shields.io/badge/Powered%20by-MyClaw.ai-blue?style=flat-square)](https://myclaw.ai)

> 33个经过实战验证的营销技能，专为OpenClaw代理设计。涵盖CRO、文案、SEO、付费广告、邮件、增长等全场景。

[English](README.md) | [中文](README.zh-CN.md) | [日本語](README.ja.md) | [Français](README.fr.md) | [Deutsch](README.de.md) | [Español](README.es.md) | [Italiano](README.it.md) | [Русский](README.ru.md)

---

## 包含内容

33个skill，覆盖所有主要营销场景：

| 类别 | Skills |
|------|--------|
| **基础** | product-marketing-context |
| **转化优化** | page-cro, signup-flow-cro, onboarding-cro, form-cro, popup-cro, paywall-upgrade-cro |
| **文案内容** | copywriting, copy-editing, cold-email, email-sequence, social-content |
| **SEO** | seo-audit, ai-seo, programmatic-seo, site-architecture, schema-markup, content-strategy |
| **付费广告&数据分析** | paid-ads, ad-creative, ab-test-setup, analytics-tracking |
| **增长&留存** | referral-program, free-tool-strategy, churn-prevention |
| **销售&上市** | revops, sales-enablement, launch-strategy, pricing-strategy, competitor-alternatives |
| **策略** | marketing-ideas, marketing-psychology, lead-magnets |

---

## 安装

### 通过ClawHub（推荐）

```bash
clawhub install MyClaw-AI/openclaw-marketing-skills
```

或安装单个skill：

```bash
clawhub install MyClaw-AI/openclaw-marketing-skills --skill copywriting page-cro
```

### 手动安装

```bash
git clone https://github.com/LeoYeAI/openclaw-marketing-skills.git
cp -r openclaw-marketing-skills/skills/* ~/.agents/skills/
```

---

## 从这里开始

在使用任何其他skill之前，先运行 `product-marketing-context` 创建 `.agents/product-marketing-context.md`。所有33个skill都会自动读取这个文件——你只需描述一次产品。

```
帮我创建产品营销上下文
```

然后自然使用任何skill：

```
优化这个落地页的转化率  → page-cro
给我的SaaS写首页文案    → copywriting
审计我们的SEO           → seo-audit
创建5封欢迎邮件序列     → email-sequence
帮我投Google广告        → paid-ads
```

---

## 致谢

基于 [marketingskills](https://github.com/PlatoTheOne/marketingskills)（由 Corey Haines 创建）转化为OpenClaw AgentSkills格式。

原项目：MIT License。本移植版：MIT License。

---

Powered by [MyClaw.ai](https://myclaw.ai) — 让每个用户都能拥有完整代码控制权的AI个人助理平台。
