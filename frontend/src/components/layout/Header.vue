<template>
  <header class="site-shell" :class="{ 'site-shell-scrolled': isScrolled }">
    <div class="top-bar">
      <div class="container top-bar-inner">
        <div class="top-contact">
          <a href="tel:02160756566">(021)-6075 6566</a>
          <a href="mailto:info@cisetech.com">info@cisetech.com</a>
        </div>
        <div class="language-switch" aria-label="语言切换">
          <span class="active">中文</span>
          <span>|</span>
          <span>EN</span>
        </div>
      </div>
    </div>

    <div class="main-header">
      <div class="container">
        <nav class="nav" aria-label="主导航">
          <router-link to="/" class="brand" @click="closeMobileMenu">
            <img :src="logoImage" alt="Cisetech Logo" />
            <span>
              <strong>Cisetech</strong>
              <small>申朴信息技术（上海）股份有限公司</small>
            </span>
          </router-link>

          <div class="desktop-nav">
            <router-link to="/" class="nav-link" :class="{ active: route.path === '/' }">首页</router-link>
            <div v-for="group in navGroups" :key="group.label" class="nav-dropdown">
              <router-link
                :to="group.path"
                class="nav-link"
                :class="{ active: isGroupActive(group) }"
              >
                {{ group.label }}
              </router-link>
              <div class="nav-dropdown-menu">
                <router-link v-for="child in group.children" :key="child.to" :to="child.to">
                  {{ child.label }}
                </router-link>
              </div>
            </div>
          </div>

          <div class="nav-actions">
            <router-link to="/contact" class="consult-link" @click="closeMobileMenu">咨询合作</router-link>
            <button class="menu-toggle" type="button" aria-label="菜单" @click="isMenuOpen = !isMenuOpen">
              <span :class="{ open: isMenuOpen }"></span>
            </button>
          </div>
        </nav>
      </div>
    </div>

    <div class="mobile-overlay" :class="{ open: isMenuOpen }" @click="closeMobileMenu"></div>
    <nav class="mobile-nav" :class="{ open: isMenuOpen }" aria-label="移动端导航">
      <router-link to="/" :class="{ active: route.path === '/' }" @click="closeMobileMenu">首页</router-link>
      <div v-for="group in navGroups" :key="group.label" class="mobile-group">
        <button type="button" @click="toggleMobileGroup(group.label)">
          <span>{{ group.label }}</span>
          <span>{{ activeMobileGroup === group.label ? '−' : '+' }}</span>
        </button>
        <div v-show="activeMobileGroup === group.label" class="mobile-submenu">
          <router-link :to="group.path" @click="closeMobileMenu">{{ group.label }}总览</router-link>
          <router-link v-for="child in group.children" :key="child.to" :to="child.to" @click="closeMobileMenu">
            {{ child.label }}
          </router-link>
        </div>
      </div>
      <router-link to="/contact" class="mobile-consult" @click="closeMobileMenu">咨询合作</router-link>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import { useRoute } from 'vue-router'

import logoImage from '../../../../assets/logos/申朴圆点logo.png'

const route = useRoute()
const isScrolled = ref(false)
const isMenuOpen = ref(false)
const activeMobileGroup = ref('')

const navGroups = [
  {
    label: '核心产品',
    path: '/services#products',
    activePaths: ['/services', '/products', '/business-detail'],
    children: [
      { label: '一体化智能可观测平台', to: '/business-detail#product-simple-insight' },
      { label: '国产通用GPU', to: '/business-detail#product-muxi-gpu' },
      { label: 'OceanBase数据库', to: '/business-detail#product-oceanbase' },
      { label: '智能招聘系统', to: '/business-detail#product-ai-recruit' },
      { label: 'AI招投标助手', to: '/business-detail#product-ai-bidding' },
      { label: '职场健康加油站', to: '/business-detail#product-ai-health' },
      { label: '低空综合管理服务平台', to: '/business-detail#product-low-altitude' },
      { label: 'SQL代码审计平台', to: '/business-detail#product-sql-audit' }
    ]
  },
  {
    label: '企业实力',
    path: '/qualifications',
    activePaths: ['/qualifications'],
    children: [
      { label: '荣誉资质', to: '/qualifications#honors' },
      { label: '权威客户', to: '/qualifications#clients' }
    ]
  },
  {
    label: '招贤纳士',
    path: '/joins',
    activePaths: ['/joins'],
    children: [
      { label: '常招职位', to: '/joins#openings' },
      { label: '文化环境', to: '/joins#culture' }
    ]
  },
  {
    label: '关于我们',
    path: '/about',
    activePaths: ['/about'],
    children: [
      { label: '关于申朴', to: '/about#about' },
      { label: '企业文化', to: '/about#culture' },
      { label: '发展历程', to: '/about#timeline' },
      { label: '分支机构', to: '/about#branches' },
      { label: '离岸交付中心', to: '/about#offshore' }
    ]
  }
]

const isGroupActive = (group: { activePaths: string[] }) => group.activePaths.includes(route.path)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

const closeMobileMenu = () => {
  isMenuOpen.value = false
}

const toggleMobileGroup = (label: string) => {
  activeMobileGroup.value = activeMobileGroup.value === label ? '' : label
}

onMounted(() => {
  handleScroll()
  window.addEventListener('scroll', handleScroll, { passive: true })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped lang="scss">
.site-shell {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  color: white;
  transition: background 0.3s ease, border-color 0.3s ease, backdrop-filter 0.3s ease;
}

.site-shell-scrolled {
  background: rgba(15, 23, 42, 0.9);
  border-bottom: 1px solid rgba(51, 65, 85, 0.5);
  backdrop-filter: blur(20px);
}

.top-bar {
  border-bottom: 1px solid transparent;
  font-size: 0.86rem;
  color: #cbd5e1;
  transition: opacity 0.3s ease, height 0.3s ease;
}

.site-shell-scrolled .top-bar {
  height: 0;
  overflow: hidden;
  opacity: 0;
}

.top-bar-inner,
.top-contact,
.language-switch,
.nav,
.brand,
.desktop-nav,
.nav-actions {
  display: flex;
  align-items: center;
}

.top-bar-inner {
  height: 36px;
  justify-content: space-between;
}

.top-contact,
.language-switch {
  gap: 1rem;
}

.top-contact a,
.language-switch span {
  color: inherit;
  text-decoration: none;
}

.top-contact a:hover,
.language-switch .active {
  color: #22d3ee;
}

.main-header {
  transition: background 0.3s ease;
}

.nav {
  height: 80px;
  justify-content: space-between;
}

.brand {
  gap: 0.75rem;
  text-decoration: none;
  color: white;
}

.brand img {
  width: 42px;
  height: 42px;
  object-fit: contain;
}

.brand strong,
.brand small {
  display: block;
}

.brand strong {
  font-size: 1.2rem;
  font-weight: 850;
}

.brand small {
  margin-top: 0.16rem;
  color: #94a3b8;
  font-size: 0.72rem;
}

.desktop-nav {
  gap: 1.9rem;
}

.nav-link {
  position: relative;
  display: inline-flex;
  align-items: center;
  min-height: 42px;
  color: #cbd5e1;
  text-decoration: none;
  font-weight: 650;
  transition: color 0.25s ease;
}

.nav-link:hover,
.nav-link.active {
  color: #22d3ee;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0.2rem;
  width: 0;
  height: 2px;
  background: #22d3ee;
  transition: width 0.25s ease;
}

.nav-link:hover::after,
.nav-link.active::after {
  width: 100%;
}

.nav-dropdown {
  position: relative;
}

.nav-dropdown-menu {
  position: absolute;
  top: 100%;
  left: 50%;
  width: 248px;
  padding: 0.75rem;
  transform: translate(-50%, 10px);
  opacity: 0;
  visibility: hidden;
  border: 1px solid rgba(148, 163, 184, 0.18);
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.96);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.28);
  backdrop-filter: blur(16px);
  transition: opacity 0.2s ease, transform 0.2s ease, visibility 0.2s ease;
}

.nav-dropdown:hover .nav-dropdown-menu {
  transform: translate(-50%, 0);
  opacity: 1;
  visibility: visible;
}

.nav-dropdown-menu a {
  display: block;
  padding: 0.58rem 0.7rem;
  border-radius: 6px;
  color: #cbd5e1;
  text-decoration: none;
  font-size: 0.9rem;
}

.nav-dropdown-menu a:hover {
  color: white;
  background: rgba(34, 211, 238, 0.12);
}

.nav-actions {
  gap: 1rem;
}

.consult-link,
.mobile-consult {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 42px;
  padding: 0 1.1rem;
  border-radius: 8px;
  color: white;
  background: linear-gradient(135deg, #06b6d4, #2563eb);
  font-weight: 750;
  text-decoration: none;
  box-shadow: 0 12px 28px rgba(14, 165, 233, 0.22);
}

.menu-toggle {
  display: none;
  width: 42px;
  height: 42px;
  border: 1px solid rgba(148, 163, 184, 0.3);
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.52);
  cursor: pointer;
}

.menu-toggle span,
.menu-toggle span::before,
.menu-toggle span::after {
  display: block;
  width: 20px;
  height: 2px;
  margin: 0 auto;
  background: white;
  transition: transform 0.25s ease, opacity 0.25s ease;
}

.menu-toggle span {
  position: relative;
}

.menu-toggle span::before,
.menu-toggle span::after {
  content: '';
  position: absolute;
  left: 0;
}

.menu-toggle span::before {
  top: -6px;
}

.menu-toggle span::after {
  top: 6px;
}

.menu-toggle span.open {
  background: transparent;
}

.menu-toggle span.open::before {
  transform: translateY(6px) rotate(45deg);
}

.menu-toggle span.open::after {
  transform: translateY(-6px) rotate(-45deg);
}

.mobile-overlay,
.mobile-nav {
  display: none;
}

@media (max-width: 1024px) {
  .desktop-nav,
  .consult-link {
    display: none;
  }

  .menu-toggle {
    display: block;
  }

  .brand small {
    display: none;
  }

  .top-contact a:nth-child(2),
  .language-switch {
    display: none;
  }

  .mobile-overlay {
    position: fixed;
    inset: 0;
    z-index: 998;
    background: rgba(2, 6, 23, 0.62);
  }

  .mobile-overlay.open {
    display: block;
  }

  .mobile-nav {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 999;
    width: min(84vw, 360px);
    height: 100vh;
    padding: 112px 1.25rem 2rem;
    overflow-y: auto;
    transform: translateX(100%);
    background: rgba(15, 23, 42, 0.98);
    box-shadow: -20px 0 40px rgba(0, 0, 0, 0.28);
    transition: transform 0.28s ease;
  }

  .mobile-nav.open {
    display: block;
    transform: translateX(0);
  }

  .mobile-nav a,
  .mobile-group button {
    width: 100%;
    display: flex;
    justify-content: space-between;
    padding: 0.85rem 0;
    border: 0;
    border-bottom: 1px solid rgba(148, 163, 184, 0.14);
    color: #e2e8f0;
    background: transparent;
    text-align: left;
    text-decoration: none;
    font: inherit;
  }

  .mobile-nav a.active {
    color: #22d3ee;
  }

  .mobile-submenu {
    padding: 0.25rem 0 0.5rem 1rem;
  }

  .mobile-submenu a {
    color: #94a3b8;
    font-size: 0.92rem;
  }

  .mobile-consult {
    margin-top: 1.25rem;
    border-bottom: 0;
  }
}
</style>
