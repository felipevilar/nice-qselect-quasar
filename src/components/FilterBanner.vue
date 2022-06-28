<template>
  <div
    class="colum q-pa-md"
    v-if="arr.length"
    :class="$q.dark.isActive ? 'bg-grey-10' : 'bg-grey-2'"
  >
    <p
      :class="$q.dark.isActive ? 'white' : 'text-grey-8'"
      style="display: inline"
    >
      {{ label }}
    </p>
    <div
      class="q-gutter-sm q-mt-sm"
      style="max-width: 250px"
      :class="{ 'truncate-chip-labels': truncate }"
    >
      <q-chip
        class="q-pa-xs"
        v-for="(item, index) in arr"
        :key="index"
        square
        removable
        @remove="arr.splice(index, 1)"
        :label="item"
        :color="$q.dark.isActive ? 'blue-grey-6' : 'blue-2'"
        :text-color="$q.dark.isActive ? 'white' : 'blue-9'"
      >
      </q-chip>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, PropType } from 'vue';

export default defineComponent({
  name: 'BannerComponent',
  props: {
    label: {
      type: String,
      default: 'Selected items',
    },
    modelValue: {
      type: Array as PropType<string[]>,
      require: true,
      default: () => [],
    },
  },
  setup(props) {
    const truncate = ref(true);
    const arr = computed(() => props.modelValue);

    return {
      arr,
      truncate,
    };
  },
});
</script>
