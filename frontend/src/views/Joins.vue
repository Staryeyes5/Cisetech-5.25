<template>
  <div class="joins-page">
    <section class="page-header">
      <div class="container">
        <p class="eyebrow">JOIN US</p>
        <h1 class="page-title">加入 Cisetech</h1>
        <p class="page-subtitle">
          与优秀团队共创未来，在金融科技、AI应用、企业数字化转型等方向持续成长。
        </p>
      </div>
    </section>

    <section id="openings" class="section openings-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">常招职位</h2>
          <p class="section-subtitle">持续寻找热爱技术、理解业务、愿意长期成长的伙伴。</p>
        </div>
        <div class="jobs-grid">
          <article v-for="job in jobs" :key="job.title" class="job-card">
            <div>
              <span class="job-type">{{ job.type }}</span>
              <h3>{{ job.title }}</h3>
              <p>{{ job.description }}</p>
            </div>
            <router-link to="/contact" class="job-link">咨询岗位</router-link>
          </article>
        </div>
      </div>
    </section>

    <section id="culture" class="section culture-section">
      <div class="container">
        <div class="culture-grid">
          <div>
            <h2 class="section-title">文化环境</h2>
            <p>
              我们重视专业能力、协作意识与持续学习，也相信稳定的团队氛围能让复杂项目走得更远。
            </p>
          </div>
          <div class="culture-list">
            <div v-for="item in culture" :key="item" class="culture-item">{{ item }}</div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { useHead } from '@vueuse/head'

useHead({
  title: '加入我们 | Cisetech官方招聘网站',
  meta: [
    {
      name: 'description',
      content: '加入Cisetech，与优秀团队共创未来。我们正在寻找具备好奇心、创造力和专业精神的伙伴。'
    },
    {
      name: 'keywords',
      content: 'Cisetech招聘,申朴信息招聘,技术岗位招聘,JOIN US'
    }
  ]
})

const jobs = [
  {
    title: 'Java开发工程师',
    type: '技术研发',
    description: '参与金融科技、企业数字化平台和后端服务研发。'
  },
  {
    title: '前端开发工程师',
    type: '技术研发',
    description: '负责企业级 Web 应用、可视化页面和交互体验开发。'
  },
  {
    title: 'AI应用工程师',
    type: 'AI方向',
    description: '围绕大模型、智能体和业务场景落地构建应用能力。'
  },
  {
    title: '项目经理',
    type: '交付管理',
    description: '推动客户项目计划、资源协调、交付质量和过程管理。'
  }
]

const culture = ['专业成长', '协作共创', '技术深耕', '长期主义']
</script>

<style scoped lang="scss">
.page-header {
  padding: 150px 0 90px;
  background:
    linear-gradient(135deg, rgba(2, 6, 23, 0.88), rgba(12, 74, 110, 0.8)),
    url('/assets/backgrounds/joins-hero.jpg') center/cover;
  color: white;
}

.eyebrow {
  color: #22d3ee;
  font-weight: 800;
  letter-spacing: 0.12em;
  margin-bottom: 1rem;
}

.page-title {
  font-size: clamp(2.5rem, 6vw, 5rem);
  line-height: 1;
  font-weight: 900;
  margin-bottom: 1.25rem;
}

.page-subtitle {
  max-width: 720px;
  color: #dbeafe;
  font-size: 1.2rem;
}

.openings-section {
  background: #f8fafc;
}

.jobs-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.job-card {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 220px;
  padding: 1.5rem;
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  box-shadow: 0 10px 28px rgba(15, 23, 42, 0.05);
}

.job-type {
  color: #0284c7;
  font-weight: 800;
  font-size: 0.9rem;
}

.job-card h3 {
  margin: 0.75rem 0;
  font-size: 1.35rem;
  color: #0f172a;
}

.job-card p {
  color: #475569;
}

.job-link {
  color: #0284c7;
  font-weight: 800;
  text-decoration: none;
}

.culture-section {
  background: #0f172a;
  color: white;
}

.culture-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 3rem;
  align-items: center;
}

.culture-section p {
  color: #cbd5e1;
  font-size: 1.05rem;
}

.culture-list {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 1rem;
}

.culture-item {
  padding: 1.25rem;
  border: 1px solid rgba(125, 211, 252, 0.25);
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.7);
  color: #e0f2fe;
  font-weight: 800;
}

@media (max-width: 768px) {
  .jobs-grid,
  .culture-grid,
  .culture-list {
    grid-template-columns: 1fr;
  }
}
</style>
