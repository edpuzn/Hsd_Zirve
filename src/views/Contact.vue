<template>
  <div id="contact" class="contact-page">
    <div class="container">
      <h1>BİZE ULAŞIN</h1>
      <p class="subtitle">Etkinlik ile ilgili sorularınız için bizimle iletişime geçebilir veya sosyal medya kanallarımızdan bizi takip edebilirsiniz.</p>
      
      <div class="contact-content">
        <div class="contact-info">
          <div class="address">
            <h3>Adres</h3>
            <p>Atatürk Üniversitesi 15 Temmuz Milli İrade Konferans Salonu<br>
            Atatürk Üniversitesi Rektörlük Binası Yanı KÜLTÜR MERKEZİ, Erzurum</p>
          </div>
          
          <a href="https://linktr.ee/aisummiterzurum" class="cta-button" target="_blank">ŞİMDİ BAŞVUR</a>
          
          <div class="social-media">
            <h3>Sosyal Medya Hesaplarımız</h3>
            <div class="social-links">
              <a href="#" target="_blank"><i class="fab fa-linkedin"></i> AI Summit LinkedIn</a>
              <a href="#" target="_blank"><i class="fab fa-instagram"></i> AI Summit Instagram</a>
              <a href="#" target="_blank"><i class="fab fa-instagram"></i> Atasoft Instagram</a>
              <a href="#" target="_blank"><i class="fab fa-instagram"></i> HSD</a>
              <a href="#" target="_blank"><i class="fab fa-instagram"></i> Atatürk Üniversitesi Instagram</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ContactPage'
}
</script>

<style scoped>
.contact-page {
  padding: 120px 0 80px;
  background-color: #f8f9fa;
  overflow: hidden;
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.contact-page.active {
  opacity: 1;
  transform: translateY(0);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
  font-size: 2.5rem;
  font-weight: 700;
  text-transform: uppercase;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) forwards;
  font-family: 'Poppins', sans-serif;
}

.subtitle {
  text-align: center;
  color: #666;
  font-size: 1.2rem;
  margin-bottom: 60px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.2s forwards;
  font-family: 'Poppins', sans-serif;
}

.contact-content {
  max-width: 800px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.4s forwards;
}

.contact-info {
  background: white;
  padding: 50px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.address {
  margin-bottom: 40px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.6s forwards;
}

.address h3 {
  color: #333;
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 20px;
  font-family: 'Poppins', sans-serif;
}

.address p {
  color: #666;
  line-height: 1.8;
  font-size: 1.1rem;
  font-family: 'Poppins', sans-serif;
}

.cta-button {
  background-color: #2F3C4E;
  color: white;
  padding: 12px 30px;
  border-radius: 30px;
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  display: inline-block;
  margin-top: 20px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 0.8s forwards;
}

.cta-button:hover {
  background-color: #2F3C4E;
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(47, 60, 78, 0.3);
}

.social-media {
  margin-top: 40px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s cubic-bezier(0.4, 0, 0.2, 1) 1s forwards;
}

.social-media h3 {
  color: #333;
  font-size: 1.5rem;
  font-weight: 600;
  margin-bottom: 25px;
  font-family: 'Poppins', sans-serif;
}

.social-links {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.social-links a {
  color: #2F3C4E;
  text-decoration: none;
  transition: color 0.3s ease;
  opacity: 0;
  transform: translateX(-20px);
}

.social-links a:hover {
  color: #2F3C4E;
  text-decoration: underline;
}

.social-links i {
  font-size: 1.5rem;
  color: #007bff;
}

.contact-page.active .social-links a:nth-child(1) { animation: slideInRight 0.5s cubic-bezier(0.4, 0, 0.2, 1) 1.2s forwards; }
.contact-page.active .social-links a:nth-child(2) { animation: slideInRight 0.5s cubic-bezier(0.4, 0, 0.2, 1) 1.3s forwards; }
.contact-page.active .social-links a:nth-child(3) { animation: slideInRight 0.5s cubic-bezier(0.4, 0, 0.2, 1) 1.4s forwards; }
.contact-page.active .social-links a:nth-child(4) { animation: slideInRight 0.5s cubic-bezier(0.4, 0, 0.2, 1) 1.5s forwards; }
.contact-page.active .social-links a:nth-child(5) { animation: slideInRight 0.5s cubic-bezier(0.4, 0, 0.2, 1) 1.6s forwards; }

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

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(-20px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@media (max-width: 768px) {
  .contact-page {
    padding: 100px 0 60px;
  }

  h1 {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1.1rem;
    margin-bottom: 40px;
  }

  .contact-info {
    padding: 30px;
  }

  .address h3,
  .social-media h3 {
    font-size: 1.3rem;
  }

  .address p {
    font-size: 1rem;
  }

  .cta-button {
    font-size: 1.1rem;
    padding: 12px 30px;
  }

  .social-links a {
    font-size: 1rem;
  }
}
</style> 