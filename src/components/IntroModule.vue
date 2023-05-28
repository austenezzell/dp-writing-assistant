<template>
  <div class="intro">
    <img alt="peace logo" src="../assets/color_peace.svg" />
    <p>{{ headline }}</p>
  </div>
</template>

<script>
export default {
  name: "IntroModule",
  props: {
    headline: String,
  },
};
</script>
