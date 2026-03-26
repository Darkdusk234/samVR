<template>
  <a-entity 
    :position="arrToCoordString(props.placedObject.position)"
    :rotation="arrToCoordString(quaternionTupleToAframeRotation(props.placedObject.orientation ?? [0,0,0,1]))"
    :scale="arrToCoordString(props.placedObject.scale ?? [1,1,1])"
    class="selectable-object editable-object"
    @click.stop="$emit('select', props.placedObject)"
  >
    <a-troika-text
      :value="props.placedObject.text"
      :color="props.placedObject.color ?? '#000000'"
      :font-size="props.placedObject.fontSize ?? 0.5"
      :outline-color="props.placedObject.outlineColor ?? '#ffffff'"
      :outline-width="props.placedObject.outlineWidth ?? 0.02"
    />
  </a-entity>
</template>

<script setup lang="ts">
const props = withDefaults(defineProps<{
  placedObject: PlacedObjectWithIncludes
}>(), {})

defineEmits<{
  select: [PlacedObjectWithIncludes]
}>()

import { arrToCoordString, quaternionTupleToAframeRotation } from '@/modules/3DUtils'
import type { PlacedObjectWithIncludes } from 'database'
</script>