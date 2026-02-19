<template>
  <div class="vertical-card stacked-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="stacked-layers">
      <div class="stack-layer layer-3"></div>
      <div class="stack-layer layer-2"></div>
      <div class="stack-layer layer-1">
        <div class="stacked-image-section">
          <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
          <div v-if="showIdBadge" class="stacked-badge">{{ card.id }}</div>
        </div>
        <div class="stacked-content">
          <div class="stacked-header">
            <h3 class="stacked-title">{{ card.title }}</h3>
            <div v-if="showCategory" class="stacked-category">{{ card.category }}</div>
          </div>
          <div v-if="showDescription" class="stacked-body">
            <p>{{ card.description }}</p>
          </div>
          <div v-if="showPrice" class="stacked-price-tag">
            <span>{{ card.price }}</span>
          </div>
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
  },
  cardBackgroundColor: {
    type: String,
    default: '#ffffff'
  },
  cardTitleColor: {
    type: String,
    default: '#222222'
  },
  cardDescriptionColor: {
    type: String,
    default: '#666666'
  },
  cardPriceColor: {
    type: String,
    default: '#ffffff'
  },
  cardCategoryBgColor: {
    type: String,
    default: '#667eea'
  },
  cardBadgeBgColor: {
    type: String,
    default: '#667eea'
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
  background: transparent;
  border-radius: var(--card-radius, 16px);
  position: relative;
  padding: 1rem;
}

.stacked-layers {
  position: relative;
  width: 100%;
  height: 100%;
}

.stack-layer {
  position: absolute;
  width: 100%;
  height: 100%;
  background: v-bind(cardBackgroundColor);
  border-radius: var(--card-radius, 16px);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.layer-3 {
  transform: translateY(8px) scale(0.94);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  opacity: 0.6;
}

.layer-2 {
  transform: translateY(4px) scale(0.97);
  box-shadow: 0 3px 12px rgba(0, 0, 0, 0.12);
  opacity: 0.8;
}

.layer-1 {
  transform: translateY(0) scale(1);
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.vertical-card:hover .layer-3 {
  transform: translateY(12px) scale(0.92);
}

.vertical-card:hover .layer-2 {
  transform: translateY(6px) scale(0.96);
}

.vertical-card:hover .layer-1 {
  transform: translateY(-8px) scale(1);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.2);
}

.stacked-image-section {
  height: 280px;
  position: relative;
  overflow: hidden;
  padding: var(--image-padding, 0px);
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f5f5f5;
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

.stacked-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: v-bind(cardBadgeBgColor);
  color: white;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: var(--badge-size, 0.8rem);
  font-weight: 700;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.image-shape-rounded {
  border-radius: 0;
}

.image-shape-square {
  border-radius: 0;
  clip-path: none;
}

.image-shape-circle {
  clip-path: circle(40% at 50% 50%);
}

.image-shape-hexagon {
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
}

.image-shape-diamond {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
}

.image-shape-pentagon {
  clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%);
}

.image-shape-octagon {
  clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%);
}

.image-shape-blob {
  clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%);
}

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

.stacked-content {
  flex: 1;
  padding: var(--content-padding, 16px);
  display: flex;
  flex-direction: column;
}

.stacked-header {
  margin-bottom: 1rem;
}

.stacked-title {
  margin: 0 0 0.5rem 0;
  font-size: var(--heading-size, 1.2rem);
  font-weight: 700;
  color: v-bind(cardTitleColor);
  line-height: 1.3;
}

.stacked-category {
  display: inline-block;
  background: v-bind(cardCategoryBgColor);
  color: white;
  padding: 0.3rem 0.8rem;
  border-radius: 12px;
  font-size: var(--badge-size, 0.7rem);
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.stacked-body {
  flex: 1;
  margin-bottom: 1rem;
}

.stacked-body p {
  margin: 0;
  font-size: var(--text-size, 0.85rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.6;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.stacked-price-tag {
  background: linear-gradient(135deg, var(--primary-color-rgba, rgba(102, 126, 234, 1)) 0%, var(--secondary-color-rgba, rgba(118, 75, 162, 1)) 100%);
  padding: 0.75rem;
  margin: 0 calc(var(--content-padding, 16px) * -1) calc(var(--content-padding, 16px) * -1) calc(var(--content-padding, 16px) * -1);
  text-align: center;
  border-radius: 0 0 var(--card-radius, 16px) var(--card-radius, 16px);
}

.stacked-price-tag span {
  font-size: var(--price-size, 1.2rem);
  font-weight: 800;
  color: v-bind(cardPriceColor);
}
</style>
