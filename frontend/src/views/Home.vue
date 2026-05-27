<template>
  <div class="home-page">
    <div class="scroll-progress" :style="{ transform: `scaleX(${scrollProgress})` }"></div>
    <canvas ref="particleCanvas" class="particles-canvas" aria-hidden="true"></canvas>
    <div class="tech-grid" aria-hidden="true"></div>
    <div
      v-for="line in flowLines"
      :key="line.left"
      class="flow-line"
      :style="{ left: line.left, animationDelay: line.delay }"
      aria-hidden="true"
    ></div>

    <section class="hero-section fullpage-section" data-section="hero">
      <div class="hero-bg" aria-hidden="true">
        <img :src="heroImage" alt="" />
      </div>
      <div class="container">
        <div class="hero-content reveal">
          <h1 class="hero-title" data-text="Cisetech">Cisetech</h1>
          <div class="hero-slogan">
            <p class="ai-glow">申朴AI·智创无限</p>
            <p>AI 聚力数转智改，创领智能新生态</p>
          </div>
        </div>
      </div>
    </section>

    <section class="section-dark fullpage-section" id="services" data-section="services">
      <div class="container">
        <div class="section-heading reveal">
          <h2>核心业务</h2>
          <p>全栈AI能力，赋能企业智能化转型</p>
        </div>

        <div class="business-grid">
          <article v-for="item in businessModules" :key="item.title" class="business-card reveal">
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

    <section class="section-dark fullpage-section" id="products" data-section="products">
      <div class="container">
        <div class="section-heading reveal">
          <h2>核心产品方案</h2>
          <p>基于核心技术研发的标准化产品与代理产品，满足多样化业务场景需求</p>
        </div>

        <div class="product-grid">
          <article v-for="product in products" :key="product.id" class="product-card reveal">
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

          <article class="product-card product-card-more reveal">
            <div class="more-icon">+</div>
            <h3>需要定制化产品？</h3>
            <p>围绕业务场景、数据基础、算力环境和交付模式，为企业定制产品组合。</p>
            <router-link to="/services#products" class="primary-action compact">查看全部产品</router-link>
          </article>
        </div>

        <div class="case-preview">
          <div class="section-heading small reveal">
            <h3>相关案例</h3>
            <p>深耕金融科技领域，以AI技术赋能银行等业务创新</p>
          </div>

          <div class="case-grid">
            <article v-for="item in caseStudies" :key="item.title" class="case-card reveal">
              <span class="case-tag">{{ item.tag }}</span>
              <h4>{{ item.title }}</h4>
              <p>{{ item.text }}</p>
              <div v-if="item.metrics" class="case-metrics">
                <div v-for="metric in item.metrics" :key="metric.label">
                  <strong>{{ metric.value }}</strong>
                  <span>{{ metric.label }}</span>
                </div>
              </div>
              <div v-else class="case-note">{{ item.note }}</div>
            </article>
          </div>
        </div>
      </div>
    </section>

    <section class="section-dark fullpage-section" id="strength" data-section="strength">
      <div class="container">
        <div class="section-heading reveal">
          <h2>企业实力</h2>
          <p>卓越技术，权威认可。构建领先、合规、可信赖的AI信息技术服务</p>
        </div>

        <div class="strength-grid">
          <router-link
            v-for="item in strengths"
            :key="item.title"
            :to="item.to"
            class="strength-card reveal"
          >
            <span class="strength-number">{{ item.value }}</span>
            <h3>{{ item.title }}</h3>
            <p>{{ item.text }}</p>
          </router-link>
        </div>

        <div class="stats-block reveal">
          <div class="section-heading small">
            <h3>核心数据</h3>
            <p>用数据说话，见证成长与实力</p>
          </div>
          <div class="stats-grid">
            <div v-for="stat in coreStats" :key="stat.label" class="stat-card">
              <strong>{{ stat.value }}<span>+</span></strong>
              <p>{{ stat.label }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="cta-section fullpage-section" id="contact" data-section="contact">
      <div class="container">
        <div class="cta-panel reveal">
          <p>专业团队，AI赋能</p>
          <h2>为您的企业打造智能化解决方案</h2>
          <div class="cta-actions">
            <router-link to="/contact" class="primary-action">立即咨询</router-link>
            <router-link to="/about" class="secondary-action">了解申朴</router-link>
          </div>
        </div>
      </div>
    </section>

    <button class="back-to-top" :class="{ visible: showBackToTop }" type="button" title="返回顶部" @click="scrollToTop">
      <span aria-hidden="true">↑</span>
    </button>

    <nav class="page-nav" aria-label="首页章节导航">
      <button
        v-for="(item, index) in pageNavItems"
        :key="item.id"
        class="page-nav-dot"
        :class="{ active: activeSection === index }"
        type="button"
        :data-title="item.label"
        :aria-label="item.label"
        @click="scrollToSection(item.id)"
      ></button>
    </nav>
  </div>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { useHead } from '@vueuse/head'

import heroImage from '../../../assets/backgrounds/背景图球.png'
import simpleInsightImage from '../../../assets/projects/unnamed 2.png'
import aiRecruitImage from '../../../assets/projects/unnamed 9.png'
import aiBiddingImage from '../../../assets/projects/招投标助手.jpg'
import muxiGpuImage from '../../../assets/projects/unnamed 3.png'
import healthImage from '../../../assets/projects/职场健康加油站.jpeg'
import oceanBaseImage from '../../../assets/projects/OceanBase2.png'
import sqlAuditImage from '../../../assets/backgrounds/sql-audit-platform.jpeg'
import lowAltitudeImage from '../../../assets/backgrounds/低空经济bg.png'

useHead({
  title: 'Cisetech - 申朴AI·智创无限',
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

const scrollProgress = ref(0)
const showBackToTop = ref(false)
const activeSection = ref(0)
const particleCanvas = ref<HTMLCanvasElement | null>(null)
let animationFrame = 0
let observer: IntersectionObserver | null = null
let resizeParticles: (() => void) | null = null

const pageNavItems = [
  { id: 'hero', label: '首页' },
  { id: 'services', label: '核心业务' },
  { id: 'products', label: '产品方案' },
  { id: 'strength', label: '企业实力' },
  { id: 'contact', label: '联系我们' }
]

const flowLines = [
  { left: '5%', delay: '0s' },
  { left: '25%', delay: '1s' },
  { left: '50%', delay: '0.5s' },
  { left: '75%', delay: '1.5s' },
  { left: '95%', delay: '2s' }
]

const businessModules = [
  {
    title: '战略咨询和规划',
    accent: '#22d3ee',
    items: [
      { title: '顶层设计', text: 'AI环境下IT管理规划、IT治理、降本增效、AI原生开发平台、应用场景设计' },
      { title: '应用模式', text: '业务流程咨询、系统方案、产品设计、技术架构' },
      { title: '技术选型', text: '开发架构、运维架构、算力架构、安全架构、Agent架构、知识库构建' }
    ]
  },
  {
    title: '解决方案',
    accent: '#a78bfa',
    items: [
      { title: '算力供给与集群管理', text: '算力租赁/供给、算力资源管理、混合算力架构设计' },
      { title: '数据加工', text: '多模态数据标注、数据采集、数据治理' },
      { title: '企业级Open Claw应用部署', text: '基于K8s容器化、高可用、可管控的智能体平台，把大模型变成可落地、可运维、可安全合规的企业级系统。实现稳定运行、数据安全、多人协作、自动执行的企业 AI 能力' },
      { title: '模型训练', text: '代码小模型、领域模型训练、Agent调优' },
      { title: '信息安全', text: '银行级移动安全SaaS服务平台、移动安全隐私合规检测产品' },
      { title: '用户体验', text: '移动APP体验监测、采购管理系统（SRM）、人力资源管理SaaS平台（HR在线）' }
    ]
  },
  {
    title: '产品',
    accent: '#34d399',
    items: [
      { title: 'AI方向', text: 'AI辅助编程工具、AI招聘、招投标助手、各类场景AI Agent、智守AI Agent安全验证平台、Agent代码安全审查' },
      { title: '大数据管理与应用方向', text: '数据资产治理与可视化平台、长尾客户营销（大数据模型+自动外呼+服销+企微私域）' },
      { title: '国产信创方向', text: '数据库SQL代码调优与AI智能审核（SQL AI Review）、数据库研发规范管理（Bettle）、数据库代码自动转换（Carn）、数据迁移与同步（Data Bus），以及企业应用鸿蒙化架构与实施方案' },
      { title: '移动安全方向', text: '金融级移动安全检测平台（IOS/安卓/鸿蒙APP、小程序、SDK等）、移动安全检测工具包、互联网运营反薅羊毛' },
      { title: '客户体验方向', text: 'Simple Insight 一体化智能可观测平台' }
    ]
  },
  {
    title: '人力资源配置与服务',
    accent: '#fbbf24',
    items: [
      { title: 'AI基建', text: '标注（文本、语音、视频、智驾等）、审核、模型训练、AI人才培训等' },
      { title: '技术人员供给', text: '人工智能、软件研发、大数据、区块链、物联网、网络与数据安全等各类技术开发、测试、运维等' },
      { title: '业务流程人员供给', text: '呼叫中心服务、客服、外呼、催收、标注、审核、运营、互联网营销推广、金融后台服务、其他业务运营服务' },
      { title: '用工配置', text: '劳务派遣、灵活用工、HRO、BPO等' },
      { title: '交付模式', text: '在岸、离岸、全职、兼职等' }
    ]
  }
]

const products = [
  { id: 'product-simple-insight', name: 'Simple Insight 一体化智能可观测平台', category: '本地私有化部署', badge: '本地私有化部署', description: '集成全栈链路监控、智能异常检测与自动化响应，本地私有化部署为企业提供全方位安全护航。', image: simpleInsightImage },
  { id: 'product-ai-recruit', name: '智能招聘系统', category: '智能人力资源', badge: '智能人力资源', description: '重塑人才招聘流程，通过简历智能解析与初筛，提升招聘效率300%以上。', image: aiRecruitImage },
  { id: 'product-ai-bidding', name: 'AI 招投标助手', category: '智慧办公', badge: '智慧办公', description: '自动化采集标讯信息、分析招标需求，一键生成合规应标文件，大幅降低人为失误，提升中标率。', image: aiBiddingImage },
  { id: 'product-muxi-gpu', name: '国产通用 GPU', category: '国产算力底座', badge: '国产算力底座', description: '专为大规模AI计算设计，支持通用计算与图形渲染，实现国产化替代的强大动力源。', image: muxiGpuImage },
  { id: 'product-ai-health', name: '职场健康加油站', category: '职场健康管理', badge: '职场健康管理', description: '专注企业职工健康管理，提供一站式健康监测、智能评估与个性化干预服务。', image: healthImage },
  { id: 'product-oceanbase', name: 'OceanBase 数据库', category: '企业级数据库', badge: '企业级数据库', description: '原生分布式数据库，具备城市级无损容灾、全兼容Oracle SQL语法、极致压缩等核心能力。', image: oceanBaseImage },
  { id: 'product-sql-audit', name: '申朴 SQL 代码审计平台', category: '数据库安全', badge: '数据库安全', description: '面向企业数据库安全的专业化静态代码检测产品，精准识别SQL注入、权限越权、数据泄露等高风险问题。', image: sqlAuditImage },
  { id: 'product-low-altitude', name: '低空综合管理服务平台', category: '智慧城市·低空经济', badge: '智慧城市·低空经济', description: '面向低空飞行管理领域的专业测试平台，支持测试任务全生命周期管理、测试数据智能生成、多语言脚本编写等核心功能。', image: lowAltitudeImage }
]

const strengths = [
  { value: '荣誉', title: '荣誉奖项', text: '凭借在信息技术领域的卓越表现，多次获得政府和行业认可。', to: '/qualifications#honors' },
  { value: '资质', title: '资质认证', text: '完善的资质认证体系，覆盖国际标准认证、行业资质和经营许可。', to: '/qualifications#qualifications' },
  { value: '专利', title: '专利证书', text: '自主研发核心技术，拥有多项发明专利。', to: '/qualifications#patents' },
  { value: '软著', title: '软件著作权', text: '自主研发软件产品，持续创新技术积累。', to: '/qualifications#software-copyrights' }
]

const coreStats = [
  { value: '100', label: '企业客户' },
  { value: '3000', label: '员工' },
  { value: '500', label: '技术专家' },
  { value: '200', label: '软件著作权' }
]

const caseStudies = [
  {
    tag: '案例一',
    title: 'SME智能信贷审批解决方案',
    text: '针对中小微企业信贷审批业务场景，使用私有化AI工具处理核心业务逻辑。',
    metrics: [
      { value: '+8.3%', label: '审批通过率' },
      { value: '-87%', label: '审批时长' }
    ]
  },
  { tag: '案例二', title: '小微企业线上开户智能解决方案', text: '专为小微企业打造，AI驱动实现极致提效，开户流程从几天缩短到几分钟。', note: 'AI驱动 · 极致提效' },
  { tag: '案例三', title: 'AI Agent安全检测平台', text: '针对AI Agent应用的安全检测与加固，确保企业AI应用安全可靠。', note: '安全检测 · 加固防护' }
]

const updateScrollState = () => {
  const scrollTop = window.scrollY
  const docHeight = document.documentElement.scrollHeight - window.innerHeight
  scrollProgress.value = docHeight > 0 ? scrollTop / docHeight : 0
  showBackToTop.value = scrollTop > 500

  const sections = pageNavItems
    .map(item => document.querySelector<HTMLElement>(`[data-section="${item.id}"]`))
    .filter(Boolean) as HTMLElement[]

  const current = sections.findIndex(section => {
    const rect = section.getBoundingClientRect()
    return rect.top <= window.innerHeight * 0.45 && rect.bottom >= window.innerHeight * 0.35
  })

  if (current >= 0) activeSection.value = current
}

const scrollToSection = (sectionId: string) => {
  document
    .querySelector<HTMLElement>(`[data-section="${sectionId}"]`)
    ?.scrollIntoView({ behavior: 'smooth', block: 'start' })
}

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

const setupReveal = () => {
  observer = new IntersectionObserver(
    entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible')
          observer?.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.16, rootMargin: '0px 0px -50px 0px' }
  )

  document.querySelectorAll('.reveal').forEach(el => observer?.observe(el))
}

const setupParticles = () => {
  const canvas = particleCanvas.value
  const context = canvas?.getContext('2d')
  if (!canvas || !context) return

  const particles = Array.from({ length: 80 }, () => ({
    x: Math.random() * window.innerWidth,
    y: Math.random() * window.innerHeight,
    vx: (Math.random() - 0.5) * 0.5,
    vy: (Math.random() - 0.5) * 0.5,
    size: Math.random() * 2 + 1
  }))

  const resize = () => {
    canvas.width = window.innerWidth
    canvas.height = window.innerHeight
  }

  const animate = () => {
    context.clearRect(0, 0, canvas.width, canvas.height)
    context.fillStyle = 'rgba(34, 211, 238, 0.72)'

    particles.forEach((particle, index) => {
      particle.x += particle.vx
      particle.y += particle.vy

      if (particle.x < 0 || particle.x > canvas.width) particle.vx *= -1
      if (particle.y < 0 || particle.y > canvas.height) particle.vy *= -1

      context.beginPath()
      context.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2)
      context.fill()

      particles.slice(index + 1).forEach(next => {
        const distance = Math.hypot(particle.x - next.x, particle.y - next.y)
        if (distance < 120) {
          context.strokeStyle = `rgba(34, 211, 238, ${0.18 * (1 - distance / 120)})`
          context.lineWidth = 1
          context.beginPath()
          context.moveTo(particle.x, particle.y)
          context.lineTo(next.x, next.y)
          context.stroke()
        }
      })
    })

    animationFrame = requestAnimationFrame(animate)
  }

  resize()
  animate()
  window.addEventListener('resize', resize)
  resizeParticles = resize
}

onMounted(() => {
  setupReveal()
  setupParticles()
  updateScrollState()
  window.addEventListener('scroll', updateScrollState, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateScrollState)
  observer?.disconnect()
  if (animationFrame) cancelAnimationFrame(animationFrame)
  if (resizeParticles) window.removeEventListener('resize', resizeParticles)
})
</script>

<style scoped lang="scss">
.home-page {
  min-height: 100vh;
  position: relative;
  overflow: hidden;
  background: #020617;
  color: #e2e8f0;
}

.scroll-progress {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1100;
  width: 100%;
  height: 4px;
  transform-origin: left center;
  background: linear-gradient(90deg, #0ea5e9, #22d3ee, #8b5cf6, #ec4899, #0ea5e9);
  background-size: 200% 100%;
  animation: gradient-shift 3s ease infinite;
}

.particles-canvas,
.tech-grid {
  position: fixed;
  inset: 0;
  pointer-events: none;
}

.particles-canvas {
  z-index: 0;
  opacity: 0.55;
}

.tech-grid {
  z-index: 0;
  opacity: 0.12;
  background-image:
    linear-gradient(90deg, rgba(14, 165, 233, 0.03) 1px, transparent 1px),
    linear-gradient(rgba(14, 165, 233, 0.03) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: grid-move 25s linear infinite;
}

.flow-line {
  position: fixed;
  top: -30vh;
  z-index: 0;
  width: 2px;
  height: 100px;
  pointer-events: none;
  background: linear-gradient(to bottom, transparent, #22d3ee, transparent);
  animation: flow-line 3s ease-in-out infinite;
}

.fullpage-section {
  position: relative;
  z-index: 1;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-top: 130px;
  padding-bottom: 40px;
}

.reveal {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.75s ease, transform 0.75s ease;
}

.reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  padding-top: 180px;
  background:
    radial-gradient(circle at 68% 42%, rgba(14, 165, 233, 0.2), transparent 34%),
    linear-gradient(135deg, #020617 0%, #07111f 48%, #0f172a 100%);
}

.hero-bg {
  position: absolute;
  inset: 0;
  opacity: 0.68;
  pointer-events: none;
}

.hero-bg img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  filter: saturate(1.08);
}

.hero-bg::after {
  content: '';
  position: absolute;
  inset: 0;
  background:
    linear-gradient(90deg, rgba(2, 6, 23, 0.92) 0%, rgba(2, 6, 23, 0.72) 45%, rgba(2, 6, 23, 0.35) 100%),
    linear-gradient(0deg, #020617 0%, transparent 34%);
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 920px;
  margin: -65px auto 0;
  text-align: center;
}

.hero-title {
  position: relative;
  display: inline-block;
  font-size: clamp(3rem, 8vw, 7rem);
  line-height: 0.98;
  font-weight: 900;
  margin-bottom: 1rem;
  background: linear-gradient(135deg, #fff 0%, #0ea5e9 50%, #22d3ee 100%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-title::before {
  content: attr(data-text);
  position: absolute;
  inset: 0;
  z-index: -1;
  background: linear-gradient(135deg, #0ea5e9, #22d3ee);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  filter: blur(40px);
  opacity: 0.7;
  animation: title-glow 3s ease-in-out infinite;
}

.hero-slogan {
  margin-bottom: 1.5rem;
}

.hero-slogan p:first-child {
  color: white;
  font-size: clamp(1.5rem, 4vw, 2.25rem);
  font-weight: 800;
  margin-bottom: 0.75rem;
}

.hero-slogan p:last-child {
  font-size: clamp(1rem, 2vw, 1.25rem);
  color: #cbd5e1;
}

.ai-glow {
  animation: ai-glow 2s ease-in-out infinite;
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
  background:
    radial-gradient(circle at 16% 10%, rgba(14, 165, 233, 0.12), transparent 26%),
    #020617;
}

.section-heading {
  text-align: center;
  margin-bottom: 3rem;
}

.section-heading.small {
  margin-bottom: 2rem;
}

.section-heading h2 {
  font-size: clamp(2.25rem, 5vw, 3rem);
  color: white;
  font-weight: 900;
  margin-bottom: 0.75rem;
}

.section-heading h3 {
  font-size: clamp(1.7rem, 3vw, 2.35rem);
  color: white;
  font-weight: 900;
  margin-bottom: 0.65rem;
}

.section-heading p {
  color: #94a3b8;
  font-size: 1.25rem;
  max-width: 780px;
  margin: 0 auto;
}

.business-grid,
.product-grid,
.case-grid,
.strength-grid,
.stats-grid {
  display: grid;
  gap: 2rem;
}

.business-grid {
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1.5rem;
}

.product-grid {
  grid-template-columns: repeat(3, minmax(0, 1fr));
}

.case-grid {
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 1.5rem;
}

.strength-grid,
.stats-grid {
  grid-template-columns: repeat(4, minmax(0, 1fr));
}

.business-card,
.product-card,
.strength-card,
.cta-panel,
.case-card,
.stat-card {
  position: relative;
  overflow: hidden;
  border: 1px solid rgba(14, 165, 233, 0.2);
  border-radius: 24px;
  background: rgba(255, 255, 255, 0.03);
  box-shadow: none;
  backdrop-filter: blur(20px);
  transition: all 0.5s ease;
}

.business-card,
.case-card,
.strength-card,
.stat-card {
  padding: 1.5rem;
}

.business-card::before,
.product-card::before,
.strength-card::before,
.cta-panel::before,
.case-card::before,
.stat-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(14, 165, 233, 0.1), transparent);
  transition: left 0.8s ease;
  pointer-events: none;
}

.business-card:hover::before,
.product-card:hover::before,
.strength-card:hover::before,
.cta-panel:hover::before,
.case-card:hover::before,
.stat-card:hover::before {
  left: 100%;
}

.business-card::after,
.product-card::after,
.strength-card::after,
.cta-panel::after,
.case-card::after,
.stat-card::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, #22d3ee, transparent);
}

.business-card:hover,
.product-card:hover,
.strength-card:hover,
.cta-panel:hover,
.case-card:hover,
.stat-card:hover {
  transform: translateY(-10px);
  border-color: rgba(14, 165, 233, 0.5);
  box-shadow:
    0 30px 60px rgba(14, 165, 233, 0.2),
    0 0 40px rgba(14, 165, 233, 0.1);
}

.business-card-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 20px;
  padding-bottom: 16px;
  border-bottom: 1px solid rgba(14, 165, 233, 0.1);
}

.business-icon {
  width: 44px;
  height: 44px;
  border-radius: 12px;
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

.product-card {
  overflow: hidden;
}

.product-media {
  position: relative;
  display: block;
  height: 12rem;
  aspect-ratio: auto;
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
  border-radius: 4px;
  color: #020617;
  background: #22d3ee;
  font-size: 0.76rem;
  font-weight: 850;
}

.product-body {
  padding: 1.5rem;
}

.product-category {
  color: #38bdf8;
  font-size: 0.86rem;
  font-weight: 800;
  margin-bottom: 0.6rem;
}

.product-body h3,
.product-card-more h3,
.case-card h4 {
  color: white;
  font-size: 1.2rem;
  font-weight: 850;
  margin-bottom: 0.75rem;
}

.product-body p,
.product-card-more p,
.case-card p,
.case-note {
  color: #94a3b8;
  line-height: 1.65;
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

.case-preview,
.stats-block {
  margin-top: 4rem;
  padding-top: 4rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.case-card {
  border-top: 3px solid #22d3ee;
}

.case-tag {
  display: inline-flex;
  padding: 0.25rem 0.55rem;
  border-radius: 6px;
  color: #38bdf8;
  background: rgba(14, 165, 233, 0.15);
  font-size: 0.78rem;
  font-weight: 850;
  margin-bottom: 0.95rem;
}

.case-metrics {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.75rem;
  margin-top: 1rem;
}

.case-metrics div {
  text-align: center;
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.78);
  padding: 0.8rem 0.5rem;
}

.case-metrics strong {
  display: block;
  color: #22d3ee;
  font-size: 1.4rem;
}

.case-metrics span {
  color: #64748b;
  font-size: 0.8rem;
}

.case-note {
  display: inline-flex;
  margin-top: 1rem;
  padding: 0.45rem 0.75rem;
  border-radius: 8px;
  background: rgba(34, 211, 238, 0.1);
  color: #67e8f9;
}

.strength-card {
  text-decoration: none;
  color: inherit;
  transition: transform 0.25s ease, border-color 0.25s ease;
}

.strength-card:hover {
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

.strength-card p,
.stat-card p {
  color: #94a3b8;
  line-height: 1.65;
}

.stat-card {
  text-align: center;
  border-radius: 16px;
  background: rgba(14, 165, 233, 0.05);
}

.stat-card strong {
  font-size: clamp(2rem, 4vw, 3.25rem);
  font-weight: 950;
  background: linear-gradient(135deg, #0ea5e9, #22d3ee);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
}

.stat-card strong span {
  color: #22d3ee;
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
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

.back-to-top {
  position: fixed;
  right: 24px;
  bottom: 24px;
  z-index: 900;
  width: 48px;
  height: 48px;
  display: grid;
  place-items: center;
  border: none;
  border-radius: 50%;
  color: white;
  background: linear-gradient(135deg, #0ea5e9, #22d3ee);
  box-shadow: 0 4px 16px rgba(14, 165, 233, 0.3);
  cursor: pointer;
  opacity: 0;
  visibility: hidden;
  transform: translateY(12px);
  transition: opacity 0.25s ease, transform 0.25s ease, visibility 0.25s ease;
}

.back-to-top.visible {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}

.back-to-top span {
  font-size: 1.4rem;
  line-height: 1;
}

.page-nav {
  position: fixed;
  right: 30px;
  top: 50%;
  z-index: 850;
  display: flex;
  flex-direction: column;
  gap: 12px;
  transform: translateY(-50%);
}

.page-nav-dot {
  position: relative;
  width: 12px;
  height: 12px;
  border: 2px solid rgba(14, 165, 233, 0.3);
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  cursor: pointer;
  transition: background 0.25s ease, border-color 0.25s ease, transform 0.25s ease;
}

.page-nav-dot::before {
  content: attr(data-title);
  position: absolute;
  right: 25px;
  top: 50%;
  transform: translateY(-50%);
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  color: #94a3b8;
  background: rgba(15, 23, 42, 0.9);
  border: 1px solid rgba(148, 163, 184, 0.22);
  border-radius: 6px;
  padding: 0.35rem 0.55rem;
  font-size: 0.75rem;
  transition: opacity 0.2s ease, transform 0.2s ease;
}

.page-nav-dot:hover::before {
  opacity: 1;
  transform: translate(-4px, -50%);
}

.page-nav-dot:hover,
.page-nav-dot.active {
  border-color: #22d3ee;
  background: linear-gradient(135deg, #0ea5e9, #22d3ee);
  transform: scale(1.3);
  box-shadow: 0 0 15px rgba(14, 165, 233, 0.6);
}

@keyframes gradient-shift {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

@keyframes grid-move {
  0% {
    transform: translate(0, 0);
  }
  100% {
    transform: translate(60px, 60px);
  }
}

@keyframes title-glow {
  0%,
  100% {
    opacity: 0.5;
    filter: blur(40px);
  }
  50% {
    opacity: 0.8;
    filter: blur(50px);
  }
}

@keyframes ai-glow {
  0%,
  100% {
    text-shadow: 0 0 20px rgba(14, 165, 233, 0.5);
    filter: brightness(1);
  }
  50% {
    text-shadow: 0 0 40px rgba(14, 165, 233, 0.8), 0 0 60px rgba(34, 211, 238, 0.5);
    filter: brightness(1.2);
  }
}

@keyframes flow-line {
  0% {
    transform: translateY(-100px);
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    transform: translateY(100vh);
    opacity: 0;
  }
}

@media (max-width: 1024px) {
  .product-grid,
  .strength-grid,
  .stats-grid,
  .case-grid {
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
  .strength-grid,
  .stats-grid,
  .case-grid {
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

  .page-nav {
    display: none;
  }

  .back-to-top {
    right: 16px;
    bottom: 16px;
  }
}
</style>
