<template>
  <div class="text-black text-3xl mt-10 mb-6">{{ comment }}</div>
</template>

<script>
export default {
  name: "Loading",
  data() {
    return {
      posts: [
        "Wear mask at all times",
        "Get Vaccinated at the earliest",
        "Go out, only if neccessary",
        "Mantain Social distancing",
      ],
    };
  },
  computed: {
    comment: function () {
      const item = this.posts[(this.posts.length * Math.random()) | 0];
      console.log(this.posts[(this.posts.length * Math.random()) | 0]);
      return item;
    },
  },
};
</script>