<template>
  <div class="fullwidth-card curved-fullwidth-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="curved-section-fullwidth image-curve-full">
      <div class="curved-background-full">
        <svg class="curve-shape-full" viewBox="0 0 1200 300" preserveAspectRatio="none">
          <path d="M0,0 L1200,0 L1200,240 Q600,300 0,240 Z" />
        </svg>
      </div>
      <div class="content-wrapper">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
        <div v-if="showIdBadge" class="curved-badge">#{{ card.id }}</div>
      </div>
    </div>

    <div class="curved-section-fullwidth title-curve-full">
      <div class="curved-background-full">
        <svg class="curve-shape-full" viewBox="0 0 1200 120" preserveAspectRatio="none">
          <path d="M0,60 Q600,0 1200,60 L1200,120 L0,120 Z" />
        </svg>
      </div>
      <div class="content-wrapper">
        <h3 class="curved-title">{{ card.title }}</h3>
      </div>
    </div>

    <div v-if="showCategory" class="curved-section-fullwidth category-curve-full">
      <div class="content-wrapper">
        <span class="curved-category">{{ card.category }}</span>
      </div>
    </div>

    <div v-if="showDescription" class="curved-section-fullwidth description-curve-full">
      <div class="content-wrapper">
        <p class="curved-description">{{ card.description }}</p>
      </div>
    </div>

    <div v-if="showPrice" class="curved-section-fullwidth price-curve-full">
      <div class="curved-background-full">
        <svg class="curve-shape-full" viewBox="0 0 1200 100" preserveAspectRatio="none">
          <path d="M0,0 Q600,60 1200,0 L1200,100 L0,100 Z" />
        </svg>
      </div>
      <div class="content-wrapper">
        <span class="curved-price">{{ card.price }}</span>
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
  cardTitleColor: { type: String, default: '#ffffff' },
  cardDescriptionColor: { type: String, default: '#444444' },
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
  box-shadow: 0 10px 35px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.fullwidth-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 18px 50px rgba(0, 0, 0, 0.25);
}

.curved-section-fullwidth {
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
  z-index: 2;
}

.curved-background-full {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 0;
}

.curve-shape-full {
  width: 100%;
  height: 100%;
  fill: currentColor;
}

.image-curve-full {
  min-height: 280px;
  position: relative;
  overflow: visible;
  color: var(--primary-color-rgba);
  margin-bottom: -30px;
  padding: 2rem 0;
}

.card-image {
  width: 100%;
  max-width: 600px;
  height: 250px;
  object-fit: cover;
  object-position: center;
  transition: transform 0.3s ease;
  border-radius: 8px;
  padding: var(--image-padding, 0px);
}

.fullwidth-card:hover .card-image {
  transform: scale(1.05);
}

.curved-badge {
  position: absolute;
  top: 2rem;
  right: 2rem;
  background: rgba(255, 255, 255, 0.95);
  color: #333;
  padding: 0.6rem 1.2rem;
  border-radius: 30px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 800;
  letter-spacing: 1px;
  z-index: 3;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.title-curve-full {
  position: relative;
  color: var(--secondary-color-rgba);
  padding: 2.5rem 0 1.5rem;
  margin-bottom: -15px;
}

.curved-title {
  position: relative;
  z-index: 2;
  margin: 0;
  font-size: var(--heading-size, 1.5rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
  text-align: center;
}

.category-curve-full {
  padding: 1.5rem 0;
  background: #f8f9fa;
}

.curved-category {
  display: inline-block;
  background: v-bind(cardCategoryBgColor);
  color: white;
  padding: 0.6rem 1.5rem;
  border-radius: 30px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.description-curve-full {
  flex: 1;
  padding: 2rem 0;
  background: #f8f9fa;
  min-height: 120px;
}

.curved-description {
  margin: 0;
  font-size: var(--text-size, 0.95rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.7;
  text-align: center;
  max-width: 700px;
}

.price-curve-full {
  position: relative;
  color: var(--primary-color-rgba);
  padding: 2.5rem 0 2rem;
  margin-top: -20px;
}

.curved-price {
  position: relative;
  z-index: 2;
  font-size: var(--price-size, 1.6rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
  letter-spacing: 1px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  text-align: center;
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
  
  .curved-badge {
    right: 1rem;
    top: 1rem;
  }
  
  .curved-title {
    font-size: var(--heading-size, 1.3rem);
  }
  
  .curved-price {
    font-size: var(--price-size, 1.4rem);
  }
}
</style>
