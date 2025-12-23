<template>
  <div class="vertical-card curved-block-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="curved-block image-curve">
      <div class="curved-background">
        <svg class="curve-shape" viewBox="0 0 300 200" preserveAspectRatio="none">
          <path d="M0,0 L300,0 L300,160 Q150,200 0,160 Z" />
        </svg>
      </div>
      <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      <div v-if="showIdBadge" class="curved-badge">#{{ card.id }}</div>
    </div>

    <div class="curved-block title-curve">
      <div class="curved-background">
        <svg class="curve-shape" viewBox="0 0 300 80" preserveAspectRatio="none">
          <path d="M0,40 Q150,0 300,40 L300,80 L0,80 Z" />
        </svg>
      </div>
      <h3 class="curved-title">{{ card.title }}</h3>
    </div>

    <div v-if="showCategory" class="curved-block category-curve">
      <span class="curved-category">{{ card.category }}</span>
    </div>

    <div v-if="showDescription" class="curved-block description-curve">
      <p class="curved-description">{{ card.description }}</p>
    </div>

    <div v-if="showPrice" class="curved-block price-curve">
      <div class="curved-background">
        <svg class="curve-shape" viewBox="0 0 300 70" preserveAspectRatio="none">
          <path d="M0,0 Q150,40 300,0 L300,70 L0,70 Z" />
        </svg>
      </div>
      <span class="curved-price">{{ card.price }}</span>
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
.vertical-card {
  width: var(--card-width, 300px);
  height: var(--card-height, 520px);
  background: v-bind(cardBackgroundColor);
  border-radius: var(--card-radius, 16px);
  overflow: hidden;
  box-shadow: 0 10px 35px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.vertical-card:hover {
  transform: translateY(-12px) rotate(1deg);
  box-shadow: 0 18px 50px rgba(0, 0, 0, 0.25);
}

.curved-block {
  width: 100%;
  position: relative;
}

.curved-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.curve-shape {
  width: 100%;
  height: 100%;
  fill: currentColor;
}

.image-curve {
  height: 200px;
  position: relative;
  overflow: visible;
  color: var(--primary-color-rgba);
  margin-bottom: -20px;
}

.image-curve .curved-background {
  z-index: 0;
}

.card-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: clip-path 0.3s ease, transform 0.3s ease;
  z-index: 1;
  padding: var(--image-padding, 0px);
}

.vertical-card:hover .card-image {
  transform: scale(1.1);
}

.curved-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(255, 255, 255, 0.95);
  color: #333;
  padding: 0.6rem 1.2rem;
  border-radius: 30px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 800;
  letter-spacing: 1px;
  z-index: 2;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.title-curve {
  position: relative;
  color: var(--secondary-color-rgba);
  padding: 2rem var(--content-padding, 16px) 1rem;
  text-align: center;
  margin-bottom: -10px;
}

.title-curve .curved-background {
  z-index: 0;
}

.curved-title {
  position: relative;
  z-index: 1;
  margin: 0;
  font-size: var(--heading-size, 1.3rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
}

.category-curve {
  padding: 1rem var(--content-padding, 16px);
  text-align: center;
  background: #f8f9fa;
}

.curved-category {
  display: inline-block;
  background: v-bind(cardCategoryBgColor);
  color: white;
  padding: 0.6rem 1.5rem;
  border-radius: 30px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.description-curve {
  flex: 1;
  padding: 1.5rem var(--content-padding, 16px);
  background: #f8f9fa;
  display: flex;
  align-items: center;
  justify-content: center;
}

.curved-description {
  margin: 0;
  font-size: var(--text-size, 0.9rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.7;
  text-align: center;
  display: -webkit-box;
  -webkit-line-clamp: 4;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.price-curve {
  position: relative;
  color: var(--primary-color-rgba);
  padding: 2rem var(--content-padding, 16px) 1.5rem;
  text-align: center;
  margin-top: -15px;
}

.price-curve .curved-background {
  z-index: 0;
}

.curved-price {
  position: relative;
  z-index: 1;
  font-size: var(--price-size, 1.6rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
  letter-spacing: 1px;
  text-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.image-shape-rounded { border-radius: 0; }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(40% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }
</style>
