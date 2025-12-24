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
.image-shape-triangle { clip-path: polygon(50% 0%, 0% 100%, 100% 100%); }
.image-shape-star { clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%); }
.image-shape-heart { clip-path: polygon(50% 20%, 60% 10%, 70% 10%, 80% 20%, 80% 35%, 50% 80%, 20% 35%, 20% 20%, 30% 10%, 40% 10%); }
.image-shape-shield { clip-path: polygon(50% 0%, 100% 20%, 100% 60%, 50% 100%, 0% 60%, 0% 20%); }
.image-shape-parallelogram { clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%); }
.image-shape-trapezoid { clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%); }
.image-shape-ellipse { border-radius: 50%; transform: scaleX(1.4); }
.image-shape-squircle { border-radius: 35%; }
.image-shape-teardrop { clip-path: polygon(50% 0%, 70% 10%, 85% 30%, 90% 50%, 85% 70%, 70% 85%, 50% 100%, 30% 85%, 15% 70%, 10% 50%, 15% 30%, 30% 10%); transform: rotate(45deg); }
.image-shape-arch { clip-path: ellipse(40% 35% at 50% 100%); }
.image-shape-cross { clip-path: polygon(40% 0%, 60% 0%, 60% 40%, 100% 40%, 100% 60%, 60% 60%, 60% 100%, 40% 100%, 40% 60%, 0% 60%, 0% 40%, 40% 40%); }
.image-shape-badge { clip-path: polygon(50% 0%, 65% 5%, 75% 15%, 85% 25%, 95% 40%, 100% 50%, 95% 60%, 85% 75%, 75% 85%, 65% 95%, 50% 100%, 35% 95%, 25% 85%, 15% 75%, 5% 60%, 0% 50%, 5% 40%, 15% 25%, 25% 15%, 35% 5%); }
.image-shape-ticket { clip-path: polygon(10% 10%, 90% 10%, 90% 40%, 85% 45%, 85% 55%, 90% 60%, 90% 90%, 10% 90%, 10% 60%, 15% 55%, 15% 45%, 10% 40%); }
.image-shape-chevron { clip-path: polygon(0% 0%, 75% 0%, 100% 50%, 75% 100%, 0% 100%, 25% 50%); }
.image-shape-arrow { clip-path: polygon(0% 30%, 70% 30%, 70% 0%, 100% 50%, 70% 100%, 70% 70%, 0% 70%); }
.image-shape-clover { clip-path: polygon(50% 20%, 60% 10%, 65% 5%, 70% 10%, 75% 20%, 85% 20%, 90% 25%, 95% 30%, 90% 40%, 80% 50%, 90% 60%, 95% 70%, 90% 75%, 85% 80%, 75% 80%, 70% 90%, 65% 95%, 60% 90%, 50% 80%, 40% 90%, 35% 95%, 30% 90%, 25% 80%, 15% 80%, 10% 75%, 5% 70%, 10% 60%, 20% 50%, 10% 40%, 5% 30%, 10% 25%, 15% 20%, 25% 20%, 30% 10%, 35% 5%, 40% 10%); }

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
