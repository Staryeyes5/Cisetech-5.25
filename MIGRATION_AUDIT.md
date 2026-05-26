# 官网 Vue 迁移前盘点

更新时间：2026-05-26

## 结论

当前项目已经有三套页面形态：

- 顶层静态页：完成度最高，建议作为视觉、内容和交互迁移基准。
- `frontend/` Vue 源码：结构清晰，但内容和视觉明显简化，适合作为未来主维护形态。
- `deploy/` 静态页：更像早期/简化部署包，内容与顶层静态页不一致，建议仅作参考，不作为迁移基准。

建议迁移策略：以顶层静态页为准，分阶段迁入 `frontend/src/views` 和公共组件，同时整理外链、占位信息、导航和 SEO。

## 页面基准对照

| 模块 | 顶层静态页 | Vue 当前页面 | deploy 当前页面 | 建议 |
| --- | --- | --- | --- | --- |
| 首页 | `index.html`，完整首页、轮播、核心产品、实力入口、CTA | `Home.vue`，简化版首页 | `deploy/index.html`，简化版首页 | 以顶层 `index.html` 迁入 `Home.vue` |
| 核心产品/业务 | `services.html`，导航叫“核心产品”，含产品矩阵和方案入口 | `Services.vue`，五大业务简化展示 | `deploy/services.html`，五大核心业务 | 需先统一栏目命名：核心产品、核心业务或产品方案 |
| 产品详情 | `business-detail.html`，高价值详情页 | 缺失 | 缺失 | 新增 Vue 路由与页面 |
| 招贤纳士 | `joins.html`，招聘职位、文化、福利、简历表单 | 缺失 | 缺失 | 新增 Vue 路由与页面 |
| 企业实力 | `qualifications.html`，证书、荣誉、客户 logo 墙更完整 | `Qualifications.vue`，简化资质卡片 | `deploy/qualifications.html`，简化版 | 以顶层 `qualifications.html` 迁入 Vue |
| 关于我们 | `about.html`，内容更完整 | `About.vue`，简化版 | `deploy/about.html`，存在 2009/新四板等冲突信息 | 以顶层 `about.html` 为准，并确认年份/上市描述 |
| 联系我们 | `contact.html`，电话、邮箱、地址更具体 | `Contact.vue`，表单只 alert | `deploy/contact.html`，占位联系方式 | 以顶层 `contact.html` 为准，补真实表单提交策略 |

## 当前 Vue 路由缺口

当前 Vue 已有：

- `/`
- `/services`
- `/products`
- `/qualifications`
- `/about`
- `/contact`

建议新增或调整：

- `/business-detail`：承接顶层 `business-detail.html`
- `/joins`：承接顶层 `joins.html`
- `/services` 与 `/products`：需要统一定位。顶层静态页没有独立 `products.html`，而是把核心产品放在 `services.html#products`，但 Vue 和 `deploy/` 有独立产品页。

## 导航需要统一

顶层导航：

- 首页
- 核心产品
- 企业实力
- 招贤纳士
- 关于我们
- 咨询合作

Vue 当前导航：

- 首页
- 核心业务
- 产品方案
- 企业实力
- 关于我们
- 联系我们按钮

建议先确认最终导航文案。保守方案：

- 首页 `/`
- 核心产品 `/services`
- 企业实力 `/qualifications`
- 招贤纳士 `/joins`
- 关于我们 `/about`
- 咨询合作 `/contact`

如果保留“产品方案”栏目，则需要明确 `/products` 与 `/services` 的职责边界。

## 外链资源风险

顶层和 `deploy/` HTML 中存在外部资源依赖，聚合统计如下：

| 域名 | 数量 | 风险 |
| --- | ---: | --- |
| `code.coze.cn` | 157 | 临时/代理资源，正式官网不建议依赖 |
| `coze-coding-project.tos.coze.site` | 30 | 外部对象存储链接，稳定性和权限需确认 |
| `fonts.googleapis.com` | 22 | 国内访问不稳定 |
| `cdn.tailwindcss.com` | 13 | 生产环境不建议使用 CDN runtime Tailwind |
| `images.unsplash.com` | 5 | 第三方图片版权与稳定性需确认 |
| `cdn.jsdelivr.net` / `cdnjs.cloudflare.com` | 3 | 可用但建议统一本地化或锁版本 |

顶层静态页外链数量较多的页面：

| 文件 | 外链数量 | 说明 |
| --- | ---: | --- |
| `qualifications.html` | 138 | 客户 logo 墙大量使用 Coze 代理链接 |
| `business-detail.html` | 30 | 产品详情图和 CDN 较多 |
| `services.html` | 20 | 产品图、Unsplash 和 Coze 链接 |
| `about.html` | 12 | 字体、CDN、少量资源链接 |
| `joins.html` | 10 | 字体、CDN、招聘页图片 |
| `index.html` | 6 | 首页少量外链但包含关键视觉图 |
| `contact.html` | 4 | 较少 |

迁移建议：

- 优先把 `code.coze.cn` 和 `coze-coding-project.tos.coze.site` 图片替换成本地 `assets/` 路径。
- 字体优先使用系统字体，或本地化字体文件。
- Tailwind 使用 `frontend/` 本地构建，不再使用 CDN runtime。
- Unsplash 图片确认版权和业务匹配度，必要时替换为现有企业素材或生成/采购图片。

## 占位和冲突信息

需要确认或修正：

- `deploy/` 中仍有 `400-888-8888`、`contact@cisetech.com`、`上海市浦东新区张江高科技园区`、`沪ICP备XXXXXXXX号` 等占位内容。
- 顶层页面多处页脚链接为 `href="#"`：隐私政策、使用条款、网站地图。
- 顶层首页有若干新闻/详情入口为 `href="#"`，需要确认是否隐藏、删除或补页面。
- 顶层联系页使用 `(021)-6075 6566`、`info@cisetech.com`、`上海市浦东新区国展路1529号906-908室`，应作为候选正式信息，但仍建议人工确认。
- 顶层 `about.html` 使用“2010年、新三板”等描述，`deploy/about.html` 使用“2009年、新四板”，两者冲突。建议以正式工商/官网口径统一。
- Vue `Contact.vue` 表单只弹窗，不提交数据。
- Vue store 默认电话和邮箱仍是 `400-888-8888`、`contact@cisetech.com`。

## SEO 现状

顶层静态页 SEO 信息不完整或不统一：

- `index.html` 有完整 title、description、keywords。
- `services.html` 只有 title，缺 description 和 keywords。
- `business-detail.html` 只有 title，缺 description 和 keywords。
- `joins.html` 有完整 title、description、keywords。
- `qualifications.html` 有完整 title、description、keywords。
- `about.html` 有完整 title、description、keywords。
- `contact.html` 有完整 title、description、keywords。

Vue 当前使用 `@vueuse/head` 和路由 meta，但文案更偏早期简化版。迁移时建议每个路由统一设置：

- `title`
- `description`
- `keywords`
- canonical URL
- Open Graph 标题、描述和图片

如后续仍以 SPA 方式部署，需要评估 SEO；企业官网更建议最终使用预渲染或静态生成方式输出页面。

## 建议迁移顺序

1. 建立迁移分支：`migrate-static-to-vue`
2. 统一最终导航和页面清单。
3. 先迁公共布局：Header、Footer、移动端菜单、页脚链接、返回顶部。
4. 迁首页 `index.html` 到 `Home.vue`，做桌面/移动截图对比。
5. 本地化首页关键视觉图和 logo。
6. 迁 `services.html` 与 `business-detail.html`，明确 `/services`、`/products`、`/business-detail` 的关系。
7. 迁 `qualifications.html`，重点处理客户 logo 墙外链本地化。
8. 迁 `about.html`，统一公司年份、上市描述、企业文化、分支机构。
9. 迁 `joins.html`，职位数据和简历表单先静态化，后续再接后端。
10. 迁 `contact.html`，补真实联系方式和表单提交策略。
11. 清理或归档 `deploy/`，避免维护多套页面。
12. 做全站 SEO、链接、图片加载、移动端显示检查。

## 第一阶段建议任务

建议下一步先做这三个小任务，每个任务单独提交：

1. 创建迁移分支 `migrate-static-to-vue`。
2. 统一 Vue 路由和导航骨架，先新增 `/joins`、`/business-detail` 占位页。
3. 迁移首页公共头部、页脚和首页主体，保持顶层 `index.html` 的视觉基准。

