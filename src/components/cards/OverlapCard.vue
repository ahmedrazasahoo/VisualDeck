<template>
  <div class="vertical-card overlap-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="overlap-image-wrapper">
      <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      <div v-if="showIdBadge" class="overlap-id">{{ String(card.id).padStart(2, '0') }}</div>
    </div>
    <div class="overlap-content-box">
      <h3 class="overlap-heading">{{ card.title }}</h3>
      <div v-if="showCategory" class="overlap-category-pill">{{ card.category }}</div>
      <div v-if="showDescription" class="overlap-description">
        <p>{{ card.description }}</p>
      </div>
      <div v-if="showPrice" class="overlap-price-badge">
        <span>{{ card.price }}</span>
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
  cardDescriptionColor: { type: String, default: '#666666' },
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
  background: transparent;
  border-radius: var(--card-radius, 16px);
  padding: 1rem;
  position: relative;
  display: flex;
  flex-direction: column;
}

.overlap-image-wrapper {
  height: 320px;
  border-radius: var(--card-radius, 16px);
  overflow: hidden;
  padding: var(--image-padding, 0px);
  background: #f5f5f5;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: transform 0.3s ease;
}

.vertical-card:hover .overlap-image-wrapper {
  transform: translateY(-8px);
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  transition: clip-path 0.3s ease, transform 0.3s ease;
}

.vertical-card:hover .card-image {
  transform: scale(1.05);
}

.overlap-id {
  position: absolute;
  top: 1rem;
  left: 1rem;
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  color: white;
  padding: 0.6rem 1rem;
  border-radius: 8px;
  font-size: var(--badge-size, 0.8rem);
  font-weight: 800;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.overlap-content-box {
  background: v-bind(cardBackgroundColor);
  border-radius: var(--card-radius, 16px);
  padding: 1.5rem var(--content-padding, 16px) var(--content-padding, 16px);
  margin-top: -50px;
  position: relative;
  z-index: 1;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  transition: transform 0.3s ease;
}

.vertical-card:hover .overlap-content-box {
  transform: translateY(-4px);
}

.overlap-heading {
  margin: 0;
  font-size: var(--heading-size, 1.2rem);
  font-weight: 700;
  color: v-bind(cardTitleColor);
  line-height: 1.3;
}

.overlap-category-pill {
  display: inline-block;
  align-self: flex-start;
  background: v-bind(cardCategoryBgColor);
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 15px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.overlap-description {
  flex: 1;
}

.overlap-description p {
  margin: 0;
  font-size: var(--text-size, 0.85rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.overlap-price-badge {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 0.75rem;
  border-radius: 10px;
  text-align: center;
}

.overlap-price-badge span {
  font-size: var(--price-size, 1.2rem);
  font-weight: 800;
  color: v-bind(cardPriceColor);
}

.image-shape-rounded { border-radius: var(--card-radius, 16px); }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(40% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }
</style>
