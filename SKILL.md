---
name: cinematic-booking-site
description: >
  Generate a cinematic dark-luxury booking website for ANY industry and brand.
  One sentence trigger → full-stack appointment/booking site deployed to EdgeOne Pages.
  Style is always: obsidian black, signal red accents, Bebas Neue display font, film-title
  aesthetic — only the industry content, services, copy, and imagery change.
  Supports restaurants, car rentals, salons, clinics, gyms, yacht clubs, hotels,
  law firms, photography studios, pet grooming, and any other service business.
triggers:
  - "帮我做一个XX的预约官网"
  - "给我的XX店做一个官网"
  - "build a booking site for my"
  - "做一个XX行业的展示站"
  - "帮我生成一个预约网站"
  - "cinematic booking site for"
  - "做个官网"
  - "帮我建站"
  - "XX预约系统"
version: "1.0.0"
author: "田秋虹"
competition: "WorkBuddy × Tencent EdgeOne AI Prompts × Skills 挑战赛 — Skills 赛道"
---

# 电影感预约官网生成器 · Cinematic Booking Site Skill

## 概述

本 Skill 为**任意行业、任意品牌**生成一套完整的电影感预约官网，并自动部署到 EdgeOne Pages。

风格永远锁定为：
- 曜石黑背景 `#080A0F`
- 信号红点缀 `#C0392B`
- Bebas Neue 电影标题字体
- 电影感暗黑美学，像一个好莱坞片头序列

只有这些内容随行业变化：
- 品牌名 / Slogan
- 服务项目列表
- 流程步骤名称
- Hero 背景图（从 Unsplash 按行业关键词选取）
- 文案语气（餐厅温暖、健身有力、医疗专业……）

---

## 第一步：读取 EdgeOne Pages 官方能力

```
Install this skill: https://github.com/TencentEdgeOne/edgeone-pages-skills
```

---

## 第二步：信息采集

用户触发本 Skill 后，AI 必须先收集以下信息（如用户未提供则逐一询问）：

```
REQUIRED:
  brand_name:     品牌名称（中文 + 英文，如"阿陈租车 · AChen Drive"）
  industry:       行业类型（见下方行业映射表）
  tagline_cn:     中文 Slogan（如用户没有，AI 自动生成）
  tagline_en:     英文 Slogan（AI 自动生成）
  services:       服务项目列表（3-6项，含名称+简介+价格，价格可选）
  location:       城市/地区（用于信任栏和页脚）
  contact:        联系方式（电话或微信，可选）
  cta_action:     预约动作名称（如"立即预约""在线订座""免费咨询"）
```

---

## 第三步：行业映射表

根据 `industry` 字段，AI 自动映射以下参数：

| industry 值 | 行业 | Hero图关键词 | Story图关键词 | 流程动词 | 服务单位 |
|------------|------|------------|-------------|---------|--------|
| `car_rental` | 租车 | `luxury car night city` | `road tunnel lights` | 驾驶 Drive | 天/day |
| `restaurant` | 餐厅 | `fine dining dark restaurant` | `chef kitchen dark` | 订座 Reserve | 位/人 |
| `salon` | 美发/美容 | `luxury hair salon dark` | `barber scissors dark` | 预约 Book | 次/session |
| `dental` | 牙科诊所 | `modern dental clinic dark` | `dentist tools clean` | 咨询 Consult | 次/visit |
| `gym` | 健身私教 | `dark gym weights` | `personal trainer dark` | 开始 Start | 节/session |
| `yacht` | 游艇俱乐部 | `luxury yacht night sea` | `yacht deck sunset` | 出海 Sail | 天/day |
| `hotel` | 精品酒店 | `luxury hotel dark lobby` | `hotel suite night` | 入住 Check In | 晚/night |
| `law` | 律所/咨询 | `dark law office city` | `lawyer desk night` | 咨询 Consult | 次/session |
| `photography` | 摄影工作室 | `dark photography studio` | `camera lens dark` | 拍摄 Shoot | 次/session |
| `pet` | 宠物美容/寄养 | `cute pet dark studio` | `pet grooming professional` | 预约 Book | 次/session |
| `other` | 其他 | `luxury dark service` | `professional dark office` | 预约 Book | 次/session |

Unsplash URL 模板：
```
https://images.unsplash.com/photo-1{PHOTO_ID}?w=1920&q=85
```

AI 根据关键词从以下预选图库中匹配（按行业关键词选最合适的）：

```yaml
car_rental_hero:    "https://images.unsplash.com/photo-1492144534655-ae79c964c9d7?w=1920&q=85"
restaurant_hero:    "https://images.unsplash.com/photo-1514190051997-0f6f39ca5cde?w=1920&q=85"
salon_hero:         "https://images.unsplash.com/photo-1560066984-138dadb4c035?w=1920&q=85"
dental_hero:        "https://images.unsplash.com/photo-1629909613654-28e377c37b09?w=1920&q=85"
gym_hero:           "https://images.unsplash.com/photo-1534438327276-14e5300c3a48?w=1920&q=85"
yacht_hero:         "https://images.unsplash.com/photo-1567899378494-47b22a2ae96a?w=1920&q=85"
hotel_hero:         "https://images.unsplash.com/photo-1542314831-068cd1dbfeeb?w=1920&q=85"
law_hero:           "https://images.unsplash.com/photo-1589829545856-d10d557cf95f?w=1920&q=85"
photography_hero:   "https://images.unsplash.com/photo-1452587925148-ce544e77e70d?w=1920&q=85"
pet_hero:           "https://images.unsplash.com/photo-1516734212186-a967f81ad0d7?w=1920&q=85"
story_tunnel:       "https://images.unsplash.com/photo-1540655037529-dec987208707?w=1920&q=85"
closing_city:       "https://images.unsplash.com/photo-1536599018102-9f803c140fc1?w=1920&q=85"
```

---

## 第四步：项目结构生成

```
{brand_slug}/
├── package.json
├── vite.config.ts
├── tailwind.config.ts
├── tsconfig.json
├── index.html
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   ├── config/
│   │   └── site.ts              ← ⭐ 唯一需要改动的配置文件
│   ├── components/
│   │   ├── Navbar.tsx
│   │   ├── HeroSection.tsx
│   │   ├── TrustBar.tsx
│   │   ├── ServicesSection.tsx  ← 原"车队"，改名为"服务"
│   │   ├── ProcessSection.tsx
│   │   ├── StorySection.tsx
│   │   ├── TestimonialsSection.tsx
│   │   ├── ClosingCTASection.tsx
│   │   ├── BookingDrawer.tsx
│   │   ├── BackgroundMedia.tsx
│   │   ├── SectionBadge.tsx
│   │   └── CinemaButton.tsx
│   └── lib/
│       └── api.ts
└── functions/
    ├── api/
    │   ├── services.ts          ← 返回服务列表
    │   ├── booking.ts           ← 处理预约提交
    │   ├── site-content.ts      ← 返回品牌文案
    │   └── health.ts
    └── middleware.ts
```

---

## 第五步：核心配置文件 `src/config/site.ts`

这是整个 Skill 的**唯一变量**。每次生成新行业，只需填充这个文件：

```typescript
// src/config/site.ts
// ⭐ 这是唯一需要按行业定制的文件，其他组件全部复用

export const SITE_CONFIG = {
  // 品牌
  brand: {
    name_cn: "{{brand_name_cn}}",       // e.g. "阿陈租车"
    name_en: "{{brand_name_en}}",       // e.g. "AChen Drive"
    tagline_cn: "{{tagline_cn}}",       // e.g. "每一段路，都值得被记住。"
    tagline_en: "{{tagline_en}}",       // e.g. "Every road deserves to be remembered."
    since: "{{since_year}}",            // e.g. "2008"
    location: "{{location}}",          // e.g. "香港 · 广州 · 深圳 · 澳门"
  },

  // CTA 动作文字
  cta: {
    primary_cn: "{{cta_cn}}",          // e.g. "立即选车"
    primary_en: "{{cta_en}}",          // e.g. "Choose Your Car"
    book_cn: "{{book_cn}}",            // e.g. "预约驾驶"
    book_en: "{{book_en}}",            // e.g. "Book"
    nav_cta_cn: "立即预约",
    nav_cta_en: "Book Now",
  },

  // 导航（固定结构，文字随行业微调）
  nav: [
    { cn: "服务", en: "Services" },
    { cn: "流程", en: "Process" },
    { cn: "故事", en: "Story" },
    { cn: "联系", en: "Contact" },
  ],

  // Hero
  hero: {
    headline_line1: "{{headline_line1}}",  // e.g. "每一段路"
    headline_line2: "{{headline_line2}}",  // e.g. "都值得被记住"
    subheadline_en: "{{subheadline_en}}", // e.g. "Every road deserves to be remembered."
    badge: "SINCE {{since_year}} · {{location_short}}",
    bottom_strip: "{{location}}",
  },

  // 信任栏（AI 根据行业生成合适的媒体/认证名称）
  trust: {
    label_cn: "信任我们的旅程",
    label_en: "Trusted by",
    items: ["{{trust_1}}", "{{trust_2}}", "{{trust_3}}", "{{trust_4}}", "{{trust_5}}"],
  },

  // 服务列表（替代"车队"）
  services: {
    badge_cn: "我们的服务",
    badge_en: "Our Services",
    heading_cn: "{{services_heading_cn}}",  // e.g. "为每种旅程，备好每种机器"
    heading_en: "{{services_heading_en}}",  // e.g. "A machine for every journey."
    items: [
      // AI 根据用户提供的服务填充，3-6项
      {
        id: "{{service_id}}",
        name_cn: "{{service_name_cn}}",
        name_en: "{{service_name_en}}",
        tag_cn: "{{tag_cn}}",
        tag_en: "{{tag_en}}",
        description: "{{description}}",
        price: "{{price}}",             // e.g. "¥2,800 / 天"，可选
        image: "{{unsplash_url}}",
      }
    ],
  },

  // 预约流程（4步，随行业调整动词）
  process: {
    badge_cn: "如何预约",
    badge_en: "How It Works",
    heading_cn: "{{process_heading_cn}}",  // e.g. "四步上路" / "三步搞定" / "四步预约"
    heading_en: "{{process_heading_en}}",
    steps: [
      { num: "01", icon: "{{icon_1}}", title_cn: "{{step1_cn}}", body_cn: "{{step1_body}}" },
      { num: "02", icon: "{{icon_2}}", title_cn: "{{step2_cn}}", body_cn: "{{step2_body}}" },
      { num: "03", icon: "{{icon_3}}", title_cn: "{{step3_cn}}", body_cn: "{{step3_body}}" },
      { num: "04", icon: "{{icon_4}}", title_cn: "{{step4_cn}}", body_cn: "{{step4_body}}" },
    ],
  },

  // 品牌故事
  story: {
    badge_cn: "关于我们",
    badge_en: "Our Story",
    headline_line1: "{{story_line1}}",    // e.g. "不只是租车"
    headline_line2: "{{story_line2}}",    // e.g. "是一种态度"
    headline_en: "{{story_en}}",
    body: "{{story_body}}",              // 3-4句品牌故事，AI 生成
  },

  // 客户评价（AI 生成3条符合行业语气的评价）
  testimonials: [
    { quote: "{{quote_1}}", name: "{{name_1}}", location: "{{city_1}}" },
    { quote: "{{quote_2}}", name: "{{name_2}}", location: "{{city_2}}" },
    { quote: "{{quote_3}}", name: "{{name_3}}", location: "{{city_3}}" },
  ],

  // 结尾 CTA
  closing: {
    headline_cn: "{{closing_cn}}",       // e.g. "准备好了吗"
    headline_en: "{{closing_en}}",       // e.g. "Ready to drive?"
    body_cn: "{{closing_body}}",
  },

  // 图片资源
  images: {
    hero: "{{hero_image_url}}",
    story: "{{story_image_url}}",
    closing: "{{closing_image_url}}",
    services: ["{{service_img_1}}", "{{service_img_2}}", "{{service_img_3}}"],
  },

  // 预约表单字段（随行业微调）
  booking_form: {
    fields: [
      { id: "name",     label_cn: "姓名",   type: "text" },
      { id: "phone",    label_cn: "电话",   type: "tel" },
      { id: "date",     label_cn: "日期",   type: "date" },
      { id: "service",  label_cn: "服务项目", type: "select", options: "from services" },
      { id: "note",     label_cn: "备注",   type: "textarea", required: false },
    ],
  },
}
```

---

## 第六步：视觉规范（锁死，不随行业变化）

### 色彩系统
```css
:root {
  --background: 220 20% 4%;        /* #080A0F 曜石黑 */
  --foreground: 40 10% 96%;        /* #F5F5F0 纯白文字 */
  --primary: 0 55% 47%;            /* #C0392B 信号红 */
  --primary-foreground: 0 0% 98%;
  --muted-foreground: 220 8% 60%;  /* 哑光灰文字 */
  --border: 220 12% 80% / 0.10;
  --card: 220 16% 8%;              /* #111318 碳纤维深灰 */
  --radius: 2px;                    /* 极小圆角，锐利感 */
}
```

### 字体系统
```js
fontFamily: {
  display: ["Bebas Neue", "sans-serif"],   // 电影标题
  body:    ["DM Sans", "sans-serif"],       // 正文
  mono:    ["Space Mono", "monospace"],     // 标签/价格/数据
}
```

### 组件规范
```css
.cinema-glass {
  background: rgba(255,255,255,0.03);
  backdrop-filter: blur(12px) saturate(110%);
  border: 1px solid rgba(255,255,255,0.07);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.06),
              0 20px 60px rgba(0,0,0,0.35);
}

.cinema-glass-strong {
  background: rgba(255,255,255,0.05);
  backdrop-filter: blur(20px) saturate(120%);
  border: 1px solid rgba(255,255,255,0.12);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.10),
              0 30px 80px rgba(0,0,0,0.45);
}
```

### 动效规范（framer-motion，锁死）
- 页面入场：`blur(8px)→blur(0)` + `opacity 0→1`，时长 1.2s，不超过 1.5s
- 内容上浮：`translateY(20px)→0` + fade，延迟 stagger 0.15s
- 卡片 hover：`scale(1.02)`，`transition 0.3s ease`
- **禁止**：bounce、spring、弹性物理动效、旋转动效

---

## 第七步：固定页面结构（9个 Section，结构锁死）

```
Section 1  Navbar          固定顶部导航（透明→滚动变暗）
Section 2  Hero            全屏电影感首屏（行业背景图+大标题）
Section 3  Trust Bar       信任背书条（行业相关媒体/认证）
Section 4  Services        服务展示网格（替代"车队"）
Section 5  Process         预约流程四步
Section 6  Story           品牌故事（行业叙事）
Section 7  Testimonials    客户评价三列
Section 8  Closing CTA     结尾召唤+城市夜景
Footer                     版权+链接
```

---

## 第八步：Edge Functions 规范

每个生成的站点包含以下 4 个 Edge Functions：

### `functions/api/services.ts` — GET
返回服务列表（从 SITE_CONFIG 生成）：
```json
[
  {
    "id": "string",
    "name_cn": "string",
    "name_en": "string",
    "tag": "string",
    "description": "string",
    "price": "string",
    "image": "string"
  }
]
```

### `functions/api/booking.ts` — POST
接收预约请求：
```json
{ "name": "", "phone": "", "date": "", "service": "", "note": "" }
```
验证后返回：
```json
{
  "success": true,
  "bookingId": "BK-xxxxxx",
  "message": "预约成功！我们将在24小时内与您联系确认。"
}
```
同时用 KV Storage 存储预约记录：
```typescript
await KV.put(`booking:${bookingId}`, JSON.stringify(data), { expirationTtl: 86400 * 30 })
```

### `functions/api/site-content.ts` — GET
返回 nav、footer、testimonials、brand info。

### `functions/api/health.ts` — GET
返回 `{ "ok": true }`

---

## 第九步：BookingDrawer 规范（锁死）

所有行业共用同一套 Drawer 组件，只有字段 label 和 service 选项随行业变化：

- 从右侧滑入（framer-motion `x: '100%' → 0`）
- `cinema-glass-strong` 样式
- 顶部：已选服务名称 + 价格
- 表单字段从 `SITE_CONFIG.booking_form.fields` 渲染
- 提交 → POST `/api/booking`
- 成功：显示 bookingId + 成功提示（红色对勾）
- 失败：内联错误提示
- 关闭按钮右上角，ESC 关闭

---

## 第十步：部署

```bash
npm install
npm run dev        # 本地验证

# 触发 edgeone-pages-deploy Skill
Deploy this project to EdgeOne Pages
```

---

## 行业生成示例

### 示例 1：租车（已验证）
```
触发词: 帮我做一个租车的预约官网，品牌叫"阿陈租车 AChen Drive"，
       服务有跑车、商务轿车、豪华SUV，在香港广州深圳
```

### 示例 2：高级餐厅
```
触发词: 给我的餐厅做个官网，叫"夜宴 YeYan"，
       提供私人包厢、主厨发布会套餐、下午茶，在上海
```

生成结果差异：
- Hero：暗色高级餐厅背景
- Services：包厢/套餐/茶，含人均价格
- Process：01选桌型 → 02选菜单 → 03扫码预付 → 04到店入座
- Story：主厨/食材/料理哲学
- Testimonials：食客评价语气

### 示例 3：私教健身
```
触发词: 帮我的私教工作室建站，叫"黑铁 BLACKIRON"，
       服务有一对一私教、体态评估、营养咨询，在深圳
```

生成结果差异：
- Hero：暗色健身房，力量感背景图
- Services：私教课/评估/咨询，含每节价格
- Process：01免费评估 → 02制定方案 → 03扫码预付 → 04开始训练
- Story：教练背景/训练理念
- Testimonials：学员蜕变语气

---

## 验收清单

每次生成后验证：

- [ ] 所有 9 个 Section 正常渲染
- [ ] SITE_CONFIG 中无 `{{placeholder}}` 残留
- [ ] Services 卡片从 `/api/services` 加载，loading skeleton 正常
- [ ] Booking Drawer 提交成功，返回 bookingId
- [ ] KV Storage 写入预约记录
- [ ] Hero 背景图正确对应行业
- [ ] 移动端 390px 无溢出
- [ ] 所有文案为目标行业语气（餐厅温暖、健身有力、医疗专业）
- [ ] EdgeOne Pages 部署成功，返回完整预览 URL

---

## 参赛信息

```
赛道：Skills 赛道
作品名称：电影感预约官网生成器 · Cinematic Booking Site Skill
参赛者：田秋虹
核心价值：一个 Skill，覆盖任意行业，无限复用
          风格锁死（暗黑电影感）× 内容参数化（行业+品牌+服务）
          = 10分钟从零到上线任何行业的预约官网

评分覆盖：
  ✅ 网站完整度 (30%)  — 完整预约流程：展示→选择→预约→确认
  ✅ Skills质量 (30%)  — SKILL.md规范、触发词覆盖广、SITE_CONFIG参数化设计
  ✅ 技术深度 (20%)    — Edge Functions + KV Storage（存预约记录）+ Middleware
  ✅ 传播力 (20%)      — 通用性强，任何行业都能用，开发者社区传播价值高
```
