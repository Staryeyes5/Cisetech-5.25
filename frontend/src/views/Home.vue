<template>
  <div class="home-page">
    <section class="hero-section">
      <div class="hero-bg" aria-hidden="true">
        <img :src="heroImage" alt="" />
      </div>
      <div class="hero-grid" aria-hidden="true"></div>
      <div class="container">
        <div class="hero-content">
          <p class="hero-kicker">Cisetech</p>
          <h1 class="hero-title">申朴AI・智创无限</h1>
          <p class="hero-subtitle">AI 聚力数转智改，创领智能新生态</p>
          <div class="hero-actions">
            <router-link to="/services" class="primary-action">探索核心产品</router-link>
            <router-link to="/contact" class="secondary-action">立即咨询</router-link>
          </div>
        </div>
      </div>
    </section>

    <section class="business-section section-dark" id="services">
      <div class="container">
        <div class="section-heading">
          <h2>核心业务</h2>
          <p>全栈AI能力，赋能企业智能化转型</p>
        </div>

        <div class="business-grid">
          <article v-for="item in businessModules" :key="item.title" class="business-card">
            <div class="business-card-header">
              <div class="business-icon" :style="{ '--accent': item.accent }"></div>
              <h3>{{ item.title }}</h3>
            </div>
            <div class="business-items">
              <div v-for="entry in item.items" :key="entry.title" class="business-item">
                <h4>{{ entry.title }}</h4>
                <p>{{ entry.text }}</p>
              </div>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section class="products-section section-dark" id="products">
      <div class="container">
        <div class="section-heading">
          <h2>核心产品方案</h2>
          <p>基于核心技术研发的标准化产品与代理产品，满足多样化业务场景需求</p>
        </div>

        <div class="product-grid">
          <article v-for="product in products" :key="product.id" class="product-card">
            <router-link :to="`/business-detail#${product.id}`" class="product-media">
              <img :src="product.image" :alt="product.name" />
              <span class="product-badge">{{ product.badge }}</span>
            </router-link>
            <div class="product-body">
              <p class="product-category">{{ product.category }}</p>
              <h3>{{ product.name }}</h3>
              <p>{{ product.description }}</p>
              <router-link :to="`/business-detail#${product.id}`" class="product-link">
                了解详情
              </router-link>
            </div>
          </article>

          <article class="product-card product-card-more">
            <div class="more-icon">+</div>
            <h3>需要定制化产品？</h3>
            <p>围绕业务场景、数据基础、算力环境和交付模式，为企业定制产品组合。</p>
            <router-link to="/services#products" class="primary-action compact">查看全部产品</router-link>
          </article>
        </div>
      </div>
    </section>

    <section class="strength-section section-dark" id="strength">
      <div class="container">
        <div class="section-heading">
          <h2>企业实力</h2>
          <p>资质、客户、技术与交付能力共同支撑长期服务</p>
        </div>

        <div class="strength-grid">
          <router-link
            v-for="item in strengths"
            :key="item.title"
            :to="item.to"
            class="strength-card"
          >
            <span class="strength-number">{{ item.value }}</span>
            <h3>{{ item.title }}</h3>
            <p>{{ item.text }}</p>
          </router-link>
        </div>
      </div>
    </section>

    <section class="cta-section">
      <div class="container">
        <div class="cta-panel">
          <p>专业团队，AI赋能</p>
          <h2>为您的企业打造智能化解决方案</h2>
          <div class="cta-actions">
            <router-link to="/contact" class="primary-action">立即咨询</router-link>
            <router-link to="/about" class="secondary-action">了解申朴</router-link>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { useHead } from '@vueuse/head'

import heroImage from '../../../assets/backgrounds/背景图球.png'
import simpleInsightImage from '../../../assets/projects/unnamed 2.png'
import aiRecruitImage from '../../../assets/projects/unnamed 9.png'
import aiBiddingImage from '../../../assets/projects/招投标助手.jpg'
import muxiGpuImage from '../../../assets/projects/unnamed 3.png'
import healthImage from '../../../assets/projects/gmyl.jpeg'
import oceanBaseImage from '../../../assets/projects/OceanBase2.png'
import sqlAuditImage from '../../../assets/backgrounds/sql-audit-platform.jpeg'
import lowAltitudeImage from '../../../assets/backgrounds/低空经济bg.png'

useHead({
  title: 'Cisetech - 申朴AI・智创无限',
  meta: [
    {
      name: 'description',
      content: '申朴信息技术（上海）股份有限公司 - 国内领先的金融科技与企业数字化转型解决方案服务商，AI驱动企业智能化升级'
    },
    {
      name: 'keywords',
      content: 'Cisetech,申朴信息,金融科技,数字化转型,AI赋能,信创'
    }
  ]
})

const businessModules = [
  {
    title: '战略咨询和规划',
    accent: '#22d3ee',
    items: [
      {
        title: '顶层设计',
        text: 'AI环境下IT管理规划、IT治理、降本增效、AI原生开发平台、应用场景设计'
      },
      {
        title: '应用模式',
        text: '业务流程咨询、系统方案、产品设计、技术架构'
      },
      {
        title: '技术选型',
        text: '开发架构、运维架构、算力架构、安全架构、Agent架构、知识库构建'
      }
    ]
  },
  {
    title: '解决方案',
    accent: '#a78bfa',
    items: [
      {
        title: '算力供给与集群管理',
        text: '算力租赁/供给、算力资源管理、混合算力架构设计'
      },
      {
        title: '数据加工',
        text: '多模态数据标注、数据采集、数据治理'
      },
      {
        title: '企业级Open Claw应用部署',
        text: '基于K8s容器化、高可用、可管控的智能体平台，把大模型变成可落地、可运维、可安全合规的企业级系统'
      },
      {
        title: '模型训练',
        text: '代码小模型、领域模型训练、Agent调优'
      }
    ]
  },
  {
    title: '产品',
    accent: '#34d399',
    items: [
      {
        title: 'AI方向',
        text: 'AI辅助编程工具、AI招聘、招投标助手、各类场景AI Agent、智安AI Agent安全验证平台'
      },
      {
        title: '大数据管理与应用方向',
        text: '数据资产治理与可视化平台、长尾客户营销'
      },
      {
        title: '国产信创方向',
        text: 'SQL AI Review、Bettle、Carn、Data Bus，以及企业应用鸿蒙化架构与实施方案'
      },
      {
        title: '客户体验方向',
        text: 'Simple Insight 一体化智能可观测平台'
      }
    ]
  },
  {
    title: '人力资源配置与服务',
    accent: '#fbbf24',
    items: [
      {
        title: 'AI基建',
        text: '标注、审核、模型训练、AI人才培训等'
      },
      {
        title: '技术人员供给',
        text: '人工智能、软件研发、大数据、区块链、物联网、网络与数据安全等技术开发、测试、运维'
      },
      {
        title: '业务流程人员供给',
        text: '呼叫中心、客服、外呼、催收、标注、审核、运营、金融后台服务'
      },
      {
        title: '用工配置与交付模式',
        text: '劳务派遣、灵活用工、HRO、RPO，在岸、离岸、全职、兼职等'
      }
    ]
  }
]

const products = [
  {
    id: 'product-simple-insight',
    name: 'Simple Insight 一体化智能可观测平台',
    category: '本地私有化部署',
    badge: '本地私有化部署',
    description: '集成全栈链路监控、智能异常检测与自动化响应，本地私有化部署为企业提供全方位安全护航。',
    image: simpleInsightImage
  },
  {
    id: 'product-ai-recruit',
    name: '智能招聘系统',
    category: '智能人力资源',
    badge: '智能人力资源',
    description: '重塑人才招聘流程，通过简历智能解析与初筛，提升招聘效率。',
    image: aiRecruitImage
  },
  {
    id: 'product-ai-bidding',
    name: 'AI 招投标助手',
    category: '智慧办公',
    badge: '智慧办公',
    description: '自动化采集标讯信息、分析招标需求，一键生成合规应标文件。',
    image: aiBiddingImage
  },
  {
    id: 'product-muxi-gpu',
    name: '国产通用 GPU',
    category: '国产算力底座',
    badge: '国产算力底座',
    description: '专为大规模AI计算设计，支持通用计算与图形渲染。',
    image: muxiGpuImage
  },
  {
    id: 'product-ai-health',
    name: '职场健康加油站',
    category: '职场健康管理',
    badge: '职场健康管理',
    description: '专注企业职工健康管理，提供健康监测、智能评估与个性化干预服务。',
    image: healthImage
  },
  {
    id: 'product-oceanbase',
    name: 'OceanBase 数据库',
    category: '企业级数据库',
    badge: '企业级数据库',
    description: '原生分布式数据库，为金融、政务、电信等关键行业提供高可用、高性能、高安全的数据基础设施解决方案。',
    image: oceanBaseImage
  },
  {
    id: 'product-sql-audit',
    name: '申朴 SQL 代码审计平台',
    category: '数据库安全',
    badge: '数据库安全',
    description: '面向企业数据库安全的专业化静态代码检测产品，精准识别SQL注入、权限越权、数据泄露等高风险问题。',
    image: sqlAuditImage
  },
  {
    id: 'product-low-altitude',
    name: '低空综合管理服务平台',
    category: '智慧城市·低空经济',
    badge: '低空经济',
    description: '面向低空飞行管理领域，支持任务全生命周期管理、数据智能生成和多场景业务协同。',
    image: lowAltitudeImage
  }
]

const strengths = [
  {
    value: 'CMMI 5',
    title: '高成熟度交付能力',
    text: '以体系化过程管理支撑复杂项目交付。',
    to: '/qualifications#honors'
  },
  {
    value: 'ISO',
    title: '多项管理体系认证',
    text: '覆盖质量、信息安全、服务管理与业务连续性。',
    to: '/qualifications#qualifications'
  },
  {
    value: '25+',
    title: '全国服务网络',
    text: '总部上海，辐射多地客户交付与服务需求。',
    to: '/about#branches'
  },
  {
    value: '500+',
    title: '专业团队',
    text: '汇聚研发、测试、运维、数据、AI与项目管理人才。',
    to: '/joins'
  }
]
</script>

<style scoped lang="scss">
.home-page {
  min-height: 100vh;
  background: #020617;
  color: #e2e8f0;
}

.hero-section {
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  overflow: hidden;
  padding: 140px 0 80px;
  background:
    radial-gradient(circle at 68% 42%, rgba(14, 165, 233, 0.2), transparent 34%),
    linear-gradient(135deg, #020617 0%, #07111f 48%, #0f172a 100%);
}

.hero-bg {
  position: absolute;
  inset: 0;
  opacity: 0.68;
  pointer-events: none;

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
    filter: saturate(1.08);
  }
}

.hero-bg::after {
  content: '';
  position: absolute;
  inset: 0;
  background:
    linear-gradient(90deg, rgba(2, 6, 23, 0.92) 0%, rgba(2, 6, 23, 0.72) 45%, rgba(2, 6, 23, 0.35) 100%),
    linear-gradient(0deg, #020617 0%, transparent 34%);
}

.hero-grid {
  position: absolute;
  inset: 0;
  opacity: 0.18;
  background-image:
    linear-gradient(rgba(34, 211, 238, 0.22) 1px, transparent 1px),
    linear-gradient(90deg, rgba(34, 211, 238, 0.22) 1px, transparent 1px);
  background-size: 64px 64px;
  pointer-events: none;
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 780px;
}

.hero-kicker {
  color: #22d3ee;
  font-weight: 900;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  margin-bottom: 1rem;
}

.hero-title {
  font-size: clamp(3rem, 8vw, 7rem);
  line-height: 0.98;
  font-weight: 950;
  color: white;
  margin-bottom: 1.5rem;
  text-shadow: 0 0 36px rgba(34, 211, 238, 0.38);
}

.hero-subtitle {
  font-size: clamp(1.2rem, 2.5vw, 2rem);
  color: #cbd5e1;
  margin-bottom: 2rem;
  max-width: 680px;
}

.hero-actions,
.cta-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.primary-action,
.secondary-action {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 48px;
  padding: 0.85rem 1.25rem;
  border-radius: 8px;
  font-weight: 800;
  text-decoration: none;
  transition: transform 0.25s ease, border-color 0.25s ease, background 0.25s ease;
}

.primary-action {
  color: #020617;
  background: linear-gradient(135deg, #22d3ee, #38bdf8);
}

.secondary-action {
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.28);
  background: rgba(15, 23, 42, 0.5);
}

.primary-action:hover,
.secondary-action:hover {
  transform: translateY(-2px);
}

.compact {
  min-height: 42px;
  padding: 0.7rem 1rem;
}

.section-dark {
  position: relative;
  padding: 96px 0;
  background:
    radial-gradient(circle at 16% 10%, rgba(14, 165, 233, 0.12), transparent 26%),
    #020617;
}

.section-heading {
  text-align: center;
  margin-bottom: 3rem;
}

.section-heading h2 {
  font-size: clamp(2.2rem, 4vw, 3.75rem);
  color: white;
  font-weight: 900;
  margin-bottom: 0.75rem;
}

.section-heading p {
  color: #94a3b8;
  font-size: 1.12rem;
  max-width: 780px;
  margin: 0 auto;
}

.business-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1.5rem;
}

.business-card,
.product-card,
.strength-card,
.cta-panel {
  border: 1px solid rgba(148, 163, 184, 0.18);
  background: rgba(15, 23, 42, 0.72);
  box-shadow: 0 20px 48px rgba(0, 0, 0, 0.24);
  backdrop-filter: blur(16px);
  border-radius: 8px;
}

.business-card {
  padding: 1.5rem;
}

.business-card-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.25rem;
}

.business-icon {
  width: 42px;
  height: 42px;
  border-radius: 8px;
  background:
    linear-gradient(135deg, color-mix(in srgb, var(--accent) 35%, transparent), rgba(15, 23, 42, 0.2));
  border: 1px solid color-mix(in srgb, var(--accent) 40%, transparent);
}

.business-card h3 {
  color: white;
  font-size: 1.35rem;
  font-weight: 850;
}

.business-items {
  display: grid;
  gap: 0.95rem;
}

.business-item h4 {
  color: #22d3ee;
  font-size: 1rem;
  margin-bottom: 0.35rem;
  font-weight: 750;
}

.business-item p {
  color: #94a3b8;
  line-height: 1.7;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1.5rem;
}

.product-card {
  overflow: hidden;
}

.product-media {
  position: relative;
  display: block;
  aspect-ratio: 16 / 10;
  overflow: hidden;
  background: #0f172a;
}

.product-media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.45s ease;
}

.product-card:hover .product-media img {
  transform: scale(1.05);
}

.product-badge {
  position: absolute;
  top: 0.85rem;
  left: 0.85rem;
  padding: 0.35rem 0.55rem;
  border-radius: 6px;
  color: #020617;
  background: #22d3ee;
  font-size: 0.76rem;
  font-weight: 850;
}

.product-body {
  padding: 1.25rem;
}

.product-category {
  color: #38bdf8;
  font-size: 0.86rem;
  font-weight: 800;
  margin-bottom: 0.6rem;
}

.product-body h3,
.product-card-more h3 {
  color: white;
  font-size: 1.2rem;
  font-weight: 850;
  margin-bottom: 0.75rem;
}

.product-body p,
.product-card-more p {
  color: #94a3b8;
  line-height: 1.65;
  margin-bottom: 1rem;
}

.product-link {
  color: #22d3ee;
  font-weight: 800;
  text-decoration: none;
}

.product-card-more {
  min-height: 100%;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-start;
}

.more-icon {
  width: 54px;
  height: 54px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  margin-bottom: 1rem;
  color: #22d3ee;
  border: 1px solid rgba(34, 211, 238, 0.4);
  font-size: 2rem;
  font-weight: 300;
}

.strength-grid {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 1rem;
}

.strength-card {
  padding: 1.5rem;
  text-decoration: none;
  color: inherit;
  transition: transform 0.25s ease, border-color 0.25s ease;
}

.strength-card:hover {
  transform: translateY(-4px);
  border-color: rgba(34, 211, 238, 0.45);
}

.strength-number {
  display: block;
  color: #22d3ee;
  font-size: 2rem;
  font-weight: 950;
  margin-bottom: 1rem;
}

.strength-card h3 {
  color: white;
  font-weight: 850;
  margin-bottom: 0.65rem;
}

.strength-card p {
  color: #94a3b8;
  line-height: 1.65;
}

.cta-section {
  padding: 96px 0;
  background:
    radial-gradient(circle at 50% 0%, rgba(34, 211, 238, 0.18), transparent 30%),
    #020617;
}

.cta-panel {
  text-align: center;
  padding: clamp(2rem, 5vw, 4rem);
}

.cta-panel p {
  color: #22d3ee;
  font-weight: 850;
  margin-bottom: 0.75rem;
}

.cta-panel h2 {
  color: white;
  font-size: clamp(2rem, 4vw, 3.5rem);
  font-weight: 950;
  margin-bottom: 2rem;
}

.cta-actions {
  justify-content: center;
}

@media (max-width: 1024px) {
  .product-grid,
  .strength-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 768px) {
  .hero-section {
    min-height: 88vh;
    padding: 120px 0 64px;
  }

  .business-grid,
  .product-grid,
  .strength-grid {
    grid-template-columns: 1fr;
  }

  .section-dark,
  .cta-section {
    padding: 72px 0;
  }

  .primary-action,
  .secondary-action {
    width: 100%;
  }
}
</style>
