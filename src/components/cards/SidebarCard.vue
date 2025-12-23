<template>
  <div class="vertical-card sidebar-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="sidebar-accent">
      <div class="sidebar-id-vertical">
        <span v-if="showIdBadge">{{ String(card.id).padStart(2, '0') }}</span>
      </div>
    </div>
    <div class="sidebar-main">
      <div class="sidebar-image-area">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      </div>
      <div class="sidebar-details">
        <div v-if="showCategory" class="sidebar-label">{{ card.category }}</div>
        <h3 class="sidebar-title">{{ card.title }}</h3>
        <div v-if="showDescription" class="sidebar-paragraph">
          <p>{{ card.description }}</p>
        </div>
        <div v-if="showPrice" class="sidebar-price-display">{{ card.price }}</div>
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
  cardPriceColor: { type: String, default: '#667eea' },
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
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
}

.vertical-card:hover {
  transform: translateX(5px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.sidebar-accent {
  width: 50px;
  background: linear-gradient(180deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding: 1rem 0;
}

.sidebar-id-vertical {
  writing-mode: vertical-rl;
  transform: rotate(180deg);
  color: white;
  font-size: var(--badge-size, 0.9rem);
  font-weight: 800;
  letter-spacing: 3px;
}

.sidebar-main {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.sidebar-image-area {
  height: 280px;
  overflow: hidden;
  padding: var(--image-padding, 0px);
  background: #f5f5f5;
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

.sidebar-details {
  flex: 1;
  padding: var(--content-padding, 16px);
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.sidebar-label {
  font-size: var(--badge-size, 0.7rem);
  color: v-bind(cardCategoryBgColor);
  text-transform: uppercase;
  font-weight: 700;
  letter-spacing: 1.5px;
}

.sidebar-title {
  margin: 0;
  font-size: var(--heading-size, 1.2rem);
  font-weight: 700;
  color: v-bind(cardTitleColor);
  line-height: 1.3;
}

.sidebar-paragraph {
  flex: 1;
}

.sidebar-paragraph p {
  margin: 0;
  font-size: var(--text-size, 0.85rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.sidebar-price-display {
  font-size: var(--price-size, 1.3rem);
  font-weight: 800;
  color: v-bind(cardPriceColor);
  padding-top: 0.5rem;
  border-top: 2px solid #f0f0f0;
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
