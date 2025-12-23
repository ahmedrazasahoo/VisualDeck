<template>
  <div class="vertical-card zigzag-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="zigzag-section zigzag-top">
      <div v-if="showIdBadge" class="zigzag-badge">{{ card.id }}</div>
      <h3 class="zigzag-title">{{ card.title }}</h3>
    </div>
    <div class="zigzag-section zigzag-image">
      <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
    </div>
    <div class="zigzag-section zigzag-middle">
      <div v-if="showCategory" class="zigzag-category">{{ card.category }}</div>
    </div>
    <div class="zigzag-section zigzag-description">
      <div v-if="showDescription">
        <p>{{ card.description }}</p>
      </div>
    </div>
    <div class="zigzag-section zigzag-bottom">
      <div v-if="showPrice" class="zigzag-price">{{ card.price }}</div>
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
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  display: flex;
  flex-direction: column;
}

.vertical-card:hover {
  transform: translateY(-6px);
}

.zigzag-section {
  position: relative;
}

.zigzag-top {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 1.5rem var(--content-padding, 16px);
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
  padding-bottom: 2rem;
}

.zigzag-badge {
  background: rgba(255, 255, 255, 0.3);
  color: white;
  display: inline-block;
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.zigzag-title {
  margin: 0;
  font-size: var(--heading-size, 1.3rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
}

.zigzag-image {
  height: 200px;
  overflow: hidden;
  padding: var(--image-padding, 0px);
  background: #f5f5f5;
  margin-top: -15px;
  clip-path: polygon(0 5%, 100% 0, 100% 95%, 0 100%);
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: clip-path 0.3s ease, transform 0.3s ease;
}

.vertical-card:hover .card-image {
  transform: scale(1.08);
}

.zigzag-middle {
  background: v-bind(cardCategoryBgColor);
  padding: 0.75rem var(--content-padding, 16px);
  margin-top: -10px;
  clip-path: polygon(0 0, 100% 10%, 100% 100%, 0 90%);
  padding-top: 1.25rem;
  padding-bottom: 1.25rem;
  text-align: center;
}

.zigzag-category {
  font-size: var(--badge-size, 0.75rem);
  color: white;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.zigzag-description {
  flex: 1;
  padding: 1rem var(--content-padding, 16px);
  margin-top: -5px;
}

.zigzag-description p {
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

.zigzag-bottom {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 1rem var(--content-padding, 16px);
  clip-path: polygon(0 15%, 100% 0, 100% 100%, 0 100%);
  padding-top: 1.5rem;
  text-align: center;
}

.zigzag-price {
  font-size: var(--price-size, 1.4rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
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
