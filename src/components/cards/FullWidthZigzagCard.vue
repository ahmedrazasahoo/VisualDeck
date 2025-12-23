<template>
  <div class="fullwidth-card zigzag-fullwidth-card" :style="{
    '--primary-color-rgba': primaryColorRgba,
    '--secondary-color-rgba': secondaryColorRgba
  }">
    <div class="fullwidth-background zigzag-top-bg">
      <div class="content-wrapper">
        <div v-if="showIdBadge" class="zigzag-badge">{{ card.id }}</div>
        <h3 class="zigzag-title">{{ card.title }}</h3>
      </div>
    </div>
    
    <div class="fullwidth-background zigzag-image-bg">
      <div class="content-wrapper">
        <img :src="card.image" :alt="card.title" :class="['card-image', `image-shape-${imageShape}`]" />
      </div>
    </div>
    
    <div class="fullwidth-background zigzag-middle-bg">
      <div class="content-wrapper">
        <div v-if="showCategory" class="zigzag-category">{{ card.category }}</div>
      </div>
    </div>
    
    <div class="fullwidth-background zigzag-description-bg">
      <div class="content-wrapper">
        <div v-if="showDescription">
          <p class="zigzag-description">{{ card.description }}</p>
        </div>
      </div>
    </div>
    
    <div class="fullwidth-background zigzag-bottom-bg">
      <div class="content-wrapper">
        <div v-if="showPrice" class="zigzag-price">{{ card.price }}</div>
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
.fullwidth-card {
  width: 100%;
  min-height: var(--card-height, 520px);
  background: v-bind(cardBackgroundColor);
  border-radius: var(--card-radius, 16px);
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.fullwidth-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.fullwidth-background {
  width: 100%;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.content-wrapper {
  width: 100%;
  max-width: var(--content-max-width, 800px);
  margin: 0 auto;
  padding: 0 var(--content-padding, 16px);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.zigzag-top-bg {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 1.5rem 0;
  clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
  padding-bottom: 2rem;
}

.zigzag-badge {
  background: rgba(255, 255, 255, 0.3);
  color: white;
  display: inline-block;
  padding: 0.4rem 1rem;
  border-radius: 20px;
  font-size: var(--badge-size, 0.75rem);
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.zigzag-title {
  margin: 0;
  font-size: var(--heading-size, 1.5rem);
  font-weight: 800;
  color: v-bind(cardTitleColor);
  line-height: 1.2;
  text-align: center;
}

.zigzag-image-bg {
  min-height: 250px;
  background: #f5f5f5;
  margin-top: -15px;
  clip-path: polygon(0 5%, 100% 0, 100% 95%, 0 100%);
  padding: 2rem 0;
}

.zigzag-image-bg .content-wrapper {
  height: 100%;
}

.card-image {
  width: 100%;
  max-width: 600px;
  height: 250px;
  object-fit: cover;
  object-position: center;
  transition: transform 0.3s ease;
  border-radius: 8px;
  padding: var(--image-padding, 0px);
}

.fullwidth-card:hover .card-image {
  transform: scale(1.05);
}

.zigzag-middle-bg {
  background: v-bind(cardCategoryBgColor);
  padding: 0.75rem 0;
  margin-top: -10px;
  clip-path: polygon(0 0, 100% 10%, 100% 100%, 0 90%);
  padding-top: 1.25rem;
  padding-bottom: 1.25rem;
}

.zigzag-category {
  font-size: var(--badge-size, 0.8rem);
  color: white;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-align: center;
}

.zigzag-description-bg {
  flex: 1;
  padding: 2rem 0;
  margin-top: -5px;
  background: v-bind(cardBackgroundColor);
  min-height: 120px;
}

.zigzag-description {
  margin: 0;
  font-size: var(--text-size, 0.95rem);
  color: v-bind(cardDescriptionColor);
  line-height: 1.7;
  text-align: center;
  max-width: 700px;
}

.zigzag-bottom-bg {
  background: linear-gradient(135deg, var(--primary-color-rgba) 0%, var(--secondary-color-rgba) 100%);
  padding: 1.5rem 0;
  clip-path: polygon(0 15%, 100% 0, 100% 100%, 0 100%);
  padding-top: 2rem;
}

.zigzag-price {
  font-size: var(--price-size, 1.6rem);
  font-weight: 900;
  color: v-bind(cardPriceColor);
  text-align: center;
}

.image-shape-rounded { border-radius: 8px; }
.image-shape-square { border-radius: 0; clip-path: none; }
.image-shape-circle { clip-path: circle(40% at 50% 50%); }
.image-shape-hexagon { clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%); }
.image-shape-diamond { clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%); }
.image-shape-pentagon { clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%); }
.image-shape-octagon { clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%); }
.image-shape-blob { clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%); }

@media (max-width: 768px) {
  .content-wrapper {
    max-width: 100%;
  }
  
  .card-image {
    max-width: 100%;
    height: 200px;
  }
  
  .zigzag-title {
    font-size: var(--heading-size, 1.3rem);
  }
  
  .zigzag-price {
    font-size: var(--price-size, 1.4rem);
  }
}
</style>
