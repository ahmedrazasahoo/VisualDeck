<template>
  <div class="vertical-card staggered-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="stagger-container">
      <div class="stagger-block image-stagger">
        <div class="stagger-inner">
          <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
        </div>
        <div v-if="showIdBadge" class="stagger-badge">{{ card.id }}</div>
      </div>

      <div class="stagger-block title-stagger">
        <div class="stagger-inner">
          <h3 class="stagger-title">{{ card.title }}</h3>
        </div>
      </div>

      <div v-if="showCategory" class="stagger-block category-stagger">
        <div class="stagger-inner">
          <span class="stagger-category">{{ card.category }}</span>
        </div>
      </div>

      <div v-if="showDescription" class="stagger-block description-stagger">
        <div class="stagger-inner">
          <p class="stagger-description">{{ card.description }}</p>
        </div>
      </div>

      <div v-if="showPrice" class="stagger-block price-stagger">
        <div class="stagger-inner">
          <span class="stagger-price">{{ card.price }}</span>
        </div>
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
  cardBackgroundColor: { type: String, default: '#f5f5f5' },
  cardTitleColor: { type: String, default: '#ffffff' },
  cardDescriptionColor: { type: String, default: '#333333' },
  cardPriceColor: { type: String, default: '#ffffff' },
  cardCategoryColor: { type: String, default: '#333333' }
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
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.12);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.vertical-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 45px rgba(0, 0, 0, 0.2);
}

.stagger-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  padding: 0.5rem;
}

.stagger-block {
  width: 100%;
  position: relative;
  transition: transform 0.3s ease;
}

.stagger-inner {
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s ease;
}

.vertical-card:hover .stagger-inner {
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.image-stagger {
  height: 180px;
  transform: translateX(10px);
}

.image-stagger .stagger-inner {
  height: 100%;
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  border-radius: 12px;
  padding: var(--image-padding, 0px);
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: clip-path 0.3s ease, transform 0.3s ease;
  opacity: 0.9;
  border-radius: 12px;
}

.vertical-card:hover .card-image {
  transform: scale(1.05);
  opacity: 1;
}

.stagger-badge {
  position: absolute;
  top: 0.75rem;
  right: 0.75rem;
  background: rgba(255, 255, 255, 0.95);
  color: #333;
  padding: 0.5rem 0.9rem;
  border-radius: 25px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 800;
  letter-spacing: 1px;
  box-shadow: 0 3px 10px rgba(0, 0, 0, 0.2);
}

.title-stagger {
  transform: translateX(-15px);
}

.title-stagger .stagger-inner {
  background: var(--secondary-color-rgba);
  padding: 1rem var(--content-padding, 16px);
  border-radius: 12px;
}

.stagger-title {
  margin: 0;
  font-size: var(--heading-size, 1.25rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
  text-align: center;
}

.category-stagger {
  transform: translateX(20px);
}

.category-stagger .stagger-inner {
  background: white;
  padding: 0.75rem var(--content-padding, 16px);
  border-radius: 12px;
  text-align: center;
}

.stagger-category {
  display: inline-block;
  background: var(--primary-color-rgba);
  color: white;
  padding: 0.5rem 1.3rem;
  border-radius: 25px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1.5px;
}

.description-stagger {
  flex: 1;
  transform: translateX(-10px);
}

.description-stagger .stagger-inner {
  height: 100%;
  background: white;
  padding: 1.25rem var(--content-padding, 16px);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.stagger-description {
  margin: 0;
  font-size: var(--text-size, 0.85rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  text-align: center;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.price-stagger {
  transform: translateX(15px);
}

.price-stagger .stagger-inner {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 1.25rem var(--content-padding, 16px);
  border-radius: 12px;
  text-align: center;
}

.stagger-price {
  font-size: var(--price-size, 1.5rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
  letter-spacing: 1px;
  text-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

.vertical-card:hover .image-stagger {
  transform: translateX(15px);
}

.vertical-card:hover .title-stagger {
  transform: translateX(-20px);
}

.vertical-card:hover .category-stagger {
  transform: translateX(25px);
}

.vertical-card:hover .description-stagger {
  transform: translateX(-15px);
}

.vertical-card:hover .price-stagger {
  transform: translateX(20px);
}

.image-shape-rounded { border-radius: 12px; }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(40% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }
</style>
