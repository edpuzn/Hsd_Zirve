<template>
  <div id="partners" class="partners-page">
    <div class="container">
      <h1>ETKİNLİK PAYDAŞLARI</h1>
      <p class="subtitle">AI Summit'in gerçekleşmesine katkı sağlayan değerli paydaşlarımız.</p>
      
      <div class="partners-grid">
        <div v-for="(partner, index) in partners" :key="index" class="partner-card">
          <div class="partner-image">
            <img :src="partner.image" :alt="partner.name" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PartnersPage',
  data() {
    return {
      partners: [
        {
          name: 'Atatürk Üniversitesi',
          image: require('@/assets/ATAUNİ.png')
        },
        {
          name: 'ATASOFT',
          image: require('@/assets/ATASOFT.png')
        },
        {
          name: 'Gençlik ve Spor Bakanlığı',
          image: require('@/assets/GSB.png')
        },
        {
          name: 'TÜGVA',
          image: require('@/assets/TUGVA.png')
        },
        {
          name: 'HSD',
          image: require('@/assets/HSD.png')
        },
        {
          name: 'TAZI',
          image: require('@/assets/TAZI.png')
        },
        {
          name: 'ARTIWİSE',
          image: require('@/assets/ARTIWİSE.png')
        },
        {
          name: 'UNIDES',
          image: require('@/assets/UNIDES.png')
        }
      ]
    }
  }
}
</script>

<style scoped>
.partners-page {
  padding: 120px 0 80px;
  background-color: #f8f9fa;
  overflow: hidden;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
  color: #2F3C4E;
  font-size: 2.5rem;
  font-weight: 700;
  text-transform: uppercase;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease forwards;
  font-family: 'Poppins', sans-serif;
}

.subtitle {
  text-align: center;
  color: #2F3C4E;
  font-size: 1.2rem;
  margin-bottom: 60px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease 0.2s forwards;
  font-family: 'Poppins', sans-serif;
}

.partners-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 40px;
  opacity: 0;
  transform: translateY(30px);
  animation: fadeInUp 0.8s ease 0.4s forwards;
}

.partner-card {
  background: white;
  border-radius: 15px;
  padding: 30px;
  text-align: center;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  cursor: pointer;
  transform: translateY(0);
}

.partner-card:nth-child(2) { animation-delay: 0.2s; }
.partner-card:nth-child(3) { animation-delay: 0.4s; }
.partner-card:nth-child(4) { animation-delay: 0.6s; }
.partner-card:nth-child(5) { animation-delay: 0.8s; }
.partner-card:nth-child(6) { animation-delay: 1s; }
.partner-card:nth-child(7) { animation-delay: 1.2s; }
.partner-card:nth-child(8) { animation-delay: 1.4s; }

.partner-card:hover {
  transform: translateY(-15px);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
}

.partner-image {
  width: 100%;
  height: 180px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
}

.partner-image img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  filter: grayscale(100%);
  transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  transform: scale(0.9);
}

.partner-card:hover .partner-image img {
  filter: grayscale(0%);
  transform: scale(1);
}

.partner-card:active {
  transform: translateY(-10px);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.partner-card:active .partner-image img {
  filter: grayscale(0%);
  transform: scale(1.1);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
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

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes scaleIn {
  from {
    transform: scale(0.9);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .partners-page {
    padding: 100px 0 60px;
  }

  h1 {
    font-size: 2rem;
  }

  .subtitle {
    font-size: 1.1rem;
    margin-bottom: 40px;
  }

  .partners-grid {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 30px;
  }

  .partner-card {
    padding: 20px;
  }

  .partner-image {
    height: 120px;
  }
}
</style> 