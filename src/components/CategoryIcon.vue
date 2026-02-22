<script setup>
import {
  Mountain,
  Trees,
  Coffee,
  Flame,
  Bike,
  Sailboat,
  Fish,
  Tag,
  Compass,
  TreePine,
  Building,
  UtensilsCrossed,
  HeartPulse,
  Trophy,
  BookOpen,
  Anchor,
  Umbrella,
  CloudSnow,
  Sunset,
  GlassWater,
  ShoppingCart,
  Aperture,
  Headphones,
  Paintbrush,
  Scroll,
  Backpack,
  MapPin,
  Tent,
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
  travel: Compass,
  nature: TreePine,
  city: Building,
  food: UtensilsCrossed,
  wellness: HeartPulse,
  adventure: Mountain,
  sports: Trophy,
  culture: BookOpen,
  ocean: Anchor,
  beach: Umbrella,
  forest: Trees,
  winter: CloudSnow,
  summer: Sunset,
  coffee: Coffee,
  wine: GlassWater,
  cooking: Flame,
  shopping: ShoppingCart,
  cycling: Bike,
  sailing: Sailboat,
  photography: Aperture,
  music: Headphones,
  art: Paintbrush,
  history: Scroll,
  hiking: Backpack,
  fishing: Fish,
  camping: Tent,
  map: MapPin,
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
