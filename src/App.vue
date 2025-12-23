<script setup>
import { ref, computed } from 'vue';
import CardSlider from './components/CardSlider.vue';

const cardStyles = ['fullwidth-zigzag', 'fullwidth-wave', 'fullwidth-curved', 'layered-block', 'geometric-block', 'curved-block', 'staggered', 'wave', 'striped', 'zigzag', 'corner', 'circular', 'ribbon', 'modern', 'classic', 'minimal', 'elegant', 'bold', 'compact', 'luxury', 'vibrant', 'shadow', 'gradient', 'neon', 'glassmorphism', 'neumorphism', 'metro', 'polaroid', 'magazine', 'stacked', 'retro', 'split', 'diagonal', 'overlap', 'sidebar', 'floating'];

const imageShapes = [
  { value: 'rounded', label: 'Rounded' },
  { value: 'square', label: 'Square' },
  { value: 'circle', label: 'Circle' },
  { value: 'hexagon', label: 'Hexagon' },
  { value: 'diamond', label: 'Diamond' },
  { value: 'pentagon', label: 'Pentagon' },
  { value: 'octagon', label: 'Octagon' },
  { value: 'blob', label: 'Blob' },
  { value: 'triangle', label: 'Triangle' },
  { value: 'star', label: 'Star' },
  { value: 'heart', label: 'Heart' },
  { value: 'shield', label: 'Shield' },
  { value: 'parallelogram', label: 'Parallelogram' },
  { value: 'trapezoid', label: 'Trapezoid' },
  { value: 'ellipse', label: 'Ellipse' },
  { value: 'squircle', label: 'Squircle' },
  { value: 'teardrop', label: 'Teardrop' },
  { value: 'arch', label: 'Arch' },
  { value: 'cross', label: 'Cross' },
  { value: 'badge', label: 'Badge' },
  { value: 'ticket', label: 'Ticket' },
  { value: 'chevron', label: 'Chevron' },
  { value: 'arrow', label: 'Arrow' },
  { value: 'clover', label: 'Clover' }
];

const currentStyle = ref('fullwidth-zigzag');
const isPanelOpen = ref(false);
const primaryColor = ref('#667eea');
const secondaryColor = ref('#764ba2');
const primaryColorOpacity = ref(1);
const secondaryColorOpacity = ref(1);
const scrollSpeed = ref(1);
const imageShape = ref('rounded');
const entranceAnimation = ref('none');
const animationDelay = ref(600);
const cardOpacity = ref(1);
const leftSpacing = ref(6);

// Collapsible section states
const sectionsOpen = ref({
  design: true,
  sections: false,
  typography: false,
  styling: false,
  dimensions: false,
  spacing: false,
  background: false,
  colors: false,
  cardColors: false,
  animation: false
});

// Background controls
const backgroundType = ref('gradient');
const backgroundValue = ref('default-gradient-1');
const customBackgroundColor = ref('#667eea');
const customBackgroundImage = ref('');
const customBackgroundVideo = ref('');

// Card-specific color controls
const cardBackgroundColor = ref('#1a1a2e');
const cardCategoryBgColor = ref('#667eea');
const cardFooterBgColor = ref('#667eea');
const cardTitleColor = ref('#ffffff');
const cardDescriptionColor = ref('#ffffff');
const cardPriceColor = ref('#ffffff');
const cardBadgeColor = ref('#ffffff');
const cardBadgeBgColor = ref('#667eea');
const cardCategoryColor = ref('#ffffff');
const cardOverlayColor = ref('rgba(0, 0, 0, 0.7)');
const cardContentBgColor = ref('#fafafa');

// Extra section backgrounds for special cards
const cardDividerBgColor = ref('#667eea');
const cardRibbonBgColor = ref('#667eea');
const cardTopSectionBgColor = ref('#667eea');
const cardBottomSectionBgColor = ref('#667eea');
const cardGlassOverlayBgColor = ref('rgba(255, 255, 255, 0.3)');
const cardFrameBgColor = ref('#ffffff');
const cardBorderBgColor = ref('#f0f0f0');
const cardStripesBgColor = ref('#667eea');
const cardSidebarBgColor = ref('#667eea');
const cardLayerBgColor = ref('#ffffff');

// Font size controls
const headingFontSize = ref(1.15);
const textFontSize = ref(0.85);
const priceFontSize = ref(1);
const badgeFontSize = ref(0.75);

// Border radius control
const borderRadius = ref(16);

// Layout controls
const cardPadding = ref(16);
const imagePadding = ref(0);
const contentPadding = ref(16);
const cardMargin = ref(0);
const cardGap = ref(24);
const cardWidth = ref(300);
const cardHeight = ref(520);

// Section visibility toggles
const showIdBadge = ref(true);
const showCategory = ref(true);
const showDescription = ref(true);
const showPrice = ref(true);

const toggleSection = (section) => {
  sectionsOpen.value[section] = !sectionsOpen.value[section];
};

const togglePanel = () => {
  isPanelOpen.value = !isPanelOpen.value;
};

const selectCardStyle = (style) => {
  currentStyle.value = style;
};

const updatePrimaryColor = (color) => {
  primaryColor.value = color;
};

const updateSecondaryColor = (color) => {
  secondaryColor.value = color;
};

const updateSpeed = (speed) => {
  scrollSpeed.value = parseFloat(speed);
};

const resetSettings = () => {
  headingFontSize.value = 1.15;
  textFontSize.value = 0.85;
  priceFontSize.value = 1;
  badgeFontSize.value = 0.75;
  borderRadius.value = 16;
  imageShape.value = 'rounded';
  cardPadding.value = 16;
  imagePadding.value = 0;
  contentPadding.value = 16;
  cardMargin.value = 0;
  cardGap.value = 24;
  cardWidth.value = 300;
  cardHeight.value = 520;
  showIdBadge.value = true;
  showCategory.value = true;
  showDescription.value = true;
  showPrice.value = true;
  entranceAnimation.value = 'none';
  animationDelay.value = 600;
  cardOpacity.value = 1;
  leftSpacing.value = 6;
  primaryColorOpacity.value = 1;
  secondaryColorOpacity.value = 1;
  backgroundType.value = 'gradient';
  backgroundValue.value = 'default-gradient-1';
  customBackgroundColor.value = '#667eea';
  customBackgroundImage.value = '';
  customBackgroundVideo.value = '';
  cardBackgroundColor.value = '#1a1a2e';
  cardCategoryBgColor.value = '#667eea';
  cardFooterBgColor.value = '#667eea';
  cardTitleColor.value = '#ffffff';
  cardDescriptionColor.value = '#ffffff';
  cardPriceColor.value = '#ffffff';
  cardBadgeColor.value = '#ffffff';
  cardBadgeBgColor.value = '#667eea';
  cardOverlayColor.value = 'rgba(0, 0, 0, 0.7)';
  cardContentBgColor.value = '#fafafa';
  cardDividerBgColor.value = '#667eea';
  cardRibbonBgColor.value = '#667eea';
  cardTopSectionBgColor.value = '#667eea';
  cardBottomSectionBgColor.value = '#667eea';
  cardGlassOverlayBgColor.value = 'rgba(255, 255, 255, 0.3)';
  cardFrameBgColor.value = '#ffffff';
  cardBorderBgColor.value = '#f0f0f0';
  cardStripesBgColor.value = '#667eea';
  cardSidebarBgColor.value = '#667eea';
  cardLayerBgColor.value = '#ffffff';
  cardCategoryColor.value = '#ffffff';
};

const cardStyleOptions = {
  modern: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardFooterBgColor', label: 'Footer Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeColor', label: 'Badge Text Color' },
    { key: 'cardBadgeBgColor', label: 'Badge Background' }
  ],
  classic: [
    { key: 'cardBadgeBgColor', label: 'ID Badge Background' },
    { key: 'cardBadgeColor', label: 'Category Tag Text' },
    { key: 'cardFooterBgColor', label: 'Footer Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardOverlayColor', label: 'Image Overlay' },
    { key: 'cardContentBgColor', label: 'Content Background' }
  ],
  minimal: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeColor', label: 'Badge Color' }
  ],
  elegant: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeColor', label: 'Badge Color' }
  ],
  bold: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardFooterBgColor', label: 'Footer Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  compact: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeBgColor', label: 'Badge Background' }
  ],
  luxury: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardFooterBgColor', label: 'Footer Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  vibrant: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  shadow: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeBgColor', label: 'Badge Background' }
  ],
  gradient: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  neon: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Neon Accent' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  glassmorphism: [
    { key: 'cardBackgroundColor', label: 'Glass Background' },
    { key: 'cardGlassOverlayBgColor', label: 'Glass Overlay Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeBgColor', label: 'Badge Background' }
  ],
  neumorphism: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryBgColor', label: 'Category Background' }
  ],
  metro: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeBgColor', label: 'Badge Background' }
  ],
  polaroid: [
    { key: 'cardFrameBgColor', label: 'Frame Background' },
    { key: 'cardBackgroundColor', label: 'Photo Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryBgColor', label: 'Category Color' }
  ],
  magazine: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Headline Color' },
    { key: 'cardDescriptionColor', label: 'Article Text Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryBgColor', label: 'Section Color' }
  ],
  stacked: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardLayerBgColor', label: 'Stack Layers Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardBottomSectionBgColor', label: 'Price Section Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardBadgeBgColor', label: 'Badge Background' }
  ],
  retro: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardBorderBgColor', label: 'Border Background' },
    { key: 'cardStripesBgColor', label: 'Stripes Background' },
    { key: 'cardCategoryBgColor', label: 'Label Background' },
    { key: 'cardTitleColor', label: 'Heading Color' },
    { key: 'cardDescriptionColor', label: 'Text Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  split: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryBgColor', label: 'Category Color' }
  ],
  diagonal: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Tag Background' },
    { key: 'cardDividerBgColor', label: 'Divider Background' },
    { key: 'cardBottomSectionBgColor', label: 'Price Section Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  overlap: [
    { key: 'cardBackgroundColor', label: 'Content Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryBgColor', label: 'Category Background' }
  ],
  sidebar: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardSidebarBgColor', label: 'Sidebar Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryBgColor', label: 'Label Color' }
  ],
  floating: [
    { key: 'cardBackgroundColor', label: 'Content Background' },
    { key: 'cardOverlayColor', label: 'Floating Overlay Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  ribbon: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Tag Background' },
    { key: 'cardRibbonBgColor', label: 'Ribbon Banner Background' },
    { key: 'cardBottomSectionBgColor', label: 'Price Strip Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  circular: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  corner: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Color' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  zigzag: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTopSectionBgColor', label: 'Top Section Background' },
    { key: 'cardCategoryBgColor', label: 'Middle Section Background' },
    { key: 'cardBottomSectionBgColor', label: 'Bottom Section Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  striped: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryColor', label: 'Category Text Color' }
  ],
  wave: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  staggered: [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryColor', label: 'Category Text Color' }
  ],
  'curved-block': [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  'geometric-block': [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' },
    { key: 'cardCategoryColor', label: 'Category Text Color' }
  ],
  'layered-block': [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  'fullwidth-zigzag': [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  'fullwidth-wave': [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ],
  'fullwidth-curved': [
    { key: 'cardBackgroundColor', label: 'Card Background' },
    { key: 'cardCategoryBgColor', label: 'Category Background' },
    { key: 'cardTitleColor', label: 'Title Color' },
    { key: 'cardDescriptionColor', label: 'Description Color' },
    { key: 'cardPriceColor', label: 'Price Color' }
  ]
};

const currentCardOptions = computed(() => {
  return cardStyleOptions[currentStyle.value] || [];
});

const handleImageUpload = (event) => {
  const file = event.target.files[0];
  if (file && file.type.startsWith('image/')) {
    const reader = new FileReader();
    reader.onload = (e) => {
      customBackgroundImage.value = e.target.result;
      backgroundType.value = 'image';
      backgroundValue.value = 'custom';
    };
    reader.readAsDataURL(file);
  }
};

const handleVideoUpload = (event) => {
  const file = event.target.files[0];
  if (file && file.type.startsWith('video/')) {
    const reader = new FileReader();
    reader.onload = (e) => {
      customBackgroundVideo.value = e.target.result;
      backgroundType.value = 'video';
      backgroundValue.value = 'custom';
    };
    reader.readAsDataURL(file);
  }
};

const selectBackgroundType = (type) => {
  backgroundType.value = type;
  if (type === 'none') {
    backgroundValue.value = '';
  } else if (type === 'color') {
    backgroundValue.value = 'custom';
  } else if (type === 'gradient') {
    backgroundValue.value = 'default-gradient-1';
  }
};

const colorRefs = {
  cardBackgroundColor,
  cardCategoryBgColor,
  cardFooterBgColor,
  cardTitleColor,
  cardDescriptionColor,
  cardPriceColor,
  cardBadgeColor,
  cardBadgeBgColor,
  cardOverlayColor,
  cardContentBgColor,
  cardDividerBgColor,
  cardRibbonBgColor,
  cardTopSectionBgColor,
  cardBottomSectionBgColor,
  cardGlassOverlayBgColor,
  cardFrameBgColor,
  cardBorderBgColor,
  cardStripesBgColor,
  cardSidebarBgColor,
  cardLayerBgColor,
  cardCategoryColor
};

const getColorValue = (key) => {
  return colorRefs[key]?.value || '#000000';
};

const setColorValue = (key, value) => {
  if (colorRefs[key]) {
    colorRefs[key].value = value;
  }
};
</script>

<template>
  <div class="app-container" :style="{ '--primary-color': primaryColor, '--secondary-color': secondaryColor }">
    <main class="app-main">
      <CardSlider
        :card-style="currentStyle"
        :primary-color="primaryColor"
        :secondary-color="secondaryColor"
        :primary-color-opacity="primaryColorOpacity"
        :secondary-color-opacity="secondaryColorOpacity"
        :scroll-speed="scrollSpeed"
        :heading-font-size="headingFontSize"
        :text-font-size="textFontSize"
        :price-font-size="priceFontSize"
        :badge-font-size="badgeFontSize"
        :border-radius="borderRadius"
        :image-shape="imageShape"
        :card-padding="cardPadding"
        :image-padding="imagePadding"
        :content-padding="contentPadding"
        :card-margin="cardMargin"
        :card-gap="cardGap"
        :card-width="cardWidth"
        :card-height="cardHeight"
        :show-id-badge="showIdBadge"
        :show-category="showCategory"
        :show-description="showDescription"
        :show-price="showPrice"
        :entrance-animation="entranceAnimation"
        :animation-delay="animationDelay"
        :card-opacity="cardOpacity"
        :left-spacing="leftSpacing"
        :background-type="backgroundType"
        :background-value="backgroundValue"
        :custom-background-color="customBackgroundColor"
        :custom-background-image="customBackgroundImage"
        :custom-background-video="customBackgroundVideo"
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
      />
    </main>

    <!-- Floating Settings Button -->
    <button class="settings-btn" @click="togglePanel">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
        <circle cx="12" cy="12" r="3"/>
        <path d="M12 1v6m0 6v6m-6-6h6m6 0h-6"/>
        <path d="M19.07 4.93l-4.24 4.24m0 5.66l4.24 4.24M4.93 4.93l4.24 4.24m0 5.66l-4.24 4.24"/>
      </svg>
      <span>Settings</span>
    </button>

    <!-- Right Side Panel -->
    <div :class="['settings-panel', { open: isPanelOpen }]">
      <div class="panel-header">
        <div class="header-content">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="12" cy="12" r="3"/>
            <path d="M12 1v6m0 6v6m-6-6h6m6 0h-6"/>
            <path d="M19.07 4.93l-4.24 4.24m0 5.66l4.24 4.24M4.93 4.93l4.24 4.24m0 5.66l-4.24 4.24"/>
          </svg>
          <h2 class="panel-title">Customize Cards</h2>
        </div>
        <button class="close-btn" @click="togglePanel" title="Close settings">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <line x1="18" y1="6" x2="6" y2="18"/>
            <line x1="6" y1="6" x2="18" y2="18"/>
          </svg>
        </button>
      </div>

      <div class="panel-content">
        <!-- Design Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('design')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="3" y="3" width="7" height="7"/>
                <rect x="14" y="3" width="7" height="7"/>
                <rect x="14" y="14" width="7" height="7"/>
                <rect x="3" y="14" width="7" height="7"/>
              </svg>
              <h3 class="section-title">Card Design</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.design }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.design" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z"/>
                </svg>
                Card Style
              </label>
              <div class="dropdown-wrapper enhanced-dropdown">
                <select v-model="currentStyle" @change="selectCardStyle(currentStyle)" class="dropdown-select styled-select">
                  <optgroup label="🎯 Full Width Cards">
                    <option value="fullwidth-zigzag">⚡ Full Width Zigzag</option>
                    <option value="fullwidth-wave">🌊 Full Width Wave</option>
                    <option value="fullwidth-curved">🌀 Full Width Curved</option>
                  </optgroup>
                  <optgroup label="🎨 Block Cards">
                    <option value="layered-block">📚 Layered Block</option>
                    <option value="geometric-block">🔷 Geometric Block</option>
                    <option value="curved-block">🔶 Curved Block</option>
                  </optgroup>
                  <optgroup label="✨ Special Effects">
                    <option value="glassmorphism">💎 Glassmorphism</option>
                    <option value="neumorphism">🎭 Neumorphism</option>
                    <option value="neon">💫 Neon</option>
                    <option value="gradient">🌈 Gradient</option>
                    <option value="shadow">🌑 Shadow</option>
                  </optgroup>
                  <optgroup label="🎪 Creative Designs">
                    <option value="staggered">📐 Staggered</option>
                    <option value="wave">〰️ Wave</option>
                    <option value="striped">📊 Striped</option>
                    <option value="zigzag">⚡ Zigzag</option>
                    <option value="corner">📌 Corner</option>
                    <option value="circular">⭕ Circular</option>
                    <option value="ribbon">🎀 Ribbon</option>
                    <option value="diagonal">📐 Diagonal</option>
                    <option value="overlap">🔲 Overlap</option>
                    <option value="sidebar">📑 Sidebar</option>
                    <option value="floating">🎈 Floating</option>
                  </optgroup>
                  <optgroup label="🎯 Classic Styles">
                    <option value="modern">🔲 Modern</option>
                    <option value="classic">📖 Classic</option>
                    <option value="minimal">⚪ Minimal</option>
                    <option value="elegant">💎 Elegant</option>
                    <option value="bold">💪 Bold</option>
                    <option value="compact">📦 Compact</option>
                    <option value="luxury">👑 Luxury</option>
                    <option value="vibrant">🎨 Vibrant</option>
                  </optgroup>
                  <optgroup label="🎬 Vintage & Modern">
                    <option value="retro">📼 Retro</option>
                    <option value="polaroid">📷 Polaroid</option>
                    <option value="magazine">📰 Magazine</option>
                    <option value="metro">🏙️ Metro</option>
                    <option value="stacked">📚 Stacked</option>
                    <option value="split">✂️ Split</option>
                  </optgroup>
                </select>
                <svg class="dropdown-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polyline points="6 9 12 15 18 9"/>
                </svg>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
                  <circle cx="8.5" cy="8.5" r="1.5"/>
                  <path d="M21 15l-5-5L5 21"/>
                </svg>
                Image Shape
              </label>
              <div class="shape-selector-grid">
                <button
                  v-for="shape in imageShapes"
                  :key="shape.value"
                  :class="['shape-option', { active: imageShape === shape.value }]"
                  @click="imageShape = shape.value"
                  type="button"
                  :title="shape.label"
                >
                  <div class="shape-preview" :class="`shape-preview-${shape.value}`">
                    <div class="shape-inner"></div>
                  </div>
                  <span class="shape-label">{{ shape.label }}</span>
                </button>
              </div>
            </div>

            <div class="preview-badge-wrapper">
              <div class="current-style-badge" :style="{ background: `linear-gradient(135deg, ${primaryColor} 0%, ${secondaryColor} 100%)` }">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
                  <polyline points="22 4 12 14.01 9 11.01"/>
                </svg>
                {{ currentStyle }}
              </div>
            </div>
          </div>
        </div>

        <!-- Card Sections -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('sections')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M9 11H3v2h6m-6 4h6v2H3m0-12h6v2H3m9 4h9v2h-9m9 4h-9v2h9m-9-12h9v2h-9"/>
              </svg>
              <h3 class="section-title">Visible Sections</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.sections }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.sections" class="section-content">
            <div class="toggle-grid">
              <div class="toggle-item">
                <label class="toggle-label">
                  <input type="checkbox" v-model="showIdBadge" class="toggle-checkbox">
                  <span class="toggle-switch"></span>
                  <span class="toggle-text">ID Badge</span>
                </label>
              </div>
              <div class="toggle-item">
                <label class="toggle-label">
                  <input type="checkbox" v-model="showCategory" class="toggle-checkbox">
                  <span class="toggle-switch"></span>
                  <span class="toggle-text">Category</span>
                </label>
              </div>
              <div class="toggle-item">
                <label class="toggle-label">
                  <input type="checkbox" v-model="showDescription" class="toggle-checkbox">
                  <span class="toggle-switch"></span>
                  <span class="toggle-text">Description</span>
                </label>
              </div>
              <div class="toggle-item">
                <label class="toggle-label">
                  <input type="checkbox" v-model="showPrice" class="toggle-checkbox">
                  <span class="toggle-switch"></span>
                  <span class="toggle-text">Price</span>
                </label>
              </div>
            </div>
          </div>
        </div>

        <!-- Typography Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('typography')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="4 7 4 4 20 4 20 7"/>
                <line x1="9" y1="20" x2="15" y2="20"/>
                <line x1="12" y1="4" x2="12" y2="20"/>
              </svg>
              <h3 class="section-title">Typography</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.typography }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.typography" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M6 4h8a4 4 0 0 1 4 4 4 4 0 0 1-4 4H6z"/>
                  <path d="M6 12h9a4 4 0 0 1 4 4 4 4 0 0 1-4 4H6z"/>
                </svg>
                Heading Size: {{ headingFontSize }}rem
              </label>
              <input type="range" v-model="headingFontSize" min="0.8" max="2" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Small</span>
                <span>Large</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="17" y1="10" x2="3" y2="10"/>
                  <line x1="21" y1="6" x2="3" y2="6"/>
                  <line x1="21" y1="14" x2="3" y2="14"/>
                  <line x1="17" y1="18" x2="3" y2="18"/>
                </svg>
                Text Size: {{ textFontSize }}rem
              </label>
              <input type="range" v-model="textFontSize" min="0.6" max="1.5" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Small</span>
                <span>Large</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="12" y1="1" x2="12" y2="23"/>
                  <path d="M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/>
                </svg>
                Price Size: {{ priceFontSize }}rem
              </label>
              <input type="range" v-model="priceFontSize" min="0.7" max="2" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Small</span>
                <span>Large</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M20.59 13.41l-7.17 7.17a2 2 0 0 1-2.83 0L2 12V2h10l8.59 8.59a2 2 0 0 1 0 2.82z"/>
                  <line x1="7" y1="7" x2="7.01" y2="7"/>
                </svg>
                Badge Size: {{ badgeFontSize }}rem
              </label>
              <input type="range" v-model="badgeFontSize" min="0.5" max="1.2" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Small</span>
                <span>Large</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Card Styling Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('styling')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
              </svg>
              <h3 class="section-title">Card Styling</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.styling }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.styling" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
                </svg>
                Border Radius: {{ borderRadius }}px
              </label>
              <input type="range" v-model="borderRadius" min="0" max="40" step="2" class="range-input" />
              <div class="range-labels">
                <span>Sharp</span>
                <span>Rounded</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="2" y="2" width="20" height="20" rx="2" ry="2"/>
                  <path d="M7 7h10v10H7z"/>
                </svg>
                Card Padding: {{ cardPadding }}px
              </label>
              <input type="range" v-model="cardPadding" min="0" max="40" step="2" class="range-input" />
              <div class="range-labels">
                <span>None</span>
                <span>Large</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
                  <circle cx="8.5" cy="8.5" r="1.5"/>
                  <path d="M21 15l-5-5L5 21"/>
                </svg>
                Image Padding: {{ imagePadding }}px
              </label>
              <input type="range" v-model="imagePadding" min="0" max="40" step="2" class="range-input" />
              <div class="range-labels">
                <span>None</span>
                <span>Large</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="8" y1="6" x2="21" y2="6"/>
                  <line x1="8" y1="12" x2="21" y2="12"/>
                  <line x1="8" y1="18" x2="21" y2="18"/>
                  <line x1="3" y1="6" x2="3.01" y2="6"/>
                  <line x1="3" y1="12" x2="3.01" y2="12"/>
                  <line x1="3" y1="18" x2="3.01" y2="18"/>
                </svg>
                Content Padding: {{ contentPadding }}px
              </label>
              <input type="range" v-model="contentPadding" min="0" max="40" step="2" class="range-input" />
              <div class="range-labels">
                <span>None</span>
                <span>Large</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Card Dimensions Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('dimensions')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="2" y="7" width="20" height="14" rx="2" ry="2"/>
                <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/>
              </svg>
              <h3 class="section-title">Card Dimensions</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.dimensions }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.dimensions" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="3" y1="12" x2="21" y2="12"/>
                  <polyline points="8 8 4 12 8 16"/>
                  <polyline points="16 16 20 12 16 8"/>
                </svg>
                Card Width: {{ cardWidth }}px
              </label>
              <input type="range" v-model="cardWidth" min="200" max="500" step="10" class="range-input" />
              <div class="range-labels">
                <span>Narrow</span>
                <span>Wide</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <line x1="12" y1="3" x2="12" y2="21"/>
                  <polyline points="8 8 12 4 16 8"/>
                  <polyline points="16 16 12 20 8 16"/>
                </svg>
                Card Height: {{ cardHeight }}px
              </label>
              <input type="range" v-model="cardHeight" min="400" max="700" step="10" class="range-input" />
              <div class="range-labels">
                <span>Short</span>
                <span>Tall</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Spacing Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('spacing')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="3" y="3" width="7" height="7"/>
                <rect x="14" y="14" width="7" height="7"/>
              </svg>
              <h3 class="section-title">Spacing</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.spacing }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.spacing" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="3" y="3" width="7" height="7"/>
                  <rect x="14" y="3" width="7" height="7"/>
                  <rect x="14" y="14" width="7" height="7"/>
                  <rect x="3" y="14" width="7" height="7"/>
                </svg>
                Card Gap: {{ cardGap }}px
              </label>
              <input type="range" v-model="cardGap" min="0" max="80" step="4" class="range-input" />
              <div class="range-labels">
                <span>Tight</span>
                <span>Loose</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <rect x="5" y="5" width="14" height="14" rx="2" ry="2"/>
                </svg>
                Card Margin: {{ cardMargin }}px
              </label>
              <input type="range" v-model="cardMargin" min="0" max="40" step="2" class="range-input" />
              <div class="range-labels">
                <span>None</span>
                <span>Large</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Background Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('background')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <rect x="3" y="3" width="18" height="18" rx="2"/>
                <path d="M3 9h18M9 21V9"/>
              </svg>
              <h3 class="section-title">Background</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.background }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.background" class="section-content">
            <div class="form-group">
              <label class="form-label">Background Type</label>
              <div class="background-type-grid">
                <button :class="['type-btn', { active: backgroundType === 'none' }]" @click="selectBackgroundType('none')">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <circle cx="12" cy="12" r="10"/>
                    <line x1="4.93" y1="4.93" x2="19.07" y2="19.07"/>
                  </svg>
                  None
                </button>
                <button :class="['type-btn', { active: backgroundType === 'gradient' }]" @click="selectBackgroundType('gradient')">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="18" height="18" rx="2"/>
                    <path d="M3 9h18M9 21V9"/>
                  </svg>
                  Gradient
                </button>
                <button :class="['type-btn', { active: backgroundType === 'color' }]" @click="selectBackgroundType('color')">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <circle cx="12" cy="12" r="10"/>
                    <path d="M12 2v20"/>
                  </svg>
                  Color
                </button>
                <button :class="['type-btn', { active: backgroundType === 'image' }]" @click="selectBackgroundType('image')">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2"/>
                    <circle cx="8.5" cy="8.5" r="1.5"/>
                    <path d="M21 15l-5-5L5 21"/>
                  </svg>
                  Image
                </button>
                <button :class="['type-btn', { active: backgroundType === 'video' }]" @click="selectBackgroundType('video')">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <polygon points="5 3 19 12 5 21 5 3"/>
                  </svg>
                  Video
                </button>
              </div>
            </div>

            <div v-if="backgroundType === 'gradient'" class="form-group">
              <label class="form-label">Select Gradient</label>
              <div class="dropdown-wrapper">
                <select v-model="backgroundValue" class="dropdown-select">
                  <option value="default-gradient-1">Purple Blue</option>
                  <option value="default-gradient-2">Sunset Orange</option>
                  <option value="default-gradient-3">Ocean Blue</option>
                  <option value="default-gradient-4">Forest Green</option>
                  <option value="default-gradient-5">Pink Purple</option>
                  <option value="default-gradient-6">Dark Night</option>
                  <option value="default-gradient-7">Warm Flame</option>
                  <option value="default-gradient-8">Cool Sky</option>
                  <option value="default-gradient-9">Peachy</option>
                  <option value="default-gradient-10">Mint Fresh</option>
                </select>
                <svg class="dropdown-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polyline points="6 9 12 15 18 9"/>
                </svg>
              </div>
            </div>

            <div v-if="backgroundType === 'color'" class="form-group">
              <label class="form-label">Background Color</label>
              <div class="color-input-wrapper">
                <input type="color" v-model="customBackgroundColor" class="color-input" />
                <span class="color-value">{{ customBackgroundColor }}</span>
              </div>
            </div>

            <div v-if="backgroundType === 'image'" class="form-group">
              <label class="form-label">Upload Image</label>
              <div class="upload-wrapper">
                <input type="file" accept="image/*" @change="handleImageUpload" class="file-input" id="image-upload" />
                <label for="image-upload" class="upload-btn">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
                    <polyline points="17 8 12 3 7 8"/>
                    <line x1="12" y1="3" x2="12" y2="15"/>
                  </svg>
                  Choose Image
                </label>
                <div v-if="customBackgroundImage" class="preview-thumbnail">
                  <img :src="customBackgroundImage" alt="Background preview" />
                </div>
              </div>
            </div>

            <div v-if="backgroundType === 'video'" class="form-group">
              <label class="form-label">Upload Video</label>
              <div class="upload-wrapper">
                <input type="file" accept="video/*" @change="handleVideoUpload" class="file-input" id="video-upload" />
                <label for="video-upload" class="upload-btn">
                  <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
                    <polyline points="17 8 12 3 7 8"/>
                    <line x1="12" y1="3" x2="12" y2="15"/>
                  </svg>
                  Choose Video
                </label>
                <div v-if="customBackgroundVideo" class="preview-thumbnail video-preview">
                  <video :src="customBackgroundVideo" muted loop></video>
                  <span class="video-label">Video loaded</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Theme Colors Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('colors')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M12 2.69l5.66 5.66a8 8 0 1 1-11.31 0z"/>
              </svg>
              <h3 class="section-title">Theme Colors</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.colors }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.colors" class="section-content">
            <div class="form-group">
              <label class="form-label">Primary Color</label>
              <div class="color-input-wrapper">
                <input type="color" v-model="primaryColor" @input="updatePrimaryColor(primaryColor)" class="color-input" />
                <span class="color-value">{{ primaryColor }}</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Primary Opacity: {{ primaryColorOpacity }}</label>
              <input type="range" v-model="primaryColorOpacity" min="0.1" max="1" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Transparent</span>
                <span>Solid</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Secondary Color</label>
              <div class="color-input-wrapper">
                <input type="color" v-model="secondaryColor" @input="updateSecondaryColor(secondaryColor)" class="color-input" />
                <span class="color-value">{{ secondaryColor }}</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Secondary Opacity: {{ secondaryColorOpacity }}</label>
              <input type="range" v-model="secondaryColorOpacity" min="0.1" max="1" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Transparent</span>
                <span>Solid</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Card Opacity: {{ cardOpacity }}</label>
              <input type="range" v-model="cardOpacity" min="0.1" max="1" step="0.05" class="range-input" />
              <div class="range-labels">
                <span>Transparent</span>
                <span>Solid</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Card-Specific Colors Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('cardColors')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="13.5" cy="6.5" r=".5"/>
                <circle cx="17.5" cy="10.5" r=".5"/>
                <circle cx="8.5" cy="7.5" r=".5"/>
                <circle cx="6.5" cy="12.5" r=".5"/>
                <path d="M12 2C6.5 2 2 6.5 2 12s4.5 10 10 10c.926 0 1.648-.746 1.648-1.688 0-.437-.18-.835-.437-1.125-.29-.289-.438-.652-.438-1.125a1.64 1.64 0 0 1 1.668-1.668h1.996c3.051 0 5.555-2.503 5.555-5.554C21.965 6.012 17.461 2 12 2z"/>
              </svg>
              <h3 class="section-title">{{ currentStyle }} Colors</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.cardColors }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.cardColors" class="section-content">
            <p class="section-description">Customize colors for the {{ currentStyle }} card style</p>
            <div v-for="option in currentCardOptions" :key="option.key" class="form-group">
              <label class="form-label">{{ option.label }}</label>
              <div class="color-input-wrapper">
                <input type="color" :value="getColorValue(option.key)" @input="setColorValue(option.key, $event.target.value)" class="color-input" />
                <span class="color-value">{{ getColorValue(option.key) }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Animation Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('animation')">
            <div class="section-header-left">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polygon points="5 3 19 12 5 21 5 3"/>
              </svg>
              <h3 class="section-title">Animation</h3>
            </div>
            <svg :class="['chevron-icon', { rotated: sectionsOpen.animation }]" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>
          
          <div v-show="sectionsOpen.animation" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polygon points="5 3 19 12 5 21 5 3"/>
                </svg>
                Entrance Animation
              </label>
              <div class="dropdown-wrapper enhanced-dropdown">
                <select v-model="entranceAnimation" class="dropdown-select styled-select">
                  <option value="none">⛔ None</option>
                  <optgroup label="⬆️ Flip Animations">
                    <option value="flip-top">🔼 Flip From Top</option>
                    <option value="flip-bottom">🔽 Flip From Bottom</option>
                    <option value="3d-flip">🎲 3D Flip</option>
                  </optgroup>
                  <optgroup label="➡️ Slide Animations">
                    <option value="slide-left">⬅️ Slide From Left</option>
                    <option value="slide-right">➡️ Slide From Right</option>
                    <option value="slide-up">⬆️ Slide Up</option>
                    <option value="slide-down">⬇️ Slide Down</option>
                  </optgroup>
                  <optgroup label="🎯 Zoom & Rotate">
                    <option value="zoom-in">🔍 Zoom In</option>
                    <option value="rotate-in">🔄 Rotate In</option>
                    <option value="spiral-in">🌀 Spiral In</option>
                    <option value="tornado">🌪️ Tornado Spin</option>
                  </optgroup>
                  <optgroup label="🎪 Bounce & Swing">
                    <option value="bounce-in">⚡ Bounce In</option>
                    <option value="elastic-bounce">🎾 Elastic Bounce</option>
                    <option value="swing-in">🎯 Swing In</option>
                  </optgroup>
                  <optgroup label="✨ Special Effects">
                    <option value="fade-in">💫 Fade In Sequence</option>
                    <option value="cascade">🌊 Cascade Fall</option>
                    <option value="wave-in">〰️ Wave In</option>
                    <option value="fold-unfold">📄 Fold & Unfold</option>
                    <option value="glitch">⚠️ Glitch Effect</option>
                  </optgroup>
                </select>
                <svg class="dropdown-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <polyline points="6 9 12 15 18 9"/>
                </svg>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Animation Delay: {{ animationDelay }}ms</label>
              <input type="range" v-model="animationDelay" min="100" max="2000" step="100" class="range-input" />
              <div class="range-labels">
                <span>Fast</span>
                <span>Slow</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Left Spacing: {{ leftSpacing }}rem</label>
              <input type="range" v-model="leftSpacing" min="0" max="15" step="0.5" class="range-input" />
              <div class="range-labels">
                <span>None</span>
                <span>Wide</span>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Scroll Speed: {{ scrollSpeed }}x</label>
              <input type="range" v-model="scrollSpeed" @input="updateSpeed(scrollSpeed)" min="0.1" max="5" step="0.1" class="range-input" />
              <div class="range-labels">
                <span>Slow</span>
                <span>Fast</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Reset Button -->
        <button class="reset-btn" @click="resetSettings">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M3 12a9 9 0 0 1 9-9 9.75 9.75 0 0 1 6.74 2.74L21 8"/>
            <path d="M21 3v5h-5"/>
            <path d="M21 12a9 9 0 0 1-9 9 9.75 9.75 0 0 1-6.74-2.74L3 16"/>
            <path d="M3 21v-5h5"/>
          </svg>
          Reset All Settings
        </button>
      </div>
    </div>

    <!-- Overlay -->
    <div v-if="isPanelOpen" class="overlay" @click="togglePanel"></div>
  </div>
</template>

<style scoped>
.app-container {
  min-height: 100vh;
  background: #f5f7fa;
  position: relative;
}

.app-main {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 2rem 0;
}

.settings-btn {
  position: fixed;
  top: 2rem;
  right: 2rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.875rem 1.75rem;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  color: white;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
  z-index: 100;
}

.settings-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.5);
}

.settings-btn:active {
  transform: translateY(-1px);
}

.settings-btn svg {
  width: 20px;
  height: 20px;
}

.settings-panel {
  position: fixed;
  top: 0;
  right: -480px;
  width: 480px;
  height: 100vh;
  background: #ffffff;
  box-shadow: -6px 0 30px rgba(0, 0, 0, 0.15);
  transition: right 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  z-index: 1000;
  display: flex;
  flex-direction: column;
}

.settings-panel.open {
  right: 0;
}

.panel-header {
  padding: 1.75rem 2rem;
  border-bottom: 2px solid rgba(255, 255, 255, 0.2);
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
}

.header-content {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.header-content svg {
  width: 24px;
  height: 24px;
  color: white;
}

.panel-title {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
  letter-spacing: -0.5px;
}

.close-btn {
  background: rgba(255, 255, 255, 0.2);
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  color: white;
}

.close-btn:hover {
  background: rgba(255, 255, 255, 0.35);
  transform: rotate(90deg);
}

.panel-content {
  padding: 1.5rem;
  overflow-y: auto;
  flex: 1;
  background: linear-gradient(to bottom, #f8f9fa 0%, #ffffff 100%);
}

.panel-content::-webkit-scrollbar {
  width: 8px;
}

.panel-content::-webkit-scrollbar-track {
  background: #f1f1f1;
}

.panel-content::-webkit-scrollbar-thumb {
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  border-radius: 4px;
}

.panel-content::-webkit-scrollbar-thumb:hover {
  background: linear-gradient(135deg, var(--secondary-color, #764ba2) 0%, var(--primary-color, #667eea) 100%);
}

.collapsible-section {
  margin-bottom: 1rem;
  background: white;
  border-radius: 14px;
  border: 1px solid #e5e7eb;
  overflow: hidden;
  transition: all 0.3s ease;
}

.collapsible-section:hover {
  border-color: var(--primary-color, #667eea);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.1);
}

.section-header {
  width: 100%;
  padding: 1.25rem 1.5rem;
  background: linear-gradient(to right, #fafbfc 0%, #ffffff 100%);
  border: none;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
  transition: all 0.3s ease;
  border-bottom: 1px solid transparent;
}

.section-header:hover {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.05) 0%, rgba(118, 75, 162, 0.05) 100%);
}

.section-header-left {
  display: flex;
  align-items: center;
  gap: 0.875rem;
}

.section-header-left svg {
  width: 20px;
  height: 20px;
  color: var(--primary-color, #667eea);
}

.section-title {
  margin: 0;
  font-size: 1rem;
  font-weight: 700;
  color: #1f2937;
  letter-spacing: -0.2px;
  text-align: left;
}

.chevron-icon {
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  color: #9ca3af;
}

.chevron-icon.rotated {
  transform: rotate(180deg);
}

.section-content {
  padding: 1.5rem;
  border-top: 1px solid #f3f4f6;
  animation: slideDown 0.3s ease;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.section-description {
  margin: 0 0 1.25rem 0;
  font-size: 0.85rem;
  color: #6b7280;
  font-style: italic;
  line-height: 1.5;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group:last-child {
  margin-bottom: 0;
}

.form-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.875rem;
  font-size: 0.9rem;
  font-weight: 600;
  color: #374151;
}

.form-label svg {
  width: 16px;
  height: 16px;
  color: var(--primary-color, #667eea);
}

.dropdown-wrapper {
  position: relative;
}

.dropdown-select {
  width: 100%;
  padding: 0.875rem 2.75rem 0.875rem 1.125rem;
  font-size: 0.95rem;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  background: white;
  color: #1f2937;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  font-weight: 500;
}

.dropdown-select:hover {
  border-color: var(--primary-color, #667eea);
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.08);
}

.dropdown-select:focus {
  outline: none;
  border-color: var(--primary-color, #667eea);
  box-shadow: 0 0 0 4px rgba(102, 126, 234, 0.15);
}

.dropdown-icon {
  position: absolute;
  right: 1.125rem;
  top: 50%;
  transform: translateY(-50%);
  pointer-events: none;
  color: #9ca3af;
  transition: color 0.3s ease;
}

.dropdown-wrapper:hover .dropdown-icon {
  color: var(--primary-color, #667eea);
}

.toggle-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0.875rem;
}

.toggle-item {
  background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%);
  padding: 0.875rem 1rem;
  border-radius: 12px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 2px solid transparent;
}

.toggle-item:hover {
  background: linear-gradient(135deg, #f3f4f6 0%, #e5e7eb 100%);
  border-color: var(--primary-color, #667eea);
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.08);
}

.toggle-label {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  cursor: pointer;
  user-select: none;
}

.toggle-checkbox {
  display: none;
}

.toggle-switch {
  position: relative;
  width: 44px;
  height: 24px;
  background: #d1d5db;
  border-radius: 12px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  flex-shrink: 0;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
}

.toggle-switch::after {
  content: '';
  position: absolute;
  top: 2px;
  left: 2px;
  width: 20px;
  height: 20px;
  background: white;
  border-radius: 50%;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.toggle-checkbox:checked + .toggle-switch {
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.15);
}

.toggle-checkbox:checked + .toggle-switch::after {
  transform: translateX(20px);
}

.toggle-text {
  font-size: 0.875rem;
  font-weight: 600;
  color: #374151;
}

.color-input-wrapper {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 0.75rem 1rem;
  background: white;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.color-input-wrapper:hover {
  border-color: var(--primary-color, #667eea);
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.08);
}

.color-input {
  width: 60px;
  height: 44px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  background: transparent;
  transition: transform 0.2s ease;
}

.color-input:hover {
  transform: scale(1.05);
}

.color-input::-webkit-color-swatch-wrapper {
  padding: 0;
}

.color-input::-webkit-color-swatch {
  border: 3px solid #e5e7eb;
  border-radius: 10px;
  transition: border-color 0.3s ease;
}

.color-input:hover::-webkit-color-swatch {
  border-color: var(--primary-color, #667eea);
}

.color-value {
  font-family: 'SF Mono', 'Monaco', 'Inconsolata', 'Fira Code', monospace;
  font-size: 0.9rem;
  color: #374151;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.range-input {
  width: 100%;
  height: 6px;
  border-radius: 6px;
  background: linear-gradient(to right, #e5e7eb 0%, #d1d5db 100%);
  outline: none;
  -webkit-appearance: none;
  appearance: none;
  transition: background 0.3s ease;
}

.range-input:hover {
  background: linear-gradient(to right, #d1d5db 0%, #9ca3af 100%);
}

.range-input::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 22px;
  height: 22px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  cursor: pointer;
  box-shadow: 0 3px 10px rgba(102, 126, 234, 0.4);
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

.range-input::-webkit-slider-thumb:hover {
  transform: scale(1.25);
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.6);
}

.range-input::-moz-range-thumb {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  cursor: pointer;
  border: none;
  box-shadow: 0 3px 10px rgba(102, 126, 234, 0.4);
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}

.range-input::-moz-range-thumb:hover {
  transform: scale(1.25);
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.6);
}

.range-labels {
  display: flex;
  justify-content: space-between;
  margin-top: 0.625rem;
  font-size: 0.75rem;
  color: #9ca3af;
  font-weight: 500;
}

.reset-btn {
  width: 100%;
  padding: 1rem 1.75rem;
  background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
  color: white;
  border: none;
  border-radius: 14px;
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.625rem;
  margin-top: 1.5rem;
  box-shadow: 0 4px 15px rgba(239, 68, 68, 0.3);
  letter-spacing: 0.3px;
}

.reset-btn:hover {
  background: linear-gradient(135deg, #dc2626 0%, #b91c1c 100%);
  transform: translateY(-3px);
  box-shadow: 0 6px 20px rgba(239, 68, 68, 0.4);
}

.reset-btn:active {
  transform: translateY(-1px);
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(4px);
  z-index: 999;
  animation: fadeIn 0.3s ease;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.background-type-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.875rem;
}

.type-btn {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.625rem;
  padding: 1.125rem;
  background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%);
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 0.875rem;
  font-weight: 600;
  color: #374151;
}

.type-btn:hover {
  background: linear-gradient(135deg, #f3f4f6 0%, #e5e7eb 100%);
  border-color: var(--primary-color, #667eea);
  transform: translateY(-3px);
  box-shadow: 0 6px 15px rgba(102, 126, 234, 0.15);
}

.type-btn.active {
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  border-color: transparent;
  color: white;
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}

.type-btn svg {
  width: 24px;
  height: 24px;
}

.upload-wrapper {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.file-input {
  display: none;
}

.upload-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.625rem;
  padding: 1rem 1.5rem;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
}

.upload-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 18px rgba(102, 126, 234, 0.45);
}

.preview-thumbnail {
  width: 100%;
  height: 140px;
  border-radius: 12px;
  overflow: hidden;
  border: 3px solid #e5e7eb;
  transition: border-color 0.3s ease;
}

.preview-thumbnail:hover {
  border-color: var(--primary-color, #667eea);
}

.preview-thumbnail img,
.preview-thumbnail video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.video-preview {
  position: relative;
}

.video-label {
  position: absolute;
  bottom: 0.625rem;
  left: 0.625rem;
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 0.375rem 0.875rem;
  border-radius: 8px;
  font-size: 0.75rem;
  font-weight: 600;
  backdrop-filter: blur(8px);
}

.preview-badge-wrapper {
  display: flex;
  justify-content: center;
  margin-top: 1.25rem;
}

.current-style-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1.5rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 50px;
  font-size: 0.875rem;
  font-weight: 700;
  text-transform: capitalize;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
  letter-spacing: 0.3px;
}

.current-style-badge svg {
  width: 16px;
  height: 16px;
}

.shape-selector-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.75rem;
}

.shape-option {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  padding: 0.875rem 0.5rem;
  background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%);
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.shape-option:hover {
  background: linear-gradient(135deg, #f3f4f6 0%, #e5e7eb 100%);
  border-color: var(--primary-color, #667eea);
  transform: translateY(-3px);
  box-shadow: 0 6px 15px rgba(102, 126, 234, 0.15);
}

.shape-option.active {
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  border-color: transparent;
  box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
}

.shape-option.active .shape-label {
  color: white;
}

.shape-option.active .shape-preview {
  background: rgba(255, 255, 255, 0.25);
  border-color: white;
}

.shape-option.active .shape-inner {
  background: white;
}

.shape-preview {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.1) 0%, rgba(118, 75, 162, 0.1) 100%);
  border: 2px solid var(--primary-color, #667eea);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s ease;
}

.shape-inner {
  width: 30px;
  height: 30px;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  transition: all 0.3s ease;
}

.shape-preview-rounded {
  border-radius: 8px;
}

.shape-preview-rounded .shape-inner {
  border-radius: 4px;
}

.shape-preview-square {
  border-radius: 0;
}

.shape-preview-square .shape-inner {
  border-radius: 0;
}

.shape-preview-circle {
  border-radius: 50%;
}

.shape-preview-circle .shape-inner {
  border-radius: 50%;
}

.shape-preview-hexagon {
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
  border: none;
}

.shape-preview-hexagon .shape-inner {
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
}

.shape-preview-diamond {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  border: none;
}

.shape-preview-diamond .shape-inner {
  clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
}

.shape-preview-pentagon {
  clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%);
  border: none;
}

.shape-preview-pentagon .shape-inner {
  clip-path: polygon(50% 0%, 100% 38%, 82% 100%, 18% 100%, 0% 38%);
}

.shape-preview-octagon {
  clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%);
  border: none;
}

.shape-preview-octagon .shape-inner {
  clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%);
}

.shape-preview-blob {
  clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%);
  border: none;
}

.shape-preview-blob .shape-inner {
  clip-path: polygon(50% 0%, 83% 12%, 100% 43%, 94% 78%, 68% 100%, 32% 100%, 6% 78%, 0% 43%, 17% 12%);
}

.shape-preview-triangle {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
  border: none;
}

.shape-preview-triangle .shape-inner {
  clip-path: polygon(50% 0%, 0% 100%, 100% 100%);
}

.shape-preview-star {
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
  border: none;
}

.shape-preview-star .shape-inner {
  clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
}

.shape-preview-heart {
  clip-path: path('M50,85 C50,85 20,60 20,40 C20,25 30,15 40,15 C45,15 50,20 50,20 C50,20 55,15 60,15 C70,15 80,25 80,40 C80,60 50,85 50,85 Z');
  border: none;
}

.shape-preview-heart .shape-inner {
  clip-path: polygon(50% 20%, 60% 10%, 70% 10%, 80% 20%, 80% 35%, 50% 80%, 20% 35%, 20% 20%, 30% 10%, 40% 10%);
}

.shape-preview-shield {
  clip-path: polygon(50% 0%, 100% 20%, 100% 60%, 50% 100%, 0% 60%, 0% 20%);
  border: none;
}

.shape-preview-shield .shape-inner {
  clip-path: polygon(50% 0%, 100% 20%, 100% 60%, 50% 100%, 0% 60%, 0% 20%);
}

.shape-preview-parallelogram {
  clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%);
  border: none;
}

.shape-preview-parallelogram .shape-inner {
  clip-path: polygon(25% 0%, 100% 0%, 75% 100%, 0% 100%);
}

.shape-preview-trapezoid {
  clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%);
  border: none;
}

.shape-preview-trapezoid .shape-inner {
  clip-path: polygon(20% 0%, 80% 0%, 100% 100%, 0% 100%);
}

.shape-preview-ellipse {
  border-radius: 50%;
  transform: scaleX(1.4);
}

.shape-preview-ellipse .shape-inner {
  border-radius: 50%;
  transform: scaleX(1.4);
}

.shape-preview-squircle {
  border-radius: 35%;
}

.shape-preview-squircle .shape-inner {
  border-radius: 35%;
}

.shape-preview-teardrop {
  clip-path: polygon(50% 0%, 70% 10%, 85% 30%, 90% 50%, 85% 70%, 70% 85%, 50% 100%, 30% 85%, 15% 70%, 10% 50%, 15% 30%, 30% 10%);
  border: none;
  transform: rotate(45deg);
}

.shape-preview-teardrop .shape-inner {
  clip-path: polygon(50% 0%, 70% 10%, 85% 30%, 90% 50%, 85% 70%, 70% 85%, 50% 100%, 30% 85%, 15% 70%, 10% 50%, 15% 30%, 30% 10%);
}

.shape-preview-arch {
  clip-path: path('M 0,100 L 0,50 Q 0,0 50,0 Q 100,0 100,50 L 100,100 Z');
  border: none;
}

.shape-preview-arch .shape-inner {
  clip-path: ellipse(40% 35% at 50% 100%);
}

.shape-preview-cross {
  clip-path: polygon(40% 0%, 60% 0%, 60% 40%, 100% 40%, 100% 60%, 60% 60%, 60% 100%, 40% 100%, 40% 60%, 0% 60%, 0% 40%, 40% 40%);
  border: none;
}

.shape-preview-cross .shape-inner {
  clip-path: polygon(40% 0%, 60% 0%, 60% 40%, 100% 40%, 100% 60%, 60% 60%, 60% 100%, 40% 100%, 40% 60%, 0% 60%, 0% 40%, 40% 40%);
}

.shape-preview-badge {
  clip-path: polygon(50% 0%, 65% 5%, 75% 15%, 85% 25%, 95% 40%, 100% 50%, 95% 60%, 85% 75%, 75% 85%, 65% 95%, 50% 100%, 35% 95%, 25% 85%, 15% 75%, 5% 60%, 0% 50%, 5% 40%, 15% 25%, 25% 15%, 35% 5%);
  border: none;
}

.shape-preview-badge .shape-inner {
  clip-path: polygon(50% 0%, 65% 5%, 75% 15%, 85% 25%, 95% 40%, 100% 50%, 95% 60%, 85% 75%, 75% 85%, 65% 95%, 50% 100%, 35% 95%, 25% 85%, 15% 75%, 5% 60%, 0% 50%, 5% 40%, 15% 25%, 25% 15%, 35% 5%);
}

.shape-preview-ticket {
  clip-path: path('M 5,0 L 95,0 Q 100,0 100,5 L 100,40 Q 97,40 97,45 Q 97,50 100,50 L 100,95 Q 100,100 95,100 L 5,100 Q 0,100 0,95 L 0,50 Q 3,50 3,45 Q 3,40 0,40 L 0,5 Q 0,0 5,0 Z');
  border: none;
}

.shape-preview-ticket .shape-inner {
  clip-path: polygon(10% 10%, 90% 10%, 90% 40%, 85% 45%, 85% 55%, 90% 60%, 90% 90%, 10% 90%, 10% 60%, 15% 55%, 15% 45%, 10% 40%);
}

.shape-preview-chevron {
  clip-path: polygon(0% 0%, 75% 0%, 100% 50%, 75% 100%, 0% 100%, 25% 50%);
  border: none;
}

.shape-preview-chevron .shape-inner {
  clip-path: polygon(0% 0%, 75% 0%, 100% 50%, 75% 100%, 0% 100%, 25% 50%);
}

.shape-preview-arrow {
  clip-path: polygon(0% 30%, 70% 30%, 70% 0%, 100% 50%, 70% 100%, 70% 70%, 0% 70%);
  border: none;
}

.shape-preview-arrow .shape-inner {
  clip-path: polygon(0% 30%, 70% 30%, 70% 0%, 100% 50%, 70% 100%, 70% 70%, 0% 70%);
}

.shape-preview-clover {
  clip-path: polygon(50% 20%, 60% 10%, 65% 5%, 70% 10%, 75% 20%, 85% 20%, 90% 25%, 95% 30%, 90% 40%, 80% 50%, 90% 60%, 95% 70%, 90% 75%, 85% 80%, 75% 80%, 70% 90%, 65% 95%, 60% 90%, 50% 80%, 40% 90%, 35% 95%, 30% 90%, 25% 80%, 15% 80%, 10% 75%, 5% 70%, 10% 60%, 20% 50%, 10% 40%, 5% 30%, 10% 25%, 15% 20%, 25% 20%, 30% 10%, 35% 5%, 40% 10%);
  border: none;
}

.shape-preview-clover .shape-inner {
  clip-path: polygon(50% 20%, 60% 10%, 65% 5%, 70% 10%, 75% 20%, 85% 20%, 90% 25%, 95% 30%, 90% 40%, 80% 50%, 90% 60%, 95% 70%, 90% 75%, 85% 80%, 75% 80%, 70% 90%, 65% 95%, 60% 90%, 50% 80%, 40% 90%, 35% 95%, 30% 90%, 25% 80%, 15% 80%, 10% 75%, 5% 70%, 10% 60%, 20% 50%, 10% 40%, 5% 30%, 10% 25%, 15% 20%, 25% 20%, 30% 10%, 35% 5%, 40% 10%);
}

.shape-label {
  font-size: 0.75rem;
  font-weight: 600;
  color: #374151;
  text-align: center;
  line-height: 1.2;
}

@media (max-width: 768px) {
  .settings-btn {
    top: 1rem;
    right: 1rem;
    padding: 0.75rem 1.5rem;
    font-size: 0.9rem;
  }

  .settings-panel {
    width: 100%;
    right: -100%;
  }

  .panel-content {
    padding: 1.25rem;
  }

  .toggle-grid {
    grid-template-columns: 1fr;
  }

  .background-type-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
</style>
