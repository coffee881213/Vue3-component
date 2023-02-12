<template>
  <div>
    <div v-for="(item, index) in list" :key="index" :style="{ background: item.background, width: '100%', height: '500px' }">
      {{index}}
    </div>
    <div v-if="loading" style="width: 100%; height: 500px;">Loading...</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [],
      loading: false,
      numOfDivs: 0
    };
  },
  methods: {
    getList(num) {
      this.loading = true;
      const delay = Math.random() * 5000;
      setTimeout(() => {
        // generate an array of random colors
		const color1 = [{ background: 'rgb(233,32,38)' }];
        const colors_add = Array.from(Array(num-1), () => {
          const r = Math.floor(Math.random() * 256);
          const g = Math.floor(Math.random() * 256);
          const b = Math.floor(Math.random() * 256);
          return { background: `rgb(${r}, ${g}, ${b})` };
        });
        // add the new colors to the existing list
        const colors = [...color1, ...colors_add];
		
        this.list = [...this.list, ...colors];
		this.numOfDivs += 10;
        this.loading = false;
      }, delay);
    }
  },
  created() {
    this.getList(10);
  },
  mounted() {
    window.addEventListener('scroll', () => {
      if (this.numOfDivs < 50 && window.scrollY > window.innerHeight * 0.5) {
        this.getList(10);
      }
    });
  }
};
</script>

<style>

</style>