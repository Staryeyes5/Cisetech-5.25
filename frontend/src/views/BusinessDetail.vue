<template>
  <div class="business-detail-page">
    <section class="page-header">
      <div class="container">
        <p class="eyebrow">核心产品详情</p>
        <h1 class="page-title">Cisetech 产品与解决方案</h1>
        <p class="page-subtitle">
          聚焦AI应用、信创适配、数据治理与企业数字化转型，提供从基础设施到业务场景的完整产品能力。
        </p>
      </div>
    </section>

    <section class="product-nav">
      <div class="container">
        <div class="anchor-list">
          <a
            v-for="product in products"
            :key="product.id"
            :href="`#${product.id}`"
            class="anchor-link"
          >
            {{ product.name }}
          </a>
        </div>
      </div>
    </section>

    <section class="products-section section">
      <div class="container">
        <article
          v-for="product in products"
          :id="product.id"
          :key="product.id"
          class="product-panel"
        >
          <div class="product-content">
            <span class="product-tag">{{ product.tag }}</span>
            <h2>{{ product.name }}</h2>
            <p>{{ product.description }}</p>
            <ul>
              <li v-for="item in product.highlights" :key="item">{{ item }}</li>
            </ul>
          </div>
        </article>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
import { useHead } from '@vueuse/head'

useHead({
  title: '核心产品详情 - Cisetech',
  meta: [
    {
      name: 'description',
      content: 'Cisetech核心产品详情，包括一体化智能可观测平台、国产通用GPU、OceanBase数据库、智能招聘系统、AI招投标助手等。'
    },
    {
      name: 'keywords',
      content: 'Cisetech,核心产品,Simple Insight,OceanBase,AI招聘,AI招投标,低空经济,SQL审计'
    }
  ]
})

const products = [
  {
    id: 'product-simple-insight',
    name: '一体化智能可观测平台',
    tag: 'Simple Insight',
    description: '面向企业级系统的可观测、监控、分析与运维决策平台。',
    highlights: ['全链路性能观测', '多维指标分析', '智能告警与定位']
  },
  {
    id: 'product-muxi-gpu',
    name: '国产通用GPU',
    tag: 'AI基础设施',
    description: '面向国产化算力场景的通用GPU产品与适配服务。',
    highlights: ['国产算力适配', 'AI训练与推理支撑', '集群部署与运维服务']
  },
  {
    id: 'product-oceanbase',
    name: 'OceanBase数据库',
    tag: '数据库与信创',
    description: '为金融与企业客户提供数据库选型、迁移、适配和治理服务。',
    highlights: ['分布式数据库能力', '信创适配服务', '数据迁移与性能优化']
  },
  {
    id: 'product-ai-recruit',
    name: '智能招聘系统',
    tag: 'AI应用',
    description: '覆盖招聘流程管理、简历筛选与岗位匹配的智能化系统。',
    highlights: ['简历解析', '岗位智能匹配', '招聘流程协同']
  },
  {
    id: 'product-ai-bidding',
    name: 'AI招投标助手',
    tag: 'AI办公',
    description: '辅助企业完成招投标文件分析、生成、审核和知识沉淀。',
    highlights: ['标书智能生成', '风险点识别', '企业知识库沉淀']
  },
  {
    id: 'product-ai-health',
    name: '职场健康加油站',
    tag: '智慧健康',
    description: '面向组织员工健康管理场景的数字化服务平台。',
    highlights: ['健康档案管理', '风险提醒', '员工服务运营']
  },
  {
    id: 'product-low-altitude',
    name: '低空综合管理服务平台',
    tag: '低空经济',
    description: '面向低空经济场景的综合管理、运行监测和服务支撑平台。',
    highlights: ['运行态势展示', '资源统筹管理', '场景化业务支撑']
  },
  {
    id: 'product-sql-audit',
    name: 'SQL代码审计平台',
    tag: '数据安全',
    description: '面向数据库开发和运维流程的SQL审核、优化与风险控制平台。',
    highlights: ['SQL规范审核', '风险识别', '性能优化建议']
  }
]
</script>

<style scoped lang="scss">
.page-header {
  padding: 150px 0 80px;
  background: linear-gradient(135deg, #020617 0%, #0f172a 55%, #0c4a6e 100%);
  color: white;
}

.eyebrow {
  color: #22d3ee;
  font-weight: 700;
  letter-spacing: 0.08em;
  margin-bottom: 1rem;
}

.page-title {
  font-size: clamp(2.25rem, 5vw, 4.5rem);
  line-height: 1.1;
  font-weight: 900;
  margin-bottom: 1.25rem;
}

.page-subtitle {
  max-width: 760px;
  color: #cbd5e1;
  font-size: 1.15rem;
}

.product-nav {
  position: sticky;
  top: 70px;
  z-index: 20;
  background: rgba(255, 255, 255, 0.94);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border-color);
}

.anchor-list {
  display: flex;
  gap: 0.75rem;
  overflow-x: auto;
  padding: 1rem 0;
}

.anchor-link {
  flex: 0 0 auto;
  padding: 0.6rem 0.9rem;
  border-radius: 6px;
  color: #0f172a;
  text-decoration: none;
  font-weight: 600;
  background: #f1f5f9;

  &:hover {
    color: #0369a1;
    background: #e0f2fe;
  }
}

.products-section {
  background: #f8fafc;
}

.product-panel {
  scroll-margin-top: 150px;
  background: white;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  padding: clamp(1.5rem, 4vw, 3rem);
  margin-bottom: 1.5rem;
  box-shadow: 0 12px 32px rgba(15, 23, 42, 0.06);
}

.product-tag {
  display: inline-flex;
  color: #0284c7;
  font-weight: 800;
  margin-bottom: 0.75rem;
}

.product-content h2 {
  font-size: clamp(1.75rem, 3vw, 2.5rem);
  margin-bottom: 1rem;
  color: #0f172a;
}

.product-content p {
  color: #475569;
  font-size: 1.05rem;
  margin-bottom: 1.5rem;
}

.product-content ul {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 0.75rem;
  padding: 0;
  list-style: none;
}

.product-content li {
  padding: 0.85rem 1rem;
  background: #f8fafc;
  border-radius: 6px;
  color: #334155;
}

@media (max-width: 768px) {
  .product-content ul {
    grid-template-columns: 1fr;
  }
}
</style>
