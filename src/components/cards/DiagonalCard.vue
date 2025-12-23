<template>
  <div class="vertical-card diagonal-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="diagonal-container">
      <div class="diagonal-image-section">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
        <div v-if="showIdBadge" class="diagonal-number">#{{ card.id }}</div>
      </div>
      <div class="diagonal-divider"></div>
      <div class="diagonal-info">
        <h3 class="diagonal-title">{{ card.title }}</h3>
        <div v-if="showCategory" class="diagonal-tag">{{ card.category }}</div>
        <div v-if="showDescription" class="diagonal-text">
          <p>{{ card.description }}</p>
        </div>
        <div v-if="showPrice" class="diagonal-price-area">
          <span>{{ card.price }}</span>
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
  background: v-bind(cardBackgroundColor);
  border-radius: var(--card-radius, 16px);
  overflow: hidden;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.12);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.vertical-card:hover {
  transform: translateY(-8px) rotate(-1deg);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.18);
}

.diagonal-container {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  position: relative;
}

.diagonal-image-section {
  height: 250px;
  position: relative;
  overflow: hidden;
  padding: var(--image-padding, 0px);
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f0f0f0;
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
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

.diagonal-number {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 0.5rem 0.8rem;
  border-radius: 20px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 700;
}

.diagonal-divider {
  height: 8px;
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  margin-top: -40px;
  position: relative;
  z-index: 1;
}

.diagonal-info {
  flex: 1;
  padding: 1.5rem var(--content-padding, 16px) var(--content-padding, 16px);
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.diagonal-title {
  margin: 0;
  font-size: var(--heading-size, 1.3rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
}

.diagonal-tag {
  display: inline-block;
  align-self: flex-start;
  background: v-bind(cardCategoryBgColor);
  color: white;
  padding: 0.4rem 1rem;
  border-radius: 20px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.diagonal-text {
  flex: 1;
}

.diagonal-text p {
  margin: 0;
  font-size: var(--text-size, 0.85rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.diagonal-price-area {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 1rem;
  margin: 0 calc(var(--content-padding, 16px) * -1) calc(var(--content-padding, 16px) * -1) calc(var(--content-padding, 16px) * -1);
  text-align: center;
  clip-path: polygon(0 20%, 100% 0, 100% 100%, 0 100%);
  padding-top: 1.5rem;
}

.diagonal-price-area span {
  font-size: var(--price-size, 1.4rem);
  font-weight: 800;
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
