<template>
  <div class="vertical-card neumorphism-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <!-- Section 1: Badge/Category Block -->
    <div class="neuro-header-section">
      <div v-if="showCategory" class="neuro-category">{{ card.category }}</div>
      <div v-if="showIdBadge" class="neuro-badge">{{ card.id }}</div>
    </div>

    <!-- Section 2: Image Block -->
    <div class="neuro-image-section">
      <div class="image-neuro-inset">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      </div>
    </div>

    <!-- Section 3: Title Block -->
    <div class="neuro-title-section">
      <h3 class="neuro-title">{{ card.title }}</h3>
    </div>

    <!-- Section 4: Description Block -->
    <div v-if="showDescription" class="neuro-description-section">
      <p class="neuro-description">{{ card.description }}</p>
    </div>

    <!-- Section 5: Price Block -->
    <div v-if="showPrice" class="neuro-price-section">
      <div class="neuro-price-emboss">
        <span class="neuro-price">{{ card.price }}</span>
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
  cardBackgroundColor: { type: String, default: '#e0e5ec' },
  cardTitleColor: { type: String, default: '#555555' },
  cardDescriptionColor: { type: String, default: '#666666' },
  cardPriceColor: { type: String, default: '#555555' },
  cardCategoryBgColor: { type: String, default: '#666666' },
  cardBadgeColor: { type: String, default: '#555555' }
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
  box-shadow: 12px 12px 24px rgba(163, 177, 198, 0.6), -12px -12px 24px rgba(255, 255, 255, 0.5);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.vertical-card:hover {
  transform: translateY(-5px);
  box-shadow: 15px 15px 30px rgba(163, 177, 198, 0.7), -15px -15px 30px rgba(255, 255, 255, 0.6);
}

/* Section 1: Header */
.neuro-header-section {
  background: v-bind(cardBackgroundColor);
  padding: var(--content-padding, 16px);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.neuro-category {
  background: v-bind(cardBackgroundColor);
  padding: 0.5rem 1rem;
  border-radius: 15px;
  box-shadow: 4px 4px 8px rgba(163, 177, 198, 0.5), -4px -4px 8px rgba(255, 255, 255, 0.6);
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  color: v-bind(cardCategoryBgColor);
  text-transform: uppercase;
  letter-spacing: 1px;
}

.neuro-badge {
  width: 45px;
  height: 45px;
  background: v-bind(cardBackgroundColor);
  border-radius: 50%;
  box-shadow: inset 4px 4px 8px rgba(163, 177, 198, 0.5), inset -4px -4px 8px rgba(255, 255, 255, 0.6);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--badge-size, 0.85rem);
  font-weight: 800;
  color: v-bind(cardBadgeColor);
}

/* Section 2: Image */
.neuro-image-section {
  background: v-bind(cardBackgroundColor);
  padding: 0 var(--content-padding, 16px) var(--content-padding, 16px);
}

.image-neuro-inset {
  width: 100%;
  height: 240px;
  background: v-bind(cardBackgroundColor);
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  overflow: hidden;
  box-shadow: inset 6px 6px 12px rgba(163, 177, 198, 0.4), inset -6px -6px 12px rgba(255, 255, 255, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  border-radius: calc(var(--card-radius, 16px) * 0.3);
  transition: clip-path 0.3s ease, transform 0.3s ease;
  will-change: transform;
}

.vertical-card:hover .card-image {
  transform: scale(1.03);
}

.image-shape-rounded { border-radius: calc(var(--card-radius, 16px) * 0.3); }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(45% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }

/* Section 3: Title */
.neuro-title-section {
  background: v-bind(cardBackgroundColor);
  padding: var(--content-padding, 16px);
}

.neuro-title {
  margin: 0;
  padding: 1rem;
  background: v-bind(cardBackgroundColor);
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  box-shadow: 4px 4px 8px rgba(163, 177, 198, 0.5), -4px -4px 8px rgba(255, 255, 255, 0.6);
  text-align: center;
  font-size: var(--heading-size, 1.15rem);
  font-weight: 700;
  color: v-bind(cardTitleColor);
  line-height: 1.3;
}

/* Section 4: Description */
.neuro-description-section {
  flex: 1;
  background: v-bind(cardBackgroundColor);
  padding: 0 var(--content-padding, 16px) var(--content-padding, 16px);
  text-align: center;
}

.neuro-description {
  margin: 0;
  padding: 0.75rem;
  background: v-bind(cardBackgroundColor);
  border-radius: calc(var(--card-radius, 16px) * 0.4);
  box-shadow: inset 3px 3px 6px rgba(163, 177, 198, 0.4), inset -3px -3px 6px rgba(255, 255, 255, 0.5);
  font-size: var(--text-size, 0.8rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Section 5: Price */
.neuro-price-section {
  background: v-bind(cardBackgroundColor);
  padding: var(--content-padding, 16px);
  display: flex;
  justify-content: center;
}

.neuro-price-emboss {
  background: v-bind(cardBackgroundColor);
  padding: 0.75rem 2rem;
  border-radius: 25px;
  box-shadow: 6px 6px 12px rgba(163, 177, 198, 0.6), -6px -6px 12px rgba(255, 255, 255, 0.6);
}

.neuro-price {
  font-size: var(--price-size, 1.2rem);
  font-weight: 800;
  color: v-bind(cardPriceColor);
}
</style>
