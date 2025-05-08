<template>
  <div id="home" class="home-page">
    <section class="hero">
      <div class="animated-background">
        <div class="gradient-sphere"></div>
        <div class="gradient-sphere"></div>
        <div class="gradient-sphere"></div>
        <canvas id="particleCanvas"></canvas>
      </div>
      <div class="container">
        <h1>FIRAT VISION FEST 2025</h1>
        <p class="date">29 Mayıs 2025 | FIRAT ÜNİVERSİTESİ</p>
         
        <div class="countdown">
          <div class="countdown-item">
            <span class="number">{{ days }}</span>
            <span class="label">Gün</span>
          </div>
          <div class="countdown-item">
            <span class="number">{{ hours }}</span>
            <span class="label">Saat</span>
          </div>
          <div class="countdown-item">
            <span class="number">{{ minutes }}</span>
            <span class="label">Dakika</span>
          </div>
          <div class="countdown-item">
            <span class="number">{{ seconds }}</span>
            <span class="label">Saniye</span>
          </div>
        </div>

        <p class="cta-text">Aramızda sizi de görmek isteriz.</p>
        <a href="https://linktr.ee/hsdfirat" class="cta-button" target="_blank">Linktr.ee/hsdfirat</a>
      </div>
    </section>

    <section class="about-section">
      <div class="container">
        <h2>FIRAT VISION FEST NEDİR?</h2>
        <div class="about-content">
          <div class="about-text">
            <p>AI Summit, yapay zeka teknolojilerinin tüm yönleriyle ele alındığı, alanında uzman konuşmacıların katılımıyla gerçekleşen önemli bir teknoloji zirvesidir. 2025 yılında "Makineler Düşünebilir mi?" temasıyla Atatürk Üniversitesi'nde düzenlenecek olan etkinlik, yapay zeka alanındaki son gelişmeleri, uygulamaları ve etik konuları masaya yatıracak.</p>
            <p>İki gün sürecek etkinlikte, akademisyenler, sektör temsilcileri ve öğrenciler bir araya gelerek yapay zeka teknolojilerinin geleceğini tartışacak, yeni fikirler üretecek ve işbirlikleri geliştirecekler.</p>
          </div>
        </div>
      </div>
    </section>

    <section class="features">
      <div class="container">
        <h2>Neden Katılmalısınız?</h2>
        <div class="features-grid">
          <div class="feature-card">
            <i class="fas fa-users"></i>
            <h3>Uzman Konuşmacılar</h3>
            <p>Alanında uzman konuşmacılardan yapay zeka teknolojilerinin en son gelişmelerini dinleyin.</p>
          </div>
          <div class="feature-card">
            <i class="fas fa-handshake"></i>
            <h3>Networking</h3>
            <p>Akademisyenler, sektör temsilcileri ve öğrencilerle tanışma ve işbirliği fırsatı yakalayın.</p>
          </div>
          <div class="feature-card">
            <i class="fas fa-lightbulb"></i>
            <h3>İlham Verici İçerik</h3>
            <p>Yapay zeka alanındaki yenilikçi projeler ve uygulamalar hakkında bilgi edinin.</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data() {
    return {
      eventDate: new Date('2025-05-29T00:00:00'),
      days: '00',
      hours: '00',
      minutes: '00',
      seconds: '00',
      canvas: null,
      ctx: null,
      particles: [],
      mouse: {
        x: null,
        y: null,
        radius: 150
      }
    }
  },
  mounted() {
    this.updateCountdown()
    setInterval(this.updateCountdown, 1000)
    this.initParticles()
    window.addEventListener('mousemove', this.handleMouseMove)
    window.addEventListener('resize', this.handleResize)
  },
  beforeUnmount() {
    window.removeEventListener('mousemove', this.handleMouseMove)
    window.removeEventListener('resize', this.handleResize)
  },
  methods: {
    updateCountdown() {
      const now = new Date()
      const diff = this.eventDate - now

      if (diff > 0) {
        const days = Math.floor(diff / (1000 * 60 * 60 * 24))
        const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60))
        const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60))
        const seconds = Math.floor((diff % (1000 * 60)) / 1000)

        this.days = days.toString().padStart(2, '0')
        this.hours = hours.toString().padStart(2, '0')
        this.minutes = minutes.toString().padStart(2, '0')
        this.seconds = seconds.toString().padStart(2, '0')
      }
    },
    initParticles() {
      this.canvas = document.getElementById('particleCanvas')
      this.ctx = this.canvas.getContext('2d')
      this.resizeCanvas()
      this.createParticles()
      this.animate()
    },
    resizeCanvas() {
      this.canvas.width = window.innerWidth
      this.canvas.height = window.innerHeight
    },
    createParticles() {
      const numberOfParticles = 100
      for (let i = 0; i < numberOfParticles; i++) {
        this.particles.push({
          x: Math.random() * this.canvas.width,
          y: Math.random() * this.canvas.height,
          size: Math.random() * 2 + 1,
          speedX: Math.random() * 2 - 1,
          speedY: Math.random() * 2 - 1,
          color: `rgba(255, 255, 255, ${Math.random() * 0.5 + 0.1})`
        })
      }
    },
    handleMouseMove(e) {
      this.mouse.x = e.x
      this.mouse.y = e.y
    },
    handleResize() {
      this.resizeCanvas()
    },
    animate() {
      this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height)
      
      // Update and draw particles
      this.particles.forEach(particle => {
        // Move particles
        particle.x += particle.speedX
        particle.y += particle.speedY

        // Bounce off edges
        if (particle.x < 0 || particle.x > this.canvas.width) particle.speedX *= -1
        if (particle.y < 0 || particle.y > this.canvas.height) particle.speedY *= -1

        // Mouse interaction
        if (this.mouse.x !== null && this.mouse.y !== null) {
          const dx = this.mouse.x - particle.x
          const dy = this.mouse.y - particle.y
          const distance = Math.sqrt(dx * dx + dy * dy)
          
          if (distance < this.mouse.radius) {
            const angle = Math.atan2(dy, dx)
            const force = (this.mouse.radius - distance) / this.mouse.radius
            particle.x -= Math.cos(angle) * force * 2
            particle.y -= Math.sin(angle) * force * 2
          }
        }

        // Draw particle
        this.ctx.beginPath()
        this.ctx.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2)
        this.ctx.fillStyle = particle.color
        this.ctx.fill()
      })

      // Draw connections
      this.particles.forEach((particle, index) => {
        for (let j = index + 1; j < this.particles.length; j++) {
          const dx = particle.x - this.particles[j].x
          const dy = particle.y - this.particles[j].y
          const distance = Math.sqrt(dx * dx + dy * dy)

          if (distance < 100) {
            this.ctx.beginPath()
            this.ctx.strokeStyle = `rgba(255, 255, 255, ${0.2 * (1 - distance / 100)})`
            this.ctx.lineWidth = 0.5
            this.ctx.moveTo(particle.x, particle.y)
            this.ctx.lineTo(this.particles[j].x, this.particles[j].y)
            this.ctx.stroke()
          }
        }
      })

      requestAnimationFrame(this.animate)
    }
  }
}
</script>

<style scoped>
.home-page {
  min-height: 100vh;
  overflow: hidden;
}

.hero {
  position: relative;
  background: #000000;
  color: white;
  text-align: center;
  padding: 200px 0;
  margin-top: -80px;
  overflow: hidden;
}

.animated-background {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
}

.gradient-sphere {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.7;
  animation: float 15s infinite;
}

.gradient-sphere:nth-child(1) {
  width: 700px;
  height: 700px;
  background: radial-gradient(circle, rgba(74, 144, 226, 0.8) 0%, rgba(74, 144, 226, 0.2) 50%, transparent 70%);
  top: -200px;
  left: -100px;
  animation-delay: 0s;
}

.gradient-sphere:nth-child(2) {
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(47, 60, 78, 0.8) 0%, rgba(47, 60, 78, 0.2) 50%, transparent 70%);
  top: 50%;
  right: -100px;
  animation-delay: -5s;
}

.gradient-sphere:nth-child(3) {
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, rgba(26, 31, 43, 0.8) 0%, rgba(26, 31, 43, 0.2) 50%, transparent 70%);
  bottom: -100px;
  left: 30%;
  animation-delay: -10s;
}

.particles {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    radial-gradient(circle at 25% 25%, rgba(255, 255, 255, 0.2) 1px, transparent 1px),
    radial-gradient(circle at 75% 75%, rgba(255, 255, 255, 0.2) 1px, transparent 1px);
  background-size: 50px 50px;
  animation: particleMove 20s linear infinite;
}

.container {
  position: relative;
  z-index: 2;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

h1 {
  font-size: 3.2rem;
  font-weight: 700;
  margin-bottom: 15px;
  text-transform: uppercase;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) forwards;
  font-family: 'Poppins', sans-serif;
}

.date {
  font-size: 1.4rem;
  margin-bottom: 30px;
  font-weight: 300;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.2s forwards;
  font-family: 'Poppins', sans-serif;
}

.countdown {
  display: flex;
  justify-content: center;
  gap: 25px;
  margin-bottom: 35px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.4s forwards;
}

.countdown-item {
  text-align: center;
  background: rgba(255, 255, 255, 0.15);
  padding: 15px 25px;
  border-radius: 12px;
  min-width: 100px;
  backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  opacity: 0;
  transform: scale(0.8);
  animation: scaleIn 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}

.countdown-item .number {
  font-size: 2.5rem;
  font-weight: 700;
  display: block;
  margin-bottom: 5px;
  font-family: 'Poppins', sans-serif;
  color: #fff;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.countdown-item .label {
  font-size: 0.9rem;
  text-transform: uppercase;
  font-weight: 400;
  font-family: 'Poppins', sans-serif;
  color: rgba(255, 255, 255, 0.9);
  letter-spacing: 1px;
}

.cta-text {
  font-size: 1.3rem;
  margin-bottom: 15px;
  font-weight: 300;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 1s forwards;
  font-family: 'Poppins', sans-serif;
}

.cta-button {
  background-color: #2F3C4E;
  color: white;
  padding: 10px 25px;
  border-radius: 25px;
  text-decoration: none;
  font-weight: 500;
  font-size: 1.1rem;
  transition: all 0.3s ease;
  display: inline-block;
  margin-top: 15px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 1.2s forwards;
  border: 2px solid #2F3C4E;
}

.cta-button:hover {
  background-color: transparent;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(47, 60, 78, 0.3);
}

.about-section {
  padding: 100px 0;
  background-color: #f8f9fa;
  opacity: 1;
  transform: translateY(0);
}

.about-section h2 {
  text-align: center;
  margin-bottom: 40px;
  color: #2F3C4E;
  font-size: 2.5rem;
  font-weight: 700;
  text-transform: uppercase;
  opacity: 1;
  transform: translateY(0);
  font-family: 'Poppins', sans-serif;
}

.about-content {
  max-width: 900px;
  margin: 0 auto;
  opacity: 1;
  transform: translateY(0);
}

.about-text p {
  margin-bottom: 20px;
  line-height: 1.8;
  color: #2F3C4E;
  font-size: 1.1rem;
  text-align: justify;
  font-family: 'Poppins', sans-serif;
}

.about-text p:last-child {
  margin-bottom: 0;
}

.features {
  padding: 100px 0;
  background-color: white;
  opacity: 1;
  transform: translateY(0);
}

.features h2 {
  text-align: center;
  margin-bottom: 60px;
  color: #2F3C4E;
  font-size: 2.5rem;
  font-weight: 700;
  text-transform: uppercase;
  opacity: 1;
  transform: translateY(0);
  font-family: 'Poppins', sans-serif;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 40px;
  opacity: 1;
  transform: translateY(0);
}

.feature-card {
  text-align: center;
  padding: 40px 30px;
  background: #f8f9fa;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  opacity: 1;
  transform: translateY(0);
}

.feature-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(74, 144, 226, 0.2);
  background: rgba(255, 255, 255, 0.1);
}

.feature-card i {
  font-size: 3rem;
  color: #4a90e2;
  margin-bottom: 25px;
}

.feature-card h3 {
  color: #2F3C4E;
  font-size: 1.5rem;
  margin-bottom: 15px;
  font-weight: 600;
  font-family: 'Poppins', sans-serif;
}

.feature-card p {
  color: #2F3C4E;
  line-height: 1.8;
  font-size: 1.1rem;
  font-family: 'Poppins', sans-serif;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes scaleIn {
  from {
    opacity: 0;
    transform: scale(0.8);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes float {
  0%, 100% {
    transform: translate(0, 0) scale(1);
  }
  25% {
    transform: translate(50px, 50px) scale(1.1);
  }
  50% {
    transform: translate(0, 100px) scale(1);
  }
  75% {
    transform: translate(-50px, 50px) scale(0.9);
  }
}

@keyframes particleMove {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 50px 50px;
  }
}

#particleCanvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

@media (max-width: 768px) {
  .hero {
    padding: 120px 0;
  }

  h1 {
    font-size: 2.2rem;
  }

  .date {
    font-size: 1.1rem;
  }

  .countdown {
    gap: 10px;
  }

  .countdown-item {
    min-width: 70px;
    padding: 12px 15px;
  }

  .countdown-item .number {
    font-size: 1.8rem;
  }

  .countdown-item .label {
    font-size: 0.8rem;
  }

  .cta-text {
    font-size: 1.1rem;
  }

  .cta-button {
    font-size: 1rem;
    padding: 10px 20px;
  }

  .about-section,
  .features {
    padding: 60px 0;
  }

  .about-section h2,
  .features h2 {
    font-size: 2rem;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }
}
</style> 