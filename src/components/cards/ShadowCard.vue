<template>
  <div class="vertical-card shadow-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <!-- Section 1: Badge/Category Block -->
    <div class="shadow-header-section">
      <span v-if="showCategory" class="shadow-category">{{ card.category }}</span>
      <span v-if="showIdBadge" class="shadow-badge">ID: {{ card.id }}</span>
    </div>

    <!-- Section 2: Image Block -->
    <div class="shadow-image-section">
      <div class="image-shadow-wrapper">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      </div>
    </div>

    <!-- Section 3: Title Block -->
    <div class="shadow-title-section">
      <h3 class="shadow-title">{{ card.title }}</h3>
    </div>

    <!-- Section 4: Description Block -->
    <div v-if="showDescription" class="shadow-description-section">
      <p class="shadow-description">{{ card.description }}</p>
    </div>

    <!-- Section 5: Price Block -->
    <div v-if="showPrice" class="shadow-price-section">
      <div class="price-shadow-box">
        <span class="shadow-price">{{ card.price }}</span>
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
  cardTitleColor: { type: String, default: '#222222' },
  cardDescriptionColor: { type: String, default: '#666666' },
  cardPriceColor: { type: String, default: '#ffffff' },
  cardCategoryBgColor: { type: String, default: '#666666' },
  cardBadgeColor: { type: String, default: '#667eea' }
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
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2), 0 20px 60px rgba(0, 0, 0, 0.15), 0 5px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.vertical-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.25), 0 25px 70px rgba(0, 0, 0, 0.2), 0 8px 20px rgba(0, 0, 0, 0.15);
}

/* Section 1: Header */
.shadow-header-section {
  background: white;
  padding: 1rem var(--content-padding, 16px);
  margin: var(--content-padding, 16px) var(--content-padding, 16px) 0;
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.shadow-category {
  font-size: var(--badge-size, 0.7rem);
  color: v-bind(cardCategoryBgColor);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.shadow-badge {
  font-size: var(--badge-size, 0.7rem);
  color: v-bind(cardBadgeColor);
  font-weight: 700;
  letter-spacing: 1px;
}

/* Section 2: Image */
.shadow-image-section {
  padding: var(--content-padding, 16px);
  background: v-bind(cardBackgroundColor);
}

.image-shadow-wrapper {
  width: 100%;
  height: 240px;
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15), 0 4px 10px rgba(0, 0, 0, 0.1), 0 2px 5px rgba(0, 0, 0, 0.08);
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
  will-change: transform;
}

.vertical-card:hover .card-image {
  transform: scale(1.05);
}

.image-shape-rounded { border-radius: calc(var(--card-radius, 16px) * 0.5); }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(45% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }

/* Section 3: Title */
.shadow-title-section {
  background: white;
  padding: 1rem;
  margin: 0 var(--content-padding, 16px);
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1), 0 3px 8px rgba(0, 0, 0, 0.08);
}

.shadow-title {
  margin: 0;
  font-size: var(--heading-size, 1.15rem);
  font-weight: 700;
  color: v-bind(cardTitleColor);
  line-height: 1.3;
}

/* Section 4: Description */
.shadow-description-section {
  flex: 1;
  padding: 1rem;
  margin: var(--content-padding, 16px) var(--content-padding, 16px) 0;
  background: white;
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
}

.shadow-description {
  margin: 0;
  font-size: var(--text-size, 0.8rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Section 5: Price */
.shadow-price-section {
  padding: var(--content-padding, 16px);
  background: v-bind(cardBackgroundColor);
  display: flex;
  justify-content: center;
}

.price-shadow-box {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 0.75rem 2rem;
  border-radius: 25px;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2), 0 3px 8px rgba(0, 0, 0, 0.15);
}

.shadow-price {
  font-size: var(--price-size, 1.15rem);
  font-weight: 800;
  color: v-bind(cardPriceColor);
}
</style>
