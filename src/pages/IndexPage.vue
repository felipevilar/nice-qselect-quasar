<template>
  <q-page class="row items-center justify-evenly">
    <q-card>
      <q-card-section>
        <reusable-selector
          :options="collection"
          v-model="selectedOption"
          square
          outlined
          options-dense
          style="width: 500px"
        />
      </q-card-section>
      <filter-banner label="Heroes" v-model="selectedOption" />
    </q-card>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import ReusableSelector from 'src/components/ReusableSelector.vue';
import FilterBanner from 'src/components/FilterBanner.vue';

export default defineComponent({
  name: 'IndexPage',
  components: { ReusableSelector, FilterBanner },
  setup() {
    const collection = ref<string[]>([
      'Son Goku',
      'Bulma',
      'Krillin',
      'Piccolo',
      'Son Gohan',
      'Vegeta',
      'Bardock',
      'Trunks',
      'Master Roshi',
      'Yamcha',
      'Tien Shinhan',
      'Chiaotzu',
      'Android 18',
      'Son Goten',
      'Beerus',
      'Whis',
      'Pilaf Gang',
      'Red Ribbon Army',
      'King Piccolo',
      'Garlic Jr.',
      'Frieza',
      'Cell',
      'Broly',
      'Majin Buu',
      'Sample of a big chip label that is too long to fit in the chip',
    ]);
    const selectedOption = ref();
    return { collection, selectedOption };
  },
});
</script>
