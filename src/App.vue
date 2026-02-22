<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import CardSlider from './components/CardSlider.vue';
import * as XLSX from 'xlsx';
import {
  Settings,
  X,
  Download,
  Link,
  Table2,
  LayoutGrid,
  Layers,
  Type,
  Star,
  Square,
  RectangleHorizontal,
  Image,
  AlignLeft,
  DollarSign,
  Tag,
  ArrowLeftRight,
  ArrowUpDown,
  Palette,
  Paintbrush,
  Droplets,
  Ban,
  Blend,
  CircleDot,
  ImageIcon,
  Play,
  Upload,
  RotateCcw,
  ChevronDown,
  Boxes,
  Clapperboard,
  CheckCircle2,
  Gauge,
  Move,
  PanelRight,
  ScanLine,
  Wand2,
  Zap,
  Waves,
  Wind,
  Shapes,
  Sparkles,
  Moon,
  LayoutDashboard,
  CornerDownRight,
  Circle,
  Bookmark,
  Slash,
  Layers2,
  BookOpen,
  Minus,
  Bold,
  Crown,
  Clock,
  Camera,
  Newspaper,
  Building2,
  Scissors,
} from 'lucide-vue-next';

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
const showStyleDropdown = ref(false);

const cardStyleGroups = [
  {
    label: 'Full Width Cards',
    options: [
      { value: 'fullwidth-zigzag', label: 'Full Width Zigzag', icon: Zap },
      { value: 'fullwidth-wave', label: 'Full Width Wave', icon: Waves },
      { value: 'fullwidth-curved', label: 'Full Width Curved', icon: Wind },
    ],
  },
  {
    label: 'Block Cards',
    options: [
      { value: 'layered-block', label: 'Layered Block', icon: Layers },
      { value: 'geometric-block', label: 'Geometric Block', icon: Shapes },
      { value: 'curved-block', label: 'Curved Block', icon: Boxes },
    ],
  },
  {
    label: 'Special Effects',
    options: [
      { value: 'glassmorphism', label: 'Glassmorphism', icon: Sparkles },
      { value: 'neumorphism', label: 'Neumorphism', icon: CircleDot },
      { value: 'neon', label: 'Neon', icon: Zap },
      { value: 'gradient', label: 'Gradient', icon: Blend },
      { value: 'shadow', label: 'Shadow', icon: Moon },
    ],
  },
  {
    label: 'Creative Designs',
    options: [
      { value: 'staggered', label: 'Staggered', icon: LayoutDashboard },
      { value: 'wave', label: 'Wave', icon: Waves },
      { value: 'striped', label: 'Striped', icon: AlignLeft },
      { value: 'zigzag', label: 'Zigzag', icon: Zap },
      { value: 'corner', label: 'Corner', icon: CornerDownRight },
      { value: 'circular', label: 'Circular', icon: Circle },
      { value: 'ribbon', label: 'Ribbon', icon: Bookmark },
      { value: 'diagonal', label: 'Diagonal', icon: Slash },
      { value: 'overlap', label: 'Overlap', icon: Layers2 },
      { value: 'sidebar', label: 'Sidebar', icon: PanelRight },
      { value: 'floating', label: 'Floating', icon: Move },
    ],
  },
  {
    label: 'Classic Styles',
    options: [
      { value: 'modern', label: 'Modern', icon: LayoutGrid },
      { value: 'classic', label: 'Classic', icon: BookOpen },
      { value: 'minimal', label: 'Minimal', icon: Minus },
      { value: 'elegant', label: 'Elegant', icon: Star },
      { value: 'bold', label: 'Bold', icon: Bold },
      { value: 'compact', label: 'Compact', icon: Square },
      { value: 'luxury', label: 'Luxury', icon: Crown },
      { value: 'vibrant', label: 'Vibrant', icon: Palette },
    ],
  },
  {
    label: 'Vintage & Modern',
    options: [
      { value: 'retro', label: 'Retro', icon: Clock },
      { value: 'polaroid', label: 'Polaroid', icon: Camera },
      { value: 'magazine', label: 'Magazine', icon: Newspaper },
      { value: 'metro', label: 'Metro', icon: Building2 },
      { value: 'stacked', label: 'Stacked', icon: Layers },
      { value: 'split', label: 'Split', icon: Scissors },
    ],
  },
];

const selectedStyleOption = computed(() => {
  for (const group of cardStyleGroups) {
    const found = group.options.find(o => o.value === currentStyle.value);
    if (found) return found;
  }
  return null;
});

const toggleStyleDropdown = () => {
  showStyleDropdown.value = !showStyleDropdown.value;
};

const pickStyle = (value) => {
  selectCardStyle(value);
  showStyleDropdown.value = false;
};

const closeStyleDropdown = (e) => {
  if (!e.target.closest('.style-dropdown-container')) {
    showStyleDropdown.value = false;
  }
};

onMounted(() => document.addEventListener('click', closeStyleDropdown));
onUnmounted(() => document.removeEventListener('click', closeStyleDropdown));

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
const scrollDirection = ref('left');

// Collapsible section states
const sectionsOpen = ref({
  design: false,
  sections: false,
  typography: false,
  styling: false,
  dimensions: false,
  spacing: false,
  background: false,
  colors: false,
  cardColors: false,
  animation: false,
  dataFetch: true,
  columnMapping: false
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

// Data fetching
const fetchUrl = ref('');
const fetchedData = ref(null);
const isFetching = ref(false);
const tableHeaders = ref([]);
const tableRows = ref([]);
const showDataTable = ref(false);
const selectedRows = ref([]);

// Column mapping
const colTitle = ref('');
const colImage = ref('');
const colDescription = ref('');
const colBadge = ref('');
const colType = ref('');
const colPrice = ref('');

const parseCSV = (text) => {
  const rows = [];
  let row = [], cell = '', inQuotes = false;
  for (let i = 0; i < text.length; i++) {
    const ch = text[i];
    if (ch === '"') {
      if (inQuotes && text[i + 1] === '"') { cell += '"'; i++; }
      else { inQuotes = !inQuotes; }
    } else if (ch === ',' && !inQuotes) {
      row.push(cell.trim()); cell = '';
    } else if ((ch === '\n' || (ch === '\r' && text[i + 1] === '\n')) && !inQuotes) {
      if (ch === '\r') i++;
      row.push(cell.trim()); rows.push(row); row = []; cell = '';
    } else {
      cell += ch;
    }
  }
  if (cell || row.length) { row.push(cell.trim()); rows.push(row); }
  return rows.filter(r => r.some(c => c !== ''));
};

const toGoogleSheetsCsvUrl = (url) => {
  const match = url.match(/spreadsheets\/d\/([a-zA-Z0-9-_]+)/);
  if (!match) return null;
  const id = match[1];
  const gidMatch = url.match(/[#&?]gid=([0-9]+)/);
  const gid = gidMatch ? gidMatch[1] : '0';
  return `https://docs.google.com/spreadsheets/d/${id}/export?format=csv&gid=${gid}`;
};

const applyParsedData = (jsonData) => {
  tableHeaders.value = jsonData[0];
  tableRows.value = jsonData.slice(1);
  fetchedData.value = jsonData;
  showDataTable.value = true;
  const headers = jsonData[0].map(h => String(h));
  const find = (...names) => {
    // First try exact match (case-insensitive)
    const exact = headers.find(h => names.some(n => h.toLowerCase() === n.toLowerCase()));
    if (exact) return exact;
    // Then try includes match
    return headers.find(h => names.some(n => h.toLowerCase().includes(n.toLowerCase()))) || '';
  };
  colTitle.value = find('title', 'name', 'product');
  colImage.value = find('images', 'image', 'img', 'photo', 'picture', 'url');
  colDescription.value = find('description', 'desc', 'detail', 'text');
  colBadge.value = find('selectid', 'select id', 'select_id', 'badge', 'id', 'no', 'number', '#');
  colType.value = find('type', 'category', 'cat', 'tag');
  colPrice.value = find('price', 'cost', 'amount');
  selectedRows.value = jsonData.slice(1).map((_, i) => i);
  sectionsOpen.value.columnMapping = true;
};

const fetchData = async () => {
  if (!fetchUrl.value.trim()) {
    alert('Please enter a URL');
    return;
  }

  isFetching.value = true;
  try {
    const raw = fetchUrl.value.trim();
    const isGoogleSheets = raw.includes('docs.google.com/spreadsheets');

    if (isGoogleSheets) {
      const csvUrl = toGoogleSheetsCsvUrl(raw);
      if (!csvUrl) throw new Error('Could not parse Google Sheets URL. Make sure the link is shared publicly.');
      const response = await fetch(csvUrl);
      if (!response.ok) throw new Error(`Failed to fetch sheet (${response.status}). Make sure the sheet is shared as "Anyone with the link can view".`);
      const text = await response.text();
      const jsonData = parseCSV(text);
      if (jsonData.length > 0) {
        applyParsedData(jsonData);
        alert('Data fetched successfully!');
      } else {
        alert('No data found in spreadsheet.');
      }
    } else if (raw.endsWith('.csv')) {
      const response = await fetch(raw);
      if (!response.ok) throw new Error(`Failed to fetch: ${response.status}`);
      const text = await response.text();
      const jsonData = parseCSV(text);
      if (jsonData.length > 0) {
        applyParsedData(jsonData);
        alert('Data fetched successfully!');
      } else {
        alert('No data found in CSV file.');
      }
    } else {
      const response = await fetch(raw);
      if (!response.ok) throw new Error(`Failed to fetch: ${response.status}`);
      const arrayBuffer = await response.arrayBuffer();
      const workbook = XLSX.read(arrayBuffer, { type: 'array' });
      const worksheet = workbook.Sheets[workbook.SheetNames[0]];
      const jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1 });
      if (jsonData.length > 0) {
        applyParsedData(jsonData);
        alert('Data fetched successfully!');
      } else {
        alert('No data found in Excel file.');
      }
    }
  } catch (error) {
    alert('Error: ' + error.message);
    console.error('Fetch error:', error);
  } finally {
    isFetching.value = false;
  }
};

const toggleRowSelection = (rowIndex) => {
  const index = selectedRows.value.indexOf(rowIndex);
  if (index > -1) {
    selectedRows.value.splice(index, 1);
  } else {
    selectedRows.value.push(rowIndex);
  }
};

const isRowSelected = (rowIndex) => {
  return selectedRows.value.includes(rowIndex);
};

const hasSelectedRows = computed(() => {
  return selectedRows.value.length > 0;
});

const mappedCardItems = computed(() => {
  if (!hasSelectedRows.value || !tableHeaders.value.length) return null;
  const headers = tableHeaders.value.map(h => String(h));
  const idx = col => headers.indexOf(col);
  return selectedRows.value.map((rowIndex, i) => {
    const row = tableRows.value[rowIndex];
    if (!row) return null;
    return {
      id: i + 1,
      title: colTitle.value ? row[idx(colTitle.value)] ?? '' : '',
      image: colImage.value ? row[idx(colImage.value)] ?? '' : '',
      description: colDescription.value ? row[idx(colDescription.value)] ?? '' : '',
      category: colType.value ? row[idx(colType.value)] ?? '' : '',
      price: colPrice.value ? row[idx(colPrice.value)] ?? '' : '',
      badge: colBadge.value ? row[idx(colBadge.value)] ?? '' : i + 1,
    };
  }).filter(Boolean);
});

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
  scrollDirection.value = 'left';
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
    <!-- Data Table on Left Side -->
    <div v-if="showDataTable" class="data-table-container">
      <div class="data-table-header">
        <h3 class="data-table-title">Fetched Excel Data</h3>
        <button class="close-table-btn" @click="showDataTable = false" title="Close table">
          <X :size="20" />
        </button>
      </div>
      <div class="data-table-wrapper">
        <table class="data-table">
          <thead>
            <tr>
              <th class="checkbox-column">Select</th>
              <th v-for="(header, index) in tableHeaders" :key="index">{{ header }}</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(row, rowIndex) in tableRows" :key="rowIndex" :class="{ 'selected-row': isRowSelected(rowIndex) }">
              <td class="checkbox-column">
                <input
                  type="checkbox"
                  :checked="isRowSelected(rowIndex)"
                  @change="toggleRowSelection(rowIndex)"
                  class="row-checkbox"
                />
              </td>
              <td v-for="(cell, cellIndex) in row" :key="cellIndex">{{ cell }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <main class="app-main" :class="{ 'with-table': showDataTable && hasSelectedRows }">
      <CardSlider
        v-if="!showDataTable || hasSelectedRows"
        :items="mappedCardItems"
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
        :scroll-direction="scrollDirection"
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
      <Settings :size="20" />
      <span>Settings</span>
    </button>

    <!-- Right Side Panel -->
    <div :class="['settings-panel', { open: isPanelOpen }]">
      <div class="panel-header">
        <div class="header-content">
          <Settings :size="24" />
          <h2 class="panel-title">Customize Cards</h2>
        </div>
        <button class="close-btn" @click="togglePanel" title="Close settings">
          <X :size="24" />
        </button>
      </div>

      <div class="panel-content">
        <!-- Data Fetching Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('dataFetch')">
            <div class="section-header-left">
              <Download :size="20" />
              <h3 class="section-title">Fetch Excel Data</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.dataFetch }]" />
          </button>

          <div v-show="sectionsOpen.dataFetch" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <Link :size="16" />
                Public Excel File URL
              </label>
              <input
                type="text"
                v-model="fetchUrl"
                placeholder="https://example.com/file.xlsx"
                class="text-input"
                :disabled="isFetching"
              />
            </div>

            <button class="fetch-btn" @click="fetchData" :disabled="isFetching">
              <Download v-if="!isFetching" :size="18" />
              <RotateCcw v-else :size="18" class="spinner" />
              {{ isFetching ? 'Fetching...' : 'Fetch Excel Data' }}
            </button>
          </div>
        </div>

        <!-- Column Mapping Section -->
        <div v-if="showDataTable && tableHeaders.length" class="collapsible-section">
          <button class="section-header" @click="toggleSection('columnMapping')">
            <div class="section-header-left">
              <Table2 :size="20" />
              <h3 class="section-title">Column Mapping</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.columnMapping }]" />
          </button>

          <div v-show="sectionsOpen.columnMapping" class="section-content">
            <p class="section-description">Map your Excel columns to each card field. Auto-detected from your headers.</p>

            <div class="form-group">
              <label class="form-label">ID / Badge Column</label>
              <div class="dropdown-wrapper">
                <select v-model="colBadge" class="dropdown-select">
                  <option value="">— None —</option>
                  <option v-for="h in tableHeaders" :key="h" :value="h">{{ h }}</option>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Image URL Column</label>
              <div class="dropdown-wrapper">
                <select v-model="colImage" class="dropdown-select">
                  <option value="">— None —</option>
                  <option v-for="h in tableHeaders" :key="h" :value="h">{{ h }}</option>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Title Column</label>
              <div class="dropdown-wrapper">
                <select v-model="colTitle" class="dropdown-select">
                  <option value="">— None —</option>
                  <option v-for="h in tableHeaders" :key="h" :value="h">{{ h }}</option>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Description Column</label>
              <div class="dropdown-wrapper">
                <select v-model="colDescription" class="dropdown-select">
                  <option value="">— None —</option>
                  <option v-for="h in tableHeaders" :key="h" :value="h">{{ h }}</option>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Category / Type Column</label>
              <div class="dropdown-wrapper">
                <select v-model="colType" class="dropdown-select">
                  <option value="">— None —</option>
                  <option v-for="h in tableHeaders" :key="h" :value="h">{{ h }}</option>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">Price Column</label>
              <div class="dropdown-wrapper">
                <select v-model="colPrice" class="dropdown-select">
                  <option value="">— None —</option>
                  <option v-for="h in tableHeaders" :key="h" :value="h">{{ h }}</option>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
              </div>
            </div>

            <div class="mapping-summary">
              <div class="mapping-chip" :class="{ mapped: colBadge }">
                <span class="chip-field">ID</span>
                <span class="chip-arrow">→</span>
                <span class="chip-col">{{ colBadge || 'not set' }}</span>
              </div>
              <div class="mapping-chip" :class="{ mapped: colImage }">
                <span class="chip-field">Image</span>
                <span class="chip-arrow">→</span>
                <span class="chip-col">{{ colImage || 'not set' }}</span>
              </div>
              <div class="mapping-chip" :class="{ mapped: colTitle }">
                <span class="chip-field">Title</span>
                <span class="chip-arrow">→</span>
                <span class="chip-col">{{ colTitle || 'not set' }}</span>
              </div>
              <div class="mapping-chip" :class="{ mapped: colDescription }">
                <span class="chip-field">Description</span>
                <span class="chip-arrow">→</span>
                <span class="chip-col">{{ colDescription || 'not set' }}</span>
              </div>
              <div class="mapping-chip" :class="{ mapped: colType }">
                <span class="chip-field">Category</span>
                <span class="chip-arrow">→</span>
                <span class="chip-col">{{ colType || 'not set' }}</span>
              </div>
              <div class="mapping-chip" :class="{ mapped: colPrice }">
                <span class="chip-field">Price</span>
                <span class="chip-arrow">→</span>
                <span class="chip-col">{{ colPrice || 'not set' }}</span>
              </div>
            </div>
          </div>
        </div>

        <!-- Design Section -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('design')">
            <div class="section-header-left">
              <LayoutGrid :size="20" />
              <h3 class="section-title">Card Design</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.design }]" />
          </button>
          
          <div v-show="sectionsOpen.design" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <Layers :size="16" />
                Card Style
              </label>
              <div class="style-dropdown-container">
                <button type="button" class="style-dropdown-trigger" @click.stop="toggleStyleDropdown">
                  <span class="style-dropdown-selected">
                    <component :is="selectedStyleOption?.icon" :size="15" class="style-option-icon" />
                    <span>{{ selectedStyleOption?.label }}</span>
                  </span>
                  <ChevronDown :size="15" :class="['style-dropdown-chevron', { rotated: showStyleDropdown }]" />
                </button>
                <div v-show="showStyleDropdown" class="style-dropdown-panel">
                  <div v-for="group in cardStyleGroups" :key="group.label" class="style-dropdown-group">
                    <div class="style-group-label">{{ group.label }}</div>
                    <button
                      v-for="option in group.options"
                      :key="option.value"
                      type="button"
                      :class="['style-dropdown-option', { active: currentStyle === option.value }]"
                      @click="pickStyle(option.value)"
                    >
                      <component :is="option.icon" :size="14" class="style-option-icon" />
                      <span>{{ option.label }}</span>
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <div class="form-group">
              <label class="form-label">
                <ImageIcon :size="16" />
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
                <CheckCircle2 :size="16" />
                {{ currentStyle }}
              </div>
            </div>
          </div>
        </div>

        <!-- Card Sections -->
        <div class="collapsible-section">
          <button class="section-header" @click="toggleSection('sections')">
            <div class="section-header-left">
              <ScanLine :size="20" />
              <h3 class="section-title">Visible Sections</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.sections }]" />
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
              <Type :size="20" />
              <h3 class="section-title">Typography</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.typography }]" />
          </button>
          
          <div v-show="sectionsOpen.typography" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <Type :size="16" />
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
                <AlignLeft :size="16" />
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
                <DollarSign :size="16" />
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
                <Tag :size="16" />
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
              <Wand2 :size="20" />
              <h3 class="section-title">Card Styling</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.styling }]" />
          </button>
          
          <div v-show="sectionsOpen.styling" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <Square :size="16" />
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
                <Move :size="16" />
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
                <Image :size="16" />
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
                <AlignLeft :size="16" />
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
              <RectangleHorizontal :size="20" />
              <h3 class="section-title">Card Dimensions</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.dimensions }]" />
          </button>
          
          <div v-show="sectionsOpen.dimensions" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <ArrowLeftRight :size="16" />
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
                <ArrowUpDown :size="16" />
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
              <Move :size="20" />
              <h3 class="section-title">Spacing</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.spacing }]" />
          </button>
          
          <div v-show="sectionsOpen.spacing" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <LayoutGrid :size="16" />
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
                <Square :size="16" />
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
              <PanelRight :size="20" />
              <h3 class="section-title">Background</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.background }]" />
          </button>
          
          <div v-show="sectionsOpen.background" class="section-content">
            <div class="form-group">
              <label class="form-label">Background Type</label>
              <div class="background-type-grid">
                <button :class="['type-btn', { active: backgroundType === 'none' }]" @click="selectBackgroundType('none')">
                  <Ban :size="20" />
                  None
                </button>
                <button :class="['type-btn', { active: backgroundType === 'gradient' }]" @click="selectBackgroundType('gradient')">
                  <Blend :size="20" />
                  Gradient
                </button>
                <button :class="['type-btn', { active: backgroundType === 'color' }]" @click="selectBackgroundType('color')">
                  <CircleDot :size="20" />
                  Color
                </button>
                <button :class="['type-btn', { active: backgroundType === 'image' }]" @click="selectBackgroundType('image')">
                  <ImageIcon :size="20" />
                  Image
                </button>
                <button :class="['type-btn', { active: backgroundType === 'video' }]" @click="selectBackgroundType('video')">
                  <Play :size="20" />
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
                <ChevronDown :size="16" class="dropdown-icon" />
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
                  <Upload :size="20" />
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
                  <Upload :size="20" />
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
              <Droplets :size="20" />
              <h3 class="section-title">Theme Colors</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.colors }]" />
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
              <Paintbrush :size="20" />
              <h3 class="section-title">{{ currentStyle }} Colors</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.cardColors }]" />
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
              <Clapperboard :size="20" />
              <h3 class="section-title">Animation</h3>
            </div>
            <ChevronDown :size="20" :class="['chevron-icon', { rotated: sectionsOpen.animation }]" />
          </button>
          
          <div v-show="sectionsOpen.animation" class="section-content">
            <div class="form-group">
              <label class="form-label">
                <Play :size="16" />
                Entrance Animation
              </label>
              <div class="dropdown-wrapper enhanced-dropdown">
                <select v-model="entranceAnimation" class="dropdown-select styled-select">
                  <option value="none">None</option>
                  <optgroup label="Flip Animations">
                    <option value="flip-top">Flip From Top</option>
                    <option value="flip-bottom">Flip From Bottom</option>
                    <option value="3d-flip">3D Flip</option>
                  </optgroup>
                  <optgroup label="Slide Animations">
                    <option value="slide-left">Slide From Left</option>
                    <option value="slide-right">Slide From Right</option>
                    <option value="slide-up">Slide Up</option>
                    <option value="slide-down">Slide Down</option>
                  </optgroup>
                  <optgroup label="Zoom & Rotate">
                    <option value="zoom-in">Zoom In</option>
                    <option value="rotate-in">Rotate In</option>
                    <option value="spiral-in">Spiral In</option>
                    <option value="tornado">Tornado Spin</option>
                  </optgroup>
                  <optgroup label="Bounce & Swing">
                    <option value="bounce-in">Bounce In</option>
                    <option value="elastic-bounce">Elastic Bounce</option>
                    <option value="swing-in">Swing In</option>
                  </optgroup>
                  <optgroup label="Special Effects">
                    <option value="fade-in">Fade In Sequence</option>
                    <option value="cascade">Cascade Fall</option>
                    <option value="wave-in">Wave In</option>
                    <option value="fold-unfold">Fold & Unfold</option>
                    <option value="glitch">Glitch Effect</option>
                  </optgroup>
                </select>
                <ChevronDown :size="16" class="dropdown-icon" />
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
              <label class="form-label">
                <ArrowLeftRight :size="16" />
                Scroll Direction
              </label>
              <div class="scroll-direction-grid">
                <button :class="['direction-btn', { active: scrollDirection === 'left' }]" @click="scrollDirection = 'left'">
                  <ArrowLeftRight :size="18" style="transform: scaleX(-1)" />
                  Left
                </button>
                <button :class="['direction-btn', { active: scrollDirection === 'right' }]" @click="scrollDirection = 'right'">
                  <ArrowLeftRight :size="18" />
                  Right
                </button>
                <button :class="['direction-btn', { active: scrollDirection === 'both' }]" @click="scrollDirection = 'both'">
                  <ArrowUpDown :size="18" style="transform: rotate(90deg)" />
                  Both
                </button>
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
        <button class="reset-btn" @click="resetSettings" style="margin-top: 1.5rem">
          <RotateCcw :size="18" />
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
  display: flex;
}

.data-table-container {
  position: fixed;
  left: 0;
  top: 0;
  bottom: 0;
  width: 100%;
  background: white;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  z-index: 50;
  overflow: hidden;
}

.data-table-header {
  padding: 1.5rem;
  border-bottom: 2px solid #e5e7eb;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
}

.data-table-title {
  margin: 0;
  font-size: 1.25rem;
  font-weight: 600;
  color: white;
}

.close-table-btn {
  background: rgba(255, 255, 255, 0.2);
  border: none;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  color: white;
}

.close-table-btn:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: scale(1.1);
}

.data-table-wrapper {
  flex: 1;
  overflow: auto;
  padding: 1rem;
}

.data-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.875rem;
}

.data-table thead {
  position: sticky;
  top: 0;
  background: #f9fafb;
  z-index: 10;
}

.data-table th {
  padding: 0.75rem;
  text-align: left;
  font-weight: 600;
  color: #374151;
  border-bottom: 2px solid #e5e7eb;
  white-space: nowrap;
}

.data-table td {
  padding: 0.75rem;
  border-bottom: 1px solid #e5e7eb;
  color: #6b7280;
}

.data-table tbody tr:hover {
  background: #f9fafb;
}

.checkbox-column {
  width: 60px;
  text-align: center;
}

.row-checkbox {
  width: 18px;
  height: 18px;
  cursor: pointer;
  accent-color: var(--primary-color, #667eea);
}

.selected-row {
  background: rgba(102, 126, 234, 0.1);
}

.selected-row:hover {
  background: rgba(102, 126, 234, 0.15);
}

.app-main {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  padding: 2rem 0;
  flex: 1;
  transition: margin-left 0.3s ease;
}

.app-main.with-table {
  margin-left: 400px;
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

.style-dropdown-container {
  position: relative;
}

.style-dropdown-trigger {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0.875rem 1.125rem;
  font-size: 0.95rem;
  font-weight: 500;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  background: white;
  color: #1f2937;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  text-align: left;
}

.style-dropdown-trigger:hover {
  border-color: var(--primary-color, #667eea);
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.08);
}

.style-dropdown-selected {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.style-dropdown-chevron {
  color: #9ca3af;
  transition: transform 0.25s ease, color 0.25s ease;
  flex-shrink: 0;
}

.style-dropdown-chevron.rotated {
  transform: rotate(180deg);
}

.style-dropdown-trigger:hover .style-dropdown-chevron {
  color: var(--primary-color, #667eea);
}

.style-dropdown-panel {
  position: absolute;
  top: calc(100% + 6px);
  left: 0;
  right: 0;
  background: white;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  z-index: 200;
  max-height: 300px;
  overflow-y: auto;
  padding: 0.375rem;
}

.style-dropdown-group {
  margin-bottom: 0.25rem;
}

.style-group-label {
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: #9ca3af;
  padding: 0.45rem 0.625rem 0.25rem;
}

.style-dropdown-option {
  width: 100%;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 0.625rem;
  font-size: 0.88rem;
  font-weight: 500;
  color: #374151;
  background: transparent;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.15s ease, color 0.15s ease;
  text-align: left;
}

.style-dropdown-option:hover {
  background: #f3f4f6;
  color: #111827;
}

.style-dropdown-option.active {
  background: rgba(102, 126, 234, 0.1);
  color: var(--primary-color, #667eea);
}

.style-option-icon {
  flex-shrink: 0;
  opacity: 0.75;
}

.style-dropdown-option.active .style-option-icon {
  opacity: 1;
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
  z-index: 1;
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

.text-input {
  width: 100%;
  padding: 0.875rem 1rem;
  background: white;
  border: 2px solid #e5e7eb;
  border-radius: 12px;
  font-size: 0.95rem;
  color: #374151;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  outline: none;
  font-family: inherit;
}

.text-input:focus {
  border-color: var(--primary-color, #667eea);
  box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
}

.text-input:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  background: #f9fafb;
}

.text-input::placeholder {
  color: #9ca3af;
}

.fetch-btn {
  width: 100%;
  padding: 0.875rem 1.5rem;
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
  color: white;
  border: none;
  border-radius: 12px;
  font-size: 0.95rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 0.75rem;
  box-shadow: 0 4px 12px rgba(16, 185, 129, 0.25);
}

.fetch-btn:hover:not(:disabled) {
  background: linear-gradient(135deg, #059669 0%, #047857 100%);
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(16, 185, 129, 0.35);
}

.fetch-btn:active:not(:disabled) {
  transform: translateY(0);
}

.fetch-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.fetch-btn .spinner {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
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

.mapping-summary {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  margin-top: 1.25rem;
  padding: 1rem;
  background: linear-gradient(135deg, #f9fafb 0%, #f3f4f6 100%);
  border-radius: 12px;
  border: 1px solid #e5e7eb;
}

.mapping-chip {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 0.75rem;
  border-radius: 8px;
  background: white;
  border: 1.5px solid #e5e7eb;
  font-size: 0.8rem;
  transition: all 0.2s ease;
}

.mapping-chip.mapped {
  border-color: var(--primary-color, #667eea);
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.05) 0%, rgba(118, 75, 162, 0.05) 100%);
}

.chip-field {
  font-weight: 700;
  color: #374151;
  min-width: 72px;
}

.chip-arrow {
  color: #9ca3af;
  font-weight: 600;
}

.chip-col {
  color: var(--primary-color, #667eea);
  font-weight: 600;
  font-family: 'SF Mono', 'Monaco', 'Inconsolata', monospace;
  font-size: 0.78rem;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.mapping-chip:not(.mapped) .chip-col {
  color: #9ca3af;
  font-style: italic;
}

.scroll-direction-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 0.75rem;
}

.direction-btn {
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
  font-size: 0.8rem;
  font-weight: 600;
  color: #374151;
}

.direction-btn:hover {
  background: linear-gradient(135deg, #f3f4f6 0%, #e5e7eb 100%);
  border-color: var(--primary-color, #667eea);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.15);
}

.direction-btn.active {
  background: linear-gradient(135deg, var(--primary-color, #667eea) 0%, var(--secondary-color, #764ba2) 100%);
  border-color: transparent;
  color: white;
  box-shadow: 0 4px 15px rgba(102, 126, 234, 0.4);
}

.direction-btn svg {
  width: 18px;
  height: 18px;
}
</style>
