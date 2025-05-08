<template>
  <div class="app">
    <nav class="navbar" :class="{ scrolled: isScrolled }">
      <div class="container">
        <div class="logo">
          <img src="@/assets/HSD.png" alt="AI Summit Logo" />
        </div>
        <div class="nav-links">
          <router-link to="#home">Ana Sayfa</router-link>
          <router-link to="#about">Hakkımızda</router-link>
          <router-link to="#speakers">Konuşmacılar</router-link>
          <router-link to="#partners">Paydaşlar</router-link>
          <router-link to="#contact">İletişim</router-link>
        </div>
      </div>
    </nav>

    <Home />
    <Speakers />
    <Partners />
    <Contact />

    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-logo">
            <img src="@/assets/HSD.png" alt="AI Summit Logo" />
            <p>Yapay zeka teknolojilerinin geleceğini şekillendiriyoruz.</p>
          </div>
          <div class="footer-links">
            <h3>Hızlı Bağlantılar</h3>
            <router-link to="#home">Ana Sayfa</router-link>
            <router-link to="#about">Hakkımızda</router-link>
            <router-link to="#speakers">Konuşmacılar</router-link>
            <router-link to="#partners">Paydaşlar</router-link>
            <router-link to="#contact">İletişim</router-link>
          </div>
          <div class="footer-cta">
            <h3>Etkinliğe Katılın</h3>
            <p>3-4 Mayıs 2025'te siz de aramızda olun!</p>
            <a href="https://linktr.ee/aisummiterzurum" class="cta-button" target="_blank">ŞİMDİ BAŞVUR</a>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2024 AI Summit. Tüm hakları saklıdır.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import Home from '@/views/Home.vue'
import About from '@/views/About.vue'
import Speakers from '@/views/Speakers.vue'
import Partners from '@/views/Partners.vue'
import Contact from '@/views/Contact.vue'

export default {
  name: 'App',
  components: {
    Home,
    Speakers,
    Partners,
    Contact
  },
  data() {
    return {
      isScrolled: false,
      currentSection: 'home'
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
    window.addEventListener('scroll', this.handleSectionVisibility)

    if (window.location.hash) {
      setTimeout(() => {
        const element = document.querySelector(window.location.hash)
        if (element) {
          element.scrollIntoView({ behavior: 'smooth' })
        }
      }, 100)
    }

    document.querySelectorAll('router-link').forEach(link => {
      link.addEventListener('click', function (e) {
        e.preventDefault()
        const target = document.querySelector(this.getAttribute('to'))
        if (target) {
          target.scrollIntoView({ behavior: 'smooth' })
        }
      })
    })
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
    window.removeEventListener('scroll', this.handleSectionVisibility)
  },
  methods: {
    handleScroll() {
      this.isScrolled = window.scrollY > 50
    },
    handleSectionVisibility() {
      const sections = ['home', 'about', 'speakers', 'partners', 'contact']
      const scrollPosition = window.scrollY + window.innerHeight / 2

      sections.forEach(section => {
        const element = document.getElementById(section)
        if (element) {
          const rect = element.getBoundingClientRect()
          const elementTop = rect.top + window.scrollY
          const elementBottom = elementTop + rect.height

          if (scrollPosition >= elementTop && scrollPosition <= elementBottom) {
            this.currentSection = section
            element.classList.add('active')
          }
        }
      })
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');

html {
  scroll-behavior: smooth;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Poppins', sans-serif;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* Sayfa Geçiş Animasyonları */
#home, #about, #speakers, #partners, #contact {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

#home.active, #about.active, #speakers.active, #partners.active, #contact.active {
  opacity: 1;
  transform: translateY(0);
}

/* Navbar Animasyonları */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(255, 255, 255, 0.95);
  padding: 20px 0;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
}

.navbar.scrolled {
  background: rgba(47, 60, 78, 0.95);
  padding: 15px 0;
}

.navbar.scrolled .nav-links a {
  color: white;
}

.navbar.scrolled .nav-links a:hover {
  color: #2F3C4E;
}

.navbar.scrolled .nav-links a::after {
  background-color: #2F3C4E;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.navbar .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo img {
  height: 50px;
  transition: all 0.3s ease;
}

.navbar.scrolled .logo img {
  height: 55px;
}

.nav-links {
  display: flex;
  gap: 30px;
}

.nav-links a,
.footer-links a {
  color: #333;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 500;
  transition: all 0.3s ease;
  position: relative;
}

.nav-links a::after,
.footer-links a::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #2F3C4E;
  transition: width 0.3s ease;
}

.nav-links a:hover::after,
.footer-links a:hover::after {
  width: 100%;
}

.nav-links a:hover,
.footer-links a:hover {
  color: #2F3C4E;
}

.footer {
  background-color: #333;
  color: white;
  padding: 80px 0 20px;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 40px;
  margin-bottom: 40px;
}

.footer-logo img {
  height: 50px;
  margin-bottom: 20px;
}

.footer-logo p {
  color: #ccc;
  line-height: 1.6;
}

.footer-links h3,
.footer-cta h3 {
  color: white;
  font-size: 1.3rem;
  margin-bottom: 20px;
}

.footer-links {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.footer-links a {
  color: #ccc;
  text-decoration: none;
  transition: all 0.3s ease;
  font-size: 1.1rem;
}

.footer-links a:hover {
  color: white;
  transform: translateX(5px);
}

.footer-cta {
  background: rgba(255, 255, 255, 0.1);
  padding: 30px;
  border-radius: 15px;
  text-align: center;
}

.footer-cta h3 {
  color: white;
  font-size: 1.5rem;
  margin-bottom: 15px;
  font-weight: 600;
}

.footer-cta p {
  color: #ccc;
  margin-bottom: 25px;
  font-size: 1.1rem;
  line-height: 1.6;
}

.footer-cta .cta-button {
  background-color: #2F3C4E;
  color: white;
  padding: 15px 40px;
  border-radius: 30px;
  text-decoration: none;
  font-weight: 600;
  font-size: 1.2rem;
  transition: all 0.3s ease;
  display: inline-block;
  border: 2px solid #2F3C4E;
}

.footer-cta .cta-button:hover {
  background-color: transparent;
  transform: translateY(-3px);
  box-shadow: 0 5px 15px rgba(47, 60, 78, 0.3);
}

.footer-bottom {
  text-align: center;
  padding-top: 20px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.footer-bottom p {
  color: #ccc;
}

@media (max-width: 768px) {
  .navbar {
    padding: 15px 0;
  }

  .logo img {
    height: 40px;
  }

  .nav-links {
    display: none;
  }

  .footer {
    padding: 60px 0 20px;
  }

  .footer-content {
    grid-template-columns: 1fr;
    gap: 30px;
  }
}
</style>
