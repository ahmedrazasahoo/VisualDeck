<template>
  <div class="fullwidth-card wave-fullwidth-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="wave-section-fullwidth header-section">
      <div class="content-wrapper">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
        <div v-if="showIdBadge" class="wave-id-badge">{{ card.id }}</div>
      </div>
    </div>

    <div class="wave-section-fullwidth content-section">
      <div class="content-wrapper">
        <h3 class="wave-title">{{ card.title }}</h3>
        <div v-if="showCategory" class="wave-category">{{ card.category }}</div>
      </div>
    </div>

    <div v-if="showDescription" class="wave-section-fullwidth description-section">
      <div class="content-wrapper">
        <p class="wave-description">{{ card.description }}</p>
      </div>
    </div>

    <div v-if="showPrice" class="wave-section-fullwidth price-section">
      <svg class="wave-divider-top" viewBox="0 0 1200 120" preserveAspectRatio="none">
        <path d="M321.39,56.44c58-10.79,114.16-30.13,172-41.86,82.39-16.72,168.19-17.73,250.45-.39C823.78,31,906.67,72,985.66,92.83c70.05,18.48,146.53,26.09,214.34,3V0H0V27.35A600.21,600.21,0,0,0,321.39,56.44Z"></path>
      </svg>
      <div class="content-wrapper">
        <span class="wave-price">{{ card.price }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  card: { type: Object, required: true },
  primaryColor: { type: String, default: '#667eea' },
  secondaryColor: { type: String, default: '#764ba2' },
  primaryColorOpacity: { type: Number, default: 1 },
  secondaryColorOpacity: { type: Number, default: 1 },
  imageShape: { type: String, default: 'rounded' },
  showIdBadge: { type: Boolean, default: true },
  showCategory: { type: Boolean, default: true },
  showDescription: { type: Boolean, default: true },
  showPrice: { type: Boolean, default: true },
  cardBackgroundColor: { type: String, default: '#ffffff' },
  cardTitleColor: { type: String, default: '#222222' },
  cardDescriptionColor: { type: String, default: '#555555' },
  cardPriceColor: { type: String, default: '#ffffff' },
  cardCategoryBgColor: { type: String, default: '#667eea' }
});

const hexToRgb = (hex) => {
  const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
  return result ? {
    r: parseInt(result[1], 16),
    g: parseInt(result[2], 16),
    b: parseInt(result[3], 16)
  } : { r: 102, g: 126, b: 234 };
};

const primaryColorRgba = computed(() => {
  const rgb = hexToRgb(props.primaryColor);
  return `rgba(${rgb.r}, ${rgb.g}, ${rgb.b}, ${props.primaryColorOpacity})`;
});

const secondaryColorRgba = computed(() => {
  const rgb = hexToRgb(props.secondaryColor);
  return `rgba(${rgb.r}, ${rgb.g}, ${rgb.b}, ${props.secondaryColorOpacity})`;
});
</script>

<style scoped>
.fullwidth-card {
  width: 100%;
  min-height: var(--card-height, 520px);
  background: v-bind(cardBackgroundColor);
  border-radius: var(--card-radius, 16px);
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.fullwidth-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.25);
}

.wave-section-fullwidth {
  width: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.content-wrapper {
  width: 100%;
  max-width: var(--content-max-width, 800px);
  margin: 0 auto;
  padding: 0 var(--content-padding, 16px);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 1;
}

.header-section {
  min-height: 250px;
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  overflow: hidden;
  padding: 2rem 0;
}

.header-section .content-wrapper {
  height: 100%;
}

.card-image {
  width: 100%;
  max-width: 600px;
  height: 250px;
  object-fit: cover;
  object-position: center;
  transition: transform 0.3s ease, opacity 0.3s ease;
  opacity: 0.9;
  border-radius: 8px;
  padding: var(--image-padding, 0px);
}

.fullwidth-card:hover .card-image {
  transform: scale(1.03);
  opacity: 1;
}

.wave-id-badge {
  position: absolute;
  top: 2rem;
  left: 2rem;
  background: rgba(255, 255, 255, 0.95);
  color: #333;
  padding: 0.6rem 1.2rem;
  border-radius: 50%;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 800;
  width: 45px;
  height: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
  z-index: 2;
}

.content-section {
  padding: 2rem 0 1.5rem;
  background: v-bind(cardBackgroundColor);
}

.wave-title {
  margin: 0 0 1rem 0;
  font-size: var(--heading-size, 1.5rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
  text-align: center;
}

.wave-category {
  display: inline-block;
  background: v-bind(cardCategoryBgColor);
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 25px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.description-section {
  flex: 1;
  padding: 2rem 0;
  background: v-bind(cardBackgroundColor);
  min-height: 120px;
}

.wave-description {
  margin: 0;
  font-size: var(--text-size, 0.95rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.7;
  text-align: center;
  max-width: 700px;
}

.price-section {
  padding: 2.5rem 0 2rem;
  background: linear-gradient(135deg, var(--secondary-color-rgba) 0%, var(--primary-color-rgba) 100%);
  position: relative;
  overflow: visible;
}

.wave-divider-top {
  position: absolute;
  top: -1px;
  left: 0;
  width: 100%;
  height: 60px;
  fill: v-bind(cardBackgroundColor);
  z-index: 1;
}

.wave-price {
  font-size: var(--price-size, 1.6rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
  letter-spacing: 1px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  text-align: center;
  position: relative;
  z-index: 2;
  display: block;
}

.image-shape-rounded { border-radius: 8px; }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(40% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }

@media (max-width: 768px) {
  .content-wrapper {
    max-width: 100%;
  }
  
  .card-image {
    max-width: 100%;
    height: 200px;
  }
  
  .wave-id-badge {
    left: 1rem;
    top: 1rem;
  }
  
  .wave-title {
    font-size: var(--heading-size, 1.3rem);
  }
  
  .wave-price {
    font-size: var(--price-size, 1.4rem);
  }
}
</style>
