<template>
  <div class="vertical-card striped-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="stripe-block image-block">
      <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      <div v-if="showIdBadge" class="stripe-badge">#{{ card.id }}</div>
    </div>
    
    <div class="stripe-block title-block">
      <h3 class="stripe-title">{{ card.title }}</h3>
    </div>
    
    <div v-if="showCategory" class="stripe-block category-block">
      <span class="category-label">{{ card.category }}</span>
    </div>
    
    <div v-if="showDescription" class="stripe-block description-block">
      <p class="stripe-description">{{ card.description }}</p>
    </div>
    
    <div v-if="showPrice" class="stripe-block price-block">
      <span class="price-value">{{ card.price }}</span>
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
  cardDescriptionColor: { type: String, default: '#333333' },
  cardPriceColor: { type: String, default: '#ffffff' },
  cardCategoryColor: { type: String, default: '#ffffff' }
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
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.vertical-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
}

.stripe-block {
  width: 100%;
  transition: transform 0.3s ease;
}

.vertical-card:hover .stripe-block {
  transform: translateX(0);
}

.image-block {
  height: 200px;
  position: relative;
  overflow: hidden;
  padding: var(--image-padding, 0px);
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  transform: translateX(-5px);
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: clip-path 0.3s ease, transform 0.3s ease;
  opacity: 0.9;
}

.vertical-card:hover .card-image {
  transform: scale(1.1);
  opacity: 1;
}

.stripe-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(255, 255, 255, 0.95);
  color: #333;
  padding: 0.5rem 1rem;
  border-radius: 25px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 800;
  letter-spacing: 1px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.title-block {
  padding: 1.25rem var(--content-padding, 16px);
  background: var(--secondary-color-rgba);
  transform: translateX(5px);
}

.stripe-title {
  margin: 0;
  font-size: var(--heading-size, 1.35rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
  text-align: center;
}

.category-block {
  padding: 0.75rem var(--content-padding, 16px);
  background: rgba(0, 0, 0, 0.05);
  text-align: center;
  transform: translateX(-8px);
}

.category-label {
  display: inline-block;
  background: var(--primary-color-rgba);
  color: v-bind(cardCategoryColor);
  padding: 0.5rem 1.5rem;
  border-radius: 25px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.description-block {
  flex: 1;
  padding: 1.5rem var(--content-padding, 16px);
  background: v-bind(cardBackgroundColor);
  display: flex;
  align-items: center;
  justify-content: center;
  transform: translateX(8px);
}

.stripe-description {
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

.price-block {
  padding: 1.5rem var(--content-padding, 16px);
  background: linear-gradient(135deg, var(--secondary-color-rgba) 0%, var(--primary-color-rgba) 100%);
  text-align: center;
  transform: translateX(-10px);
}

.price-value {
  font-size: var(--price-size, 1.6rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
  letter-spacing: 1px;
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
