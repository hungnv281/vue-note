<template>
  <input type="text" v-model="search" />
  <p v-if="noResults">Sorry, no results for {{ search }}</p>
  <div v-for="(r, i) in results" :key="i">
    {{ r }}
  </div>
</template>

<script>
import { useVueFuse } from "vue-fuse";

export default {
  name: "SearchCpn",
  onMounted() {
    // const myList = ["aaaa", "bbbb", "cccc", "abc", "xyz"];
    const { search, results, noResults } = useVueFuse(this.listNote);

    return {
      search,
      results,
      noResults,
    };
  },
  props: {
    listNotes: Array,
  }
};
</script>