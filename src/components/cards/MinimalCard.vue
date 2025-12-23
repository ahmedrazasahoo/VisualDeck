<template>
  <div class="vertical-card minimal-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="card-content-minimal">
      <div v-if="showIdBadge" class="card-id-minimal">{{ String(card.id).padStart(2, '0') }}</div>
      <div class="card-image-container">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      </div>
      <div class="card-info-section">
        <div class="card-title-row">
          <h3 class="card-title">{{ card.title }}</h3>
          <span v-if="showPrice" class="card-price-minimal">{{ card.price }}</span>
        </div>
        <div v-if="showCategory" class="card-category-row">
          <span class="category-line"></span>
          <span class="card-category-text">{{ card.category }}</span>
          <span class="category-line"></span>
        </div>
        <div v-if="showDescription" class="card-description-section">
          <p class="card-description">{{ card.description }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  card: {
    type: Object,
    required: true
  },
  primaryColor: {
    type: String,
    default: '#667eea'
  },
  secondaryColor: {
    type: String,
    default: '#764ba2'
  },
  primaryColorOpacity: {
    type: Number,
    default: 1
  },
  secondaryColorOpacity: {
    type: Number,
    default: 1
  },
  imageShape: {
    type: String,
    default: 'rounded'
  },
  showIdBadge: {
    type: Boolean,
    default: true
  },
  showCategory: {
    type: Boolean,
    default: true
  },
  showDescription: {
    type: Boolean,
    default: true
  },
  showPrice: {
    type: Boolean,
    default: true
  }
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
  background: white;
  border-radius: var(--card-radius, 16px);
  overflow: hidden;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border: 2px solid #f0f0f0;
}

.vertical-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.08);
}

.card-content-minimal {
  padding: var(--content-padding, 16px);
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.card-id-minimal {
  align-self: flex-start;
  background: #000;
  color: white;
  padding: 0.4rem 0.8rem;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 700;
  letter-spacing: 2px;
  border-radius: 4px;
  margin-bottom: 1rem;
}

.card-image-container {
  width: 85%;
  height: 280px;
  overflow: hidden;
  padding: var(--image-padding, 0px);
  margin-bottom: 1.5rem;
  border-radius: calc(var(--card-radius, 16px) * 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  filter: grayscale(20%);
  transition: clip-path 0.3s ease, border-radius 0.3s ease, transform 0.3s ease;
  will-change: transform;
}

.vertical-card:hover .card-image {
  transform: scale(1.05);
}

/* Image Shape Variants */
.image-shape-rounded { border-radius: calc(var(--card-radius, 16px) * 0.5); }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(45% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }
.image-shape-triangle { clip-path: polygon(50% 0%, 0% 100%, 100% 100%); }
.image-shape-star { clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%); }
.image-shape-heart { clip-path: polygon(50% 20%, 60% 10%, 70% 10%, 80% 20%, 80% 35%, 50% 80%, 20% 35%, 20% 20%, 30% 10%, 40% 10%); }
.image-shape-shield { clip-path: polygon(50% 0%, 100% 20%, 100% 60%, 50% 100%, 0% 60%, 0% 20%); }
.image-shape-parallelogram { clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%); }
.image-shape-trapezoid { clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%); }
.image-shape-ellipse { border-radius: 50%; transform: scaleX(1.4); }
.image-shape-squircle { border-radius: 35%; }
.image-shape-teardrop { clip-path: polygon(50% 0%, 70% 10%, 85% 30%, 90% 50%, 85% 70%, 70% 85%, 50% 100%, 30% 85%, 15% 70%, 10% 50%, 15% 30%, 30% 10%); transform: rotate(45deg); }
.image-shape-arch { clip-path: ellipse(40% 35% at 50% 100%); }
.image-shape-cross { clip-path: polygon(40% 0%, 60% 0%, 60% 40%, 100% 40%, 100% 60%, 60% 60%, 60% 100%, 40% 100%, 40% 60%, 0% 60%, 0% 40%, 40% 40%); }
.image-shape-badge { clip-path: polygon(50% 0%, 65% 5%, 75% 15%, 85% 25%, 95% 40%, 100% 50%, 95% 60%, 85% 75%, 75% 85%, 65% 95%, 50% 100%, 35% 95%, 25% 85%, 15% 75%, 5% 60%, 0% 50%, 5% 40%, 15% 25%, 25% 15%, 35% 5%); }
.image-shape-ticket { clip-path: polygon(10% 10%, 90% 10%, 90% 40%, 85% 45%, 85% 55%, 90% 60%, 90% 90%, 10% 90%, 10% 60%, 15% 55%, 15% 45%, 10% 40%); }
.image-shape-chevron { clip-path: polygon(0% 0%, 75% 0%, 100% 50%, 75% 100%, 0% 100%, 25% 50%); }
.image-shape-arrow { clip-path: polygon(0% 30%, 70% 30%, 70% 0%, 100% 50%, 70% 100%, 70% 70%, 0% 70%); }
.image-shape-clover { clip-path: polygon(50% 20%, 60% 10%, 65% 5%, 70% 10%, 75% 20%, 85% 20%, 90% 25%, 95% 30%, 90% 40%, 80% 50%, 90% 60%, 95% 70%, 90% 75%, 85% 80%, 75% 80%, 70% 90%, 65% 95%, 60% 90%, 50% 80%, 40% 90%, 35% 95%, 30% 90%, 25% 80%, 15% 80%, 10% 75%, 5% 70%, 10% 60%, 20% 50%, 10% 40%, 5% 30%, 10% 25%, 15% 20%, 25% 20%, 30% 10%, 35% 5%, 40% 10%); }

.card-info-section {
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.card-title-row {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 0.5rem;
}

.card-title {
  margin: 0;
  font-size: var(--heading-size, 1.1rem);
  font-weight: 600;
  color: #222;
  line-height: 1.3;
  flex: 1;
}

.card-price-minimal {
  font-size: var(--price-size, 0.95rem);
  font-weight: 700;
  color: #000;
  white-space: nowrap;
}

.card-category-row {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.category-line {
  flex: 1;
  height: 1px;
  background: #e0e0e0;
}

.card-category-text {
  font-size: var(--badge-size, 0.7rem);
  color: #999;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 500;
}

.card-description-section {
  flex: 1;
}

.card-description {
  margin: 0;
  font-size: var(--text-size, 0.8rem);
  color: #666;
  line-height: 1.6;
  text-align: center;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>
