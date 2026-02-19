<script setup>
import {
  Mountain,
  Waves,
  Building2,
  Trees,
  Sun,
  Snowflake,
  Palmtree,
  Star,
  Utensils,
  Coffee,
  Wine,
  ChefHat,
  ShoppingBag,
  Dumbbell,
  Bike,
  Sailboat,
  Camera,
  Music,
  Palette,
  Landmark,
  Heart,
  Leaf,
  Globe,
  Plane,
  Tent,
  Fish,
  Flame,
  Map,
  Tag,
} from 'lucide-vue-next';

const props = defineProps({
  category: {
    type: String,
    default: ''
  },
  size: {
    type: Number,
    default: 16
  }
});

const categoryIconMap = {
  travel: Plane,
  nature: Leaf,
  city: Building2,
  food: Utensils,
  wellness: Heart,
  adventure: Mountain,
  sports: Dumbbell,
  culture: Landmark,
  ocean: Waves,
  beach: Palmtree,
  forest: Trees,
  winter: Snowflake,
  summer: Sun,
  coffee: Coffee,
  wine: Wine,
  cooking: ChefHat,
  shopping: ShoppingBag,
  cycling: Bike,
  sailing: Sailboat,
  photography: Camera,
  music: Music,
  art: Palette,
  history: Landmark,
  hiking: Tent,
  fishing: Fish,
  camping: Flame,
  map: Map,
};

const resolveIcon = (category) => {
  if (!category) return Tag;
  const key = category.toLowerCase().trim();
  if (categoryIconMap[key]) return categoryIconMap[key];
  // fuzzy match: check if any key is contained in the category
  for (const [k, icon] of Object.entries(categoryIconMap)) {
    if (key.includes(k) || k.includes(key)) return icon;
  }
  return Tag;
};

import { computed } from 'vue';
const icon = computed(() => resolveIcon(props.category));
</script>

<template>
  <component :is="icon" :size="size" />
</template>
