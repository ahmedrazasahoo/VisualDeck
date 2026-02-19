<script setup>
import { ref, onMounted, onUnmounted, computed, watch } from 'vue';
import { cardsData } from '../store/api.js';
import ModernCard from './cards/ModernCard.vue';
import ClassicCard from './cards/ClassicCard.vue';
import MinimalCard from './cards/MinimalCard.vue';
import ElegantCard from './cards/ElegantCard.vue';
import BoldCard from './cards/BoldCard.vue';
import CompactCard from './cards/CompactCard.vue';
import LuxuryCard from './cards/LuxuryCard.vue';
import VibrantCard from './cards/VibrantCard.vue';
import ShadowCard from './cards/ShadowCard.vue';
import GradientCard from './cards/GradientCard.vue';
import NeonCard from './cards/NeonCard.vue';
import GlassmorphismCard from './cards/GlassmorphismCard.vue';
import NeumorphismCard from './cards/NeumorphismCard.vue';
import MetroCard from './cards/MetroCard.vue';
import PolaroidCard from './cards/PolaroidCard.vue';
import MagazineCard from './cards/MagazineCard.vue';
import StackedCard from './cards/StackedCard.vue';
import RetroCard from './cards/RetroCard.vue';
import SplitCard from './cards/SplitCard.vue';
import DiagonalCard from './cards/DiagonalCard.vue';
import OverlapCard from './cards/OverlapCard.vue';
import SidebarCard from './cards/SidebarCard.vue';
import FloatingCard from './cards/FloatingCard.vue';
import RibbonCard from './cards/RibbonCard.vue';
import CircularCard from './cards/CircularCard.vue';
import CornerCard from './cards/CornerCard.vue';
import ZigzagCard from './cards/ZigzagCard.vue';
import StripedCard from './cards/StripedCard.vue';
import WaveCard from './cards/WaveCard.vue';
import StaggeredCard from './cards/StaggeredCard.vue';
import CurvedBlockCard from './cards/CurvedBlockCard.vue';
import GeometricBlockCard from './cards/GeometricBlockCard.vue';
import LayeredBlockCard from './cards/LayeredBlockCard.vue';
import FullWidthZigzagCard from './cards/FullWidthZigzagCard.vue';
import FullWidthWaveCard from './cards/FullWidthWaveCard.vue';
import FullWidthCurvedCard from './cards/FullWidthCurvedCard.vue';

const props = defineProps({
  items: {
    type: Array,
    default: null
  },
  cardStyle: {
    type: String,
    default: 'modern'
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
  scrollSpeed: {
    type: Number,
    default: 1
  },
  headingFontSize: {
    type: Number,
    default: 1.15
  },
  textFontSize: {
    type: Number,
    default: 0.85
  },
  priceFontSize: {
    type: Number,
    default: 1
  },
  badgeFontSize: {
    type: Number,
    default: 0.75
  },
  borderRadius: {
    type: Number,
    default: 16
  },
  imageShape: {
    type: String,
    default: 'rounded'
  },
  cardPadding: {
    type: Number,
    default: 16
  },
  imagePadding: {
    type: Number,
    default: 0
  },
  contentPadding: {
    type: Number,
    default: 16
  },
  cardMargin: {
    type: Number,
    default: 0
  },
  cardGap: {
    type: Number,
    default: 24
  },
  cardWidth: {
    type: Number,
    default: 300
  },
  cardHeight: {
    type: Number,
    default: 520
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
  entranceAnimation: {
    type: String,
    default: 'none'
  },
  animationDelay: {
    type: Number,
    default: 600
  },
  cardOpacity: {
    type: Number,
    default: 1
  },
  leftSpacing: {
    type: Number,
    default: 6
  },
  scrollDirection: {
    type: String,
    default: 'left'
  },
  backgroundType: {
    type: String,
    default: 'gradient'
  },
  backgroundValue: {
    type: String,
    default: 'default-gradient-1'
  },
  customBackgroundColor: {
    type: String,
    default: '#667eea'
  },
  customBackgroundImage: {
    type: String,
    default: ''
  },
  customBackgroundVideo: {
    type: String,
    default: ''
  },
  cardBackgroundColor: {
    type: String,
    default: '#1a1a2e'
  },
  cardCategoryBgColor: {
    type: String,
    default: '#667eea'
  },
  cardFooterBgColor: {
    type: String,
    default: '#667eea'
  },
  cardTitleColor: {
    type: String,
    default: '#ffffff'
  },
  cardDescriptionColor: {
    type: String,
    default: '#ffffff'
  },
  cardPriceColor: {
    type: String,
    default: '#ffffff'
  },
  cardBadgeColor: {
    type: String,
    default: '#ffffff'
  },
  cardBadgeBgColor: {
    type: String,
    default: '#667eea'
  },
  cardOverlayColor: {
    type: String,
    default: 'rgba(0, 0, 0, 0.7)'
  },
  cardContentBgColor: {
    type: String,
    default: '#fafafa'
  },
  cardCategoryColor: {
    type: String,
    default: '#ffffff'
  },
  cardDividerBgColor: {
    type: String,
    default: '#667eea'
  },
  cardRibbonBgColor: {
    type: String,
    default: '#667eea'
  },
  cardTopSectionBgColor: {
    type: String,
    default: '#667eea'
  },
  cardBottomSectionBgColor: {
    type: String,
    default: '#667eea'
  },
  cardGlassOverlayBgColor: {
    type: String,
    default: 'rgba(255, 255, 255, 0.3)'
  },
  cardFrameBgColor: {
    type: String,
    default: '#ffffff'
  },
  cardBorderBgColor: {
    type: String,
    default: '#f0f0f0'
  },
  cardStripesBgColor: {
    type: String,
    default: '#667eea'
  },
  cardSidebarBgColor: {
    type: String,
    default: '#667eea'
  },
  cardLayerBgColor: {
    type: String,
    default: '#ffffff'
  }
});

const cardComponents = {
  'fullwidth-zigzag': FullWidthZigzagCard,
  'fullwidth-wave': FullWidthWaveCard,
  'fullwidth-curved': FullWidthCurvedCard,
  'layered-block': LayeredBlockCard,
  'geometric-block': GeometricBlockCard,
  'curved-block': CurvedBlockCard,
  staggered: StaggeredCard,
  wave: WaveCard,
  striped: StripedCard,
  zigzag: ZigzagCard,
  corner: CornerCard,
  circular: CircularCard,
  ribbon: RibbonCard,
  modern: ModernCard,
  classic: ClassicCard,
  minimal: MinimalCard,
  elegant: ElegantCard,
  bold: BoldCard,
  compact: CompactCard,
  luxury: LuxuryCard,
  vibrant: VibrantCard,
  shadow: ShadowCard,
  gradient: GradientCard,
  neon: NeonCard,
  glassmorphism: GlassmorphismCard,
  neumorphism: NeumorphismCard,
  metro: MetroCard,
  polaroid: PolaroidCard,
  magazine: MagazineCard,
  stacked: StackedCard,
  retro: RetroCard,
  split: SplitCard,
  diagonal: DiagonalCard,
  overlap: OverlapCard,
  sidebar: SidebarCard,
  floating: FloatingCard
};

const currentCardComponent = computed(() => cardComponents[props.cardStyle] || ModernCard);

const displayCards = computed(() => props.items && props.items.length ? props.items : cardsData);

const backgroundGradients = {
  'default-gradient-1': 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
  'default-gradient-2': 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
  'default-gradient-3': 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
  'default-gradient-4': 'linear-gradient(135deg, #43e97b 0%, #38f9d7 100%)',
  'default-gradient-5': 'linear-gradient(135deg, #fa709a 0%, #fee140 100%)',
  'default-gradient-6': 'linear-gradient(135deg, #30cfd0 0%, #330867 100%)',
  'default-gradient-7': 'linear-gradient(135deg, #ff9a56 0%, #ff6a88 100%)',
  'default-gradient-8': 'linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%)',
  'default-gradient-9': 'linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%)',
  'default-gradient-10': 'linear-gradient(135deg, #d299c2 0%, #fef9d7 100%)'
};

const backgroundStyle = computed(() => {
  if (props.backgroundType === 'none') {
    return {
      background: 'transparent'
    };
  } else if (props.backgroundType === 'gradient') {
    return {
      background: backgroundGradients[props.backgroundValue] || backgroundGradients['default-gradient-1']
    };
  } else if (props.backgroundType === 'color') {
    return {
      background: props.customBackgroundColor
    };
  } else if (props.backgroundType === 'image' && props.customBackgroundImage) {
    return {
      backgroundImage: `url(${props.customBackgroundImage})`,
      backgroundSize: 'cover',
      backgroundPosition: 'center',
      backgroundRepeat: 'no-repeat'
    };
  } else if (props.backgroundType === 'video') {
    return {
      background: 'transparent'
    };
  }
  return {
    background: backgroundGradients['default-gradient-1']
  };
});

const scrollContainer = ref(null);
const trackInner = ref(null);
const animationFrame = ref(null);
const entranceAnimationComplete = ref(false);
const animatedCardsCount = ref(0);
const cardsToAnimate = ref(0);
let scrollPosition = 0;
let isPaused = false;
let bounceDirection = 1;

const getHalfWidth = () => {
  if (!trackInner.value) return 0;
  return trackInner.value.scrollWidth / 2;
};

const applyTransform = () => {
  if (trackInner.value) {
    trackInner.value.style.transform = `translateX(${-scrollPosition}px)`;
  }
};

const autoScroll = () => {
  if (!isPaused && trackInner.value) {
    const halfWidth = getHalfWidth();
    if (halfWidth > 0) {
      if (props.scrollDirection === 'both') {
        scrollPosition += props.scrollSpeed * bounceDirection;
        if (scrollPosition >= halfWidth) {
          scrollPosition = halfWidth;
          bounceDirection = -1;
        } else if (scrollPosition <= 0) {
          scrollPosition = 0;
          bounceDirection = 1;
        }
      } else if (props.scrollDirection === 'right') {
        scrollPosition -= props.scrollSpeed;
        if (scrollPosition <= 0) {
          scrollPosition += halfWidth;
        }
      } else {
        // default: left
        scrollPosition += props.scrollSpeed;
        if (scrollPosition >= halfWidth) {
          scrollPosition -= halfWidth;
        }
      }
      applyTransform();
    }
  }
  animationFrame.value = requestAnimationFrame(autoScroll);
};

const calculateCardsToFit = () => {
  const screenWidth = window.innerWidth;
  const totalCardWidth = props.cardWidth + props.cardGap + (props.cardMargin * 2);
  const cardsThatFit = Math.floor(screenWidth / totalCardWidth);
  return Math.min(cardsThatFit, displayCards.value.length);
};

const playEntranceAnimation = () => {
  entranceAnimationComplete.value = false;
  animatedCardsCount.value = 0;
  cardsToAnimate.value = calculateCardsToFit();

  // Reset scroll position to show card ID 1 first
  scrollPosition = 0;
  applyTransform();

  const animateNextCard = (cardIndex) => {
    if (cardIndex >= cardsToAnimate.value) {
      setTimeout(() => {
        entranceAnimationComplete.value = true;
        isPaused = false;
      }, props.animationDelay);
      return;
    }

    animatedCardsCount.value = cardIndex + 1;

    setTimeout(() => {
      animateNextCard(cardIndex + 1);
    }, props.animationDelay);
  };

  isPaused = true;
  setTimeout(() => {
    animateNextCard(0);
  }, 300);
};

const handleMouseEnter = () => {
  isPaused = true;
};

const handleMouseLeave = () => {
  if (props.entranceAnimation !== 'none' && !entranceAnimationComplete.value) {
    return;
  }
  isPaused = false;
};

// Watch for changes in entranceAnimation prop
watch(() => props.entranceAnimation, (newVal) => {
  if (newVal !== 'none') {
    playEntranceAnimation();
  } else {
    entranceAnimationComplete.value = true;
    animatedCardsCount.value = 0;
    isPaused = false;
  }
});

// Watch for card style changes and reset animation state
watch(() => props.cardStyle, () => {
  scrollPosition = 0;
  applyTransform();
  entranceAnimationComplete.value = false;
  animatedCardsCount.value = 0;

  setTimeout(() => {
    if (props.entranceAnimation !== 'none') {
      playEntranceAnimation();
    } else {
      entranceAnimationComplete.value = true;
      isPaused = false;
    }
  }, 100);
});

onMounted(() => {
  // Single RAF loop runs forever; isPaused controls movement
  autoScroll();
  if (props.entranceAnimation !== 'none') {
    playEntranceAnimation();
  } else {
    entranceAnimationComplete.value = true;
    isPaused = false;
  }
});

onUnmounted(() => {
  if (animationFrame.value) {
    cancelAnimationFrame(animationFrame.value);
  }
});
</script>

<template>
  <div class="carousel-container" :style="{
    ...backgroundStyle,
    '--heading-size': `${headingFontSize}rem`,
    '--text-size': `${textFontSize}rem`,
    '--price-size': `${priceFontSize}rem`,
    '--badge-size': `${badgeFontSize}rem`,
    '--card-radius': `${borderRadius}px`,
    '--card-padding': `${cardPadding}px`,
    '--image-padding': `${imagePadding}px`,
    '--content-padding': `${contentPadding}px`,
    '--card-margin': `${cardMargin}px`,
    '--card-gap': `${cardGap}px`,
    '--card-width': `${cardWidth}px`,
    '--card-height': `${cardHeight}px`,
    '--primary-color': primaryColor,
    '--secondary-color': secondaryColor,
    '--primary-color-opacity': primaryColorOpacity,
    '--secondary-color-opacity': secondaryColorOpacity,
    '--card-opacity': cardOpacity
  }">
    <!-- Video Background -->
    <video
      v-if="backgroundType === 'video' && customBackgroundVideo"
      class="background-video"
      :src="customBackgroundVideo"
      autoplay
      loop
      muted
      playsinline
    ></video>

    <!-- Left spacing overlay: hidden during entrance animation so it never covers the first card -->
    <div
      class="left-spacing-overlay"
      :style="{ width: `${entranceAnimationComplete || entranceAnimation === 'none' ? leftSpacing : 0}rem` }"
    ></div>

    <div
      ref="scrollContainer"
      class="carousel-track"
      @mouseenter="handleMouseEnter"
      @mouseleave="handleMouseLeave"
    >
      <div ref="trackInner" class="carousel-track-inner">
      <!-- Duplicate cards for infinite loop effect -->
      <template v-for="n in 2" :key="`set-${n}-${cardStyle}`">
        <div
          v-for="(card, index) in displayCards"
          :key="`${cardStyle}-${n}-${card.id}`"
          :class="[
            'card-wrapper',
            {
              [`entrance-animation-${entranceAnimation}`]: entranceAnimation !== 'none' && n === 1 && index < animatedCardsCount && !entranceAnimationComplete,
              'entrance-hidden': entranceAnimation !== 'none' && n === 1 && index >= animatedCardsCount && !entranceAnimationComplete
            }
          ]"
        >
          <component
            :is="currentCardComponent"
            :key="`${cardStyle}-component-${card.id}`"
            :card="card"
            :primary-color="primaryColor"
            :secondary-color="secondaryColor"
            :primary-color-opacity="primaryColorOpacity"
            :secondary-color-opacity="secondaryColorOpacity"
            :image-shape="imageShape"
            :show-id-badge="showIdBadge"
            :show-category="showCategory"
            :show-description="showDescription"
            :show-price="showPrice"
            :card-background-color="cardBackgroundColor"
            :card-category-bg-color="cardCategoryBgColor"
            :card-footer-bg-color="cardFooterBgColor"
            :card-title-color="cardTitleColor"
            :card-description-color="cardDescriptionColor"
            :card-price-color="cardPriceColor"
            :card-badge-color="cardBadgeColor"
            :card-badge-bg-color="cardBadgeBgColor"
            :card-overlay-color="cardOverlayColor"
            :card-content-bg-color="cardContentBgColor"
            :card-category-color="cardCategoryColor"
            :card-divider-bg-color="cardDividerBgColor"
            :card-ribbon-bg-color="cardRibbonBgColor"
            :card-top-section-bg-color="cardTopSectionBgColor"
            :card-bottom-section-bg-color="cardBottomSectionBgColor"
            :card-glass-overlay-bg-color="cardGlassOverlayBgColor"
            :card-frame-bg-color="cardFrameBgColor"
            :card-border-bg-color="cardBorderBgColor"
            :card-stripes-bg-color="cardStripesBgColor"
            :card-sidebar-bg-color="cardSidebarBgColor"
            :card-layer-bg-color="cardLayerBgColor"
          />
        </div>
      </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.carousel-container {
  width: 100vw;
  overflow: hidden;
  padding: 2rem 0;
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  position: relative;
  margin-left: calc(-50vw + 50%);
}

.background-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
}

.left-spacing-overlay {
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  z-index: 2;
  pointer-events: none;
  flex-shrink: 0;
}

.carousel-track {
  overflow: hidden;
  padding: 1rem 0;
  position: relative;
  z-index: 1;
  min-height: calc(var(--card-height, 520px) + 2rem);
  display: flex;
  align-items: center;
  width: 100%;
}

.carousel-track-inner {
  display: flex;
  gap: var(--card-gap, 24px);
  align-items: center;
  will-change: transform;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

.card-wrapper {
  flex-shrink: 0;
  margin: var(--card-margin, 0px);
  position: relative;
  transition: opacity 0.3s ease;
  opacity: var(--card-opacity, 1);
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
  min-width: var(--card-width, 300px);
  max-width: var(--card-width, 300px);
}

.card-wrapper.entrance-hidden {
  opacity: 0;
  visibility: hidden;
}

/* Flip From Top Animation */
.card-wrapper.entrance-animation-flip-top {
  animation: flipTop 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: center;
}

@keyframes flipTop {
  0% {
    opacity: 0;
    transform: translateY(-100vh) rotateY(90deg) scale(0.5);
  }
  50% {
    opacity: 1;
    transform: translateY(0) rotateY(45deg) scale(0.9);
  }
  100% {
    opacity: 1;
    transform: translateY(0) rotateY(0deg) scale(1);
  }
}

/* Slide From Left Animation */
.card-wrapper.entrance-animation-slide-left {
  animation: slideLeft 0.7s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes slideLeft {
  0% {
    opacity: 0;
    transform: translateX(-150vw) scale(0.8);
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1);
  }
}

/* Slide From Right Animation */
.card-wrapper.entrance-animation-slide-right {
  animation: slideRight 0.7s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes slideRight {
  0% {
    opacity: 0;
    transform: translateX(150vw) scale(0.8);
  }
  100% {
    opacity: 1;
    transform: translateX(0) scale(1);
  }
}

/* Fade In Animation */
.card-wrapper.entrance-animation-fade-in {
  animation: fadeIn 0.8s ease-in-out forwards;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: scale(0.95);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

/* Zoom In Animation */
.card-wrapper.entrance-animation-zoom-in {
  animation: zoomIn 0.7s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes zoomIn {
  0% {
    opacity: 0;
    transform: scale(0);
  }
  60% {
    opacity: 1;
    transform: scale(1.1);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

/* Rotate In Animation */
.card-wrapper.entrance-animation-rotate-in {
  animation: rotateIn 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: center;
}

@keyframes rotateIn {
  0% {
    opacity: 0;
    transform: rotate(-180deg) scale(0.3);
  }
  100% {
    opacity: 1;
    transform: rotate(0deg) scale(1);
  }
}

/* Bounce In Animation */
.card-wrapper.entrance-animation-bounce-in {
  animation: bounceIn 1s cubic-bezier(0.68, -0.55, 0.265, 1.55) forwards;
}

@keyframes bounceIn {
  0% {
    opacity: 0;
    transform: translateY(-100vh) scale(0.3);
  }
  50% {
    opacity: 1;
    transform: translateY(20px) scale(1.05);
  }
  70% {
    transform: translateY(-10px) scale(0.95);
  }
  85% {
    transform: translateY(5px) scale(1.02);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* Spiral In Animation */
.card-wrapper.entrance-animation-spiral-in {
  animation: spiralIn 1s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: center;
}

@keyframes spiralIn {
  0% {
    opacity: 0;
    transform: translate(-50vw, -100vh) rotate(-720deg) scale(0.1);
  }
  100% {
    opacity: 1;
    transform: translate(0, 0) rotate(0deg) scale(1);
  }
}

/* Cascade Fall Animation */
.card-wrapper.entrance-animation-cascade {
  animation: cascadeFall 0.9s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: top center;
}

@keyframes cascadeFall {
  0% {
    opacity: 0;
    transform: translateY(-100vh) rotateX(-90deg) scale(0.5);
  }
  60% {
    opacity: 1;
    transform: translateY(10px) rotateX(10deg) scale(1.05);
  }
  100% {
    opacity: 1;
    transform: translateY(0) rotateX(0deg) scale(1);
  }
}

/* Swing In Animation */
.card-wrapper.entrance-animation-swing-in {
  animation: swingIn 1s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: top center;
}

@keyframes swingIn {
  0% {
    opacity: 0;
    transform: translateY(-100vh) rotate(-45deg);
  }
  30% {
    opacity: 1;
    transform: translateY(0) rotate(20deg);
  }
  60% {
    transform: rotate(-10deg);
  }
  80% {
    transform: rotate(5deg);
  }
  100% {
    opacity: 1;
    transform: rotate(0deg);
  }
}

/* Flip From Bottom Animation */
.card-wrapper.entrance-animation-flip-bottom {
  animation: flipBottom 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: center;
}

@keyframes flipBottom {
  0% {
    opacity: 0;
    transform: translateY(100vh) rotateY(-90deg) scale(0.5);
  }
  50% {
    opacity: 1;
    transform: translateY(0) rotateY(-45deg) scale(0.9);
  }
  100% {
    opacity: 1;
    transform: translateY(0) rotateY(0deg) scale(1);
  }
}

/* Slide Up Animation */
.card-wrapper.entrance-animation-slide-up {
  animation: slideUp 0.7s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes slideUp {
  0% {
    opacity: 0;
    transform: translateY(100vh) scale(0.8);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* Slide Down Animation */
.card-wrapper.entrance-animation-slide-down {
  animation: slideDown 0.7s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes slideDown {
  0% {
    opacity: 0;
    transform: translateY(-100vh) scale(0.8);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

/* Elastic Bounce Animation */
.card-wrapper.entrance-animation-elastic-bounce {
  animation: elasticBounce 1.2s cubic-bezier(0.68, -0.55, 0.265, 1.55) forwards;
}

@keyframes elasticBounce {
  0% {
    opacity: 0;
    transform: scale(0) translateY(-50vh);
  }
  40% {
    opacity: 1;
    transform: scale(1.2) translateY(0);
  }
  60% {
    transform: scale(0.85);
  }
  80% {
    transform: scale(1.08);
  }
  100% {
    opacity: 1;
    transform: scale(1);
  }
}

/* 3D Flip Animation */
.card-wrapper.entrance-animation-3d-flip {
  animation: flip3D 1s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  perspective: 1000px;
  transform-style: preserve-3d;
}

@keyframes flip3D {
  0% {
    opacity: 0;
    transform: rotateX(-180deg) rotateY(-180deg) scale(0.3);
  }
  50% {
    opacity: 1;
    transform: rotateX(-90deg) rotateY(-90deg) scale(0.8);
  }
  100% {
    opacity: 1;
    transform: rotateX(0deg) rotateY(0deg) scale(1);
  }
}

/* Wave In Animation */
.card-wrapper.entrance-animation-wave-in {
  animation: waveIn 0.9s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes waveIn {
  0% {
    opacity: 0;
    transform: translateX(-100vw) translateY(-20px) rotate(-10deg);
  }
  30% {
    transform: translateX(0) translateY(20px) rotate(5deg);
  }
  60% {
    transform: translateX(0) translateY(-10px) rotate(-2deg);
  }
  100% {
    opacity: 1;
    transform: translateX(0) translateY(0) rotate(0deg);
  }
}

/* Tornado Spin Animation */
.card-wrapper.entrance-animation-tornado {
  animation: tornado 1.2s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: center;
}

@keyframes tornado {
  0% {
    opacity: 0;
    transform: translate(-50vw, -100vh) rotate(1080deg) scale(0.1);
  }
  60% {
    opacity: 1;
    transform: translate(0, 0) rotate(360deg) scale(1.1);
  }
  100% {
    opacity: 1;
    transform: translate(0, 0) rotate(0deg) scale(1);
  }
}

/* Fold & Unfold Animation */
.card-wrapper.entrance-animation-fold-unfold {
  animation: foldUnfold 1s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
  transform-origin: center;
  perspective: 1000px;
}

@keyframes foldUnfold {
  0% {
    opacity: 0;
    transform: scaleY(0) rotateX(-90deg);
  }
  50% {
    opacity: 1;
    transform: scaleY(1) rotateX(10deg);
  }
  100% {
    opacity: 1;
    transform: scaleY(1) rotateX(0deg);
  }
}

/* Glitch Effect Animation */
.card-wrapper.entrance-animation-glitch {
  animation: glitch 0.8s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes glitch {
  0% {
    opacity: 0;
    transform: translate(-20px, -20px) skew(10deg);
    filter: hue-rotate(90deg);
  }
  20% {
    opacity: 0.5;
    transform: translate(10px, -10px) skew(-5deg);
    filter: hue-rotate(-45deg);
  }
  40% {
    opacity: 0.7;
    transform: translate(-5px, 15px) skew(8deg);
    filter: hue-rotate(30deg);
  }
  60% {
    opacity: 0.9;
    transform: translate(8px, -5px) skew(-3deg);
    filter: hue-rotate(-15deg);
  }
  80% {
    opacity: 1;
    transform: translate(-3px, 3px) skew(2deg);
    filter: hue-rotate(5deg);
  }
  100% {
    opacity: 1;
    transform: translate(0, 0) skew(0deg);
    filter: hue-rotate(0deg);
  }
}
</style>
