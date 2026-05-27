<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-grid">
        <div class="footer-col brand-col">
          <div class="footer-logo">
            <img :src="logoImage" alt="Cisetech Logo" />
            <div>
              <strong>Cisetech</strong>
              <span>申朴信息技术（上海）股份有限公司</span>
            </div>
          </div>
          <p class="footer-desc">申信达诚，朴心进取</p>
        </div>

        <div class="footer-col">
          <h4 class="footer-title">核心产品</h4>
          <ul class="footer-links">
            <li v-for="item in productLinks" :key="item.to">
              <router-link :to="item.to">{{ item.label }}</router-link>
            </li>
          </ul>
        </div>

        <div class="footer-col">
          <h4 class="footer-title">联系我们</h4>
          <ul class="footer-contact">
            <li>
              <span class="contact-icon">☎</span>
              <a href="tel:02160756566">(021)-6075 6566</a>
            </li>
            <li>
              <span class="contact-icon">✉</span>
              <a href="mailto:info@cisetech.com">info@cisetech.com</a>
            </li>
            <li>
              <span class="contact-icon">⌖</span>
              <span>上海市浦东新区国展路1529号906-908室</span>
            </li>
          </ul>
        </div>

        <div class="footer-col">
          <h4 class="footer-title">关注我们</h4>
          <div class="wechat-card">
            <img :src="qrImage" alt="微信公众号二维码" />
            <p>扫码关注公众号</p>
          </div>
        </div>
      </div>

      <div class="footer-bottom">
        <p>© 2026 Cisetech. All rights reserved.</p>
        <nav aria-label="页脚链接">
          <a href="#">隐私政策</a>
          <a href="#">使用条款</a>
          <a href="#">网站地图</a>
        </nav>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import logoImage from '../../../../assets/logos/申朴圆点logo.png'
import qrImage from '../../../../assets/logos/申朴服务号二维码.jpg'

const productLinks = [
  { label: '一体化智能可观测平台', to: '/business-detail#product-simple-insight' },
  { label: '国产通用GPU', to: '/business-detail#product-muxi-gpu' },
  { label: 'OceanBase数据库', to: '/business-detail#product-oceanbase' },
  { label: '智能招聘系统', to: '/business-detail#product-ai-recruit' },
  { label: 'AI招投标助手', to: '/business-detail#product-ai-bidding' },
  { label: '职场健康加油站', to: '/business-detail#product-ai-health' },
  { label: '低空综合管理服务平台', to: '/business-detail#product-low-altitude' },
  { label: 'SQL代码审计平台', to: '/business-detail#product-sql-audit' }
]
</script>

<style scoped lang="scss">
.footer {
  position: relative;
  z-index: 2;
  background: #0f172a;
  border-top: 1px solid rgba(51, 65, 85, 0.5);
  color: white;
  padding: 3rem 0 1.75rem;
}

.footer-grid {
  display: grid;
  grid-template-columns: 1.35fr 1fr 1fr 0.9fr;
  gap: 2rem;
}

.footer-logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 1rem;
}

.footer-logo img {
  width: 38px;
  height: 38px;
  object-fit: contain;
}

.footer-logo strong,
.footer-logo span {
  display: block;
}

.footer-logo strong {
  font-size: 1.08rem;
}

.footer-logo span {
  color: #64748b;
  font-size: 0.76rem;
  margin-top: 0.12rem;
}

.footer-desc,
.footer-links a,
.footer-contact,
.footer-bottom,
.footer-bottom a {
  color: #94a3b8;
}

.footer-desc {
  line-height: 1.7;
}

.footer-title {
  position: relative;
  color: white;
  font-size: 1rem;
  font-weight: 800;
  margin-bottom: 1.25rem;
  padding-bottom: 0.65rem;
}

.footer-title::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: 34px;
  height: 2px;
  background: #22d3ee;
}

.footer-links,
.footer-contact {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.7rem;
}

.footer-links a,
.footer-contact a {
  text-decoration: none;
  transition: color 0.2s ease;
}

.footer-links a:hover,
.footer-contact a:hover,
.footer-bottom a:hover {
  color: #22d3ee;
}

.footer-contact li {
  display: flex;
  gap: 0.65rem;
  align-items: flex-start;
  line-height: 1.55;
}

.contact-icon {
  color: #22d3ee;
  width: 1rem;
  flex: 0 0 auto;
}

.wechat-card {
  width: 132px;
  padding: 0.75rem;
  border: 1px solid rgba(148, 163, 184, 0.18);
  border-radius: 8px;
  background: rgba(15, 23, 42, 0.66);
  text-align: center;
}

.wechat-card img {
  width: 100%;
  aspect-ratio: 1;
  object-fit: cover;
  border-radius: 6px;
  background: white;
}

.wechat-card p {
  color: #94a3b8;
  font-size: 0.78rem;
  margin-top: 0.5rem;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  margin-top: 2.5rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(51, 65, 85, 0.7);
  font-size: 0.88rem;
}

.footer-bottom nav {
  display: flex;
  gap: 1.25rem;
}

.footer-bottom a {
  text-decoration: none;
}

@media (max-width: 1024px) {
  .footer-grid {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (max-width: 768px) {
  .footer-grid {
    grid-template-columns: 1fr;
  }

  .footer-bottom {
    align-items: flex-start;
    flex-direction: column;
  }

  .footer-bottom nav {
    flex-wrap: wrap;
  }
}
</style>
