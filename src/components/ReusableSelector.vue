<template>
  <q-select
    v-bind="$attrs"
    ref="refSelect"
    :label="label"
    :options="collection"
    multiple
    transition-show="jump-down"
    transition-hide="jump-up"
    @filter="filterFn"
    v-model="selection"
    use-input
  >
    <template #prepend>
      <q-icon name="settings" />
    </template>

    <template #option="scope">
      <q-item v-bind="scope.itemProps" data-cy="generic-options">
        <q-item-section avatar>
          <q-checkbox
            v-model="selection"
            :val="scope.opt"
            color="green"
          ></q-checkbox>
        </q-item-section>
        <q-item-section>
          <q-item-label class="overflow" style="max-width: 325px">
            {{ scope.opt }}
          </q-item-label>
        </q-item-section>
      </q-item>
    </template>

    <template #no-option>
      <q-item>
        <q-item-section class="text-italic text-grey">
          <q-item-label>
            {{ notFound }}
          </q-item-label>
        </q-item-section>
      </q-item>
    </template>

    <template #selected-item="scope">
      <q-chip
        removable
        square
        @remove="scope.removeAtIndex(scope.index)"
        :color="$q.dark.isActive ? 'grey-8' : color"
        text-color="white"
        style="font-size: 12px; max-width: 200px"
      >
        <q-item-label class="overflow">{{ scope.opt }}</q-item-label>
      </q-chip>
    </template>
  </q-select>
</template>

<script lang="ts">
import { QSelect } from 'quasar';
import { defineComponent, ref, PropType, computed } from 'vue';

type FilterUpdateFn = { (fn: () => void): void };

export default defineComponent({
  name: 'TypeSelect',
  props: {
    options: {
      type: Array as PropType<string[]> | undefined,
      required: true,
      default: () => [],
    },
    label: {
      type: String,
      default: 'Select an option...',
    },
    modelValue: {
      type: Array as PropType<string[]>,
      default: () => [],
    },
    color: {
      type: String,
      default: 'primary',
    },
  },
  emits: ['update:modelValue'],
  setup(props, { emit }) {
    const collection = ref<string[]>(props.options);
    const notFound = 'Sorry, no options were found';
    const refSelect = ref<QSelect>();
    const selection = computed({
      get: () => props.modelValue,
      set: (val) => emit('update:modelValue', val),
    });

    const filterFn = (val: string, update: FilterUpdateFn) => {
      if (val === '') {
        update(() => {
          collection.value = props.options;
        });
      } else {
        update(() => {
          const needle = val.toLowerCase();
          collection.value = props.options?.filter(
            (v) => v.toLowerCase().indexOf(needle) > -1
          );
        });
      }
    };

    return {
      refSelect,
      collection,
      selection,
      notFound,
      filterFn,
    };
  },
});
</script>

<style lang="sass" scoped>
.overflow
  overflow: hidden
  text-overflow: ellipsis
  white-space: nowrap
  display: block
</style>
