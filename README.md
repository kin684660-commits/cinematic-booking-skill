# 🎬 电影感预约官网生成器 · Cinematic Booking Site Skill

> **WorkBuddy × Tencent EdgeOne · AI Prompts & Skills 挑战赛 — Skills 赛道**  
> 作者：田秋虹

---

## 一句话描述

**一个 Skill，覆盖任意行业。**  
输入品牌名 + 行业 + 服务列表，10 分钟生成并部署一套完整的电影感预约官网到 EdgeOne Pages。

---

## 视觉风格（锁死，不随行业变化）

| 元素 | 规格 |
|------|------|
| 背景色 | `#080A0F` 曜石黑 |
| 强调色 | `#C0392B` 信号红 |
| 标题字体 | Bebas Neue（电影感） |
| 正文字体 | DM Sans |
| 圆角 | 2px（极锐利） |
| 动效 | blur淡入 + 上浮，禁止弹跳/旋转 |

---

## 支持行业

租车 · 餐厅 · 美发美容 · 牙科诊所 · 私教健身 · 游艇俱乐部 · 精品酒店 · 律所咨询 · 摄影工作室 · 宠物美容 · **任意服务类行业**

---

## 文件说明

| 文件 | 说明 |
|------|------|
| `SKILL.md` | Skill 主文件，包含完整生成逻辑、行业映射表、视觉规范、Edge Functions 规范 |
| `README.md` | 本文件 |

---

## 触发词示例

```
帮我做一个租车的预约官网，品牌叫"阿陈租车 AChen Drive"，服务有跑车、商务轿车、豪华SUV，在香港广州深圳

给我的餐厅做个官网，叫"夜宴 YeYan"，提供私人包厢、主厨发布会套餐、下午茶，在上海

帮我的私教工作室建站，叫"黑铁 BLACKIRON"，服务有一对一私教、体态评估、营养咨询，在深圳
```

---

## 生成内容

每次运行 Skill，自动生成：

- ✅ 完整 React + Vite + Tailwind 项目结构
- ✅ 9 个 Section（Navbar / Hero / TrustBar / Services / Process / Story / Testimonials / ClosingCTA / Footer）
- ✅ 4 个 Edge Functions（services / booking / site-content / health）
- ✅ KV Storage 存储预约记录
- ✅ 右侧滑入 BookingDrawer 预约表单
- ✅ 自动部署到 EdgeOne Pages，返回预览 URL

---

## 核心设计理念

**风格锁死 × 内容参数化**

`site.ts` 是唯一需要按行业填充的配置文件，其余所有组件完全复用。  
这意味着任何行业都能在同一套视觉语言下生成独特的品牌官网。

---

## 参赛评分对应

| 维度 | 覆盖点 |
|------|--------|
| 网站完整度 (30%) | 完整预约流程：展示 → 选服务 → 填写预约 → 确认 bookingId |
| Skills 质量 (30%) | SKILL.md 规范完整、触发词覆盖广、SITE_CONFIG 参数化设计 |
| 技术深度 (20%) | Edge Functions + KV Storage + Middleware |
| 传播力 (20%) | 通用性强，开发者可直接复用到任意行业 |
