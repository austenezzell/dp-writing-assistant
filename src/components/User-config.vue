<template>
  <div class="container">
    <header>
      <h1>{{ headline }}</h1>
      <p>{{ description }}</p>
    </header>
    <div class="form">
      <div className="form">
        <p>Select your copywriting use case: {{ copyType }}</p>
        <input type="radio" id="product" value="UX" v-model="copyType" />
        <label for="one">Product</label>
        <input
          type="radio"
          id="marketing"
          value="Marketing"
          v-model="copyType"
        />
        <label for="two">Marketing</label>
        <br />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserConfig",
  props: {
    headline: String,
    description: String,
    copyType: String,
    productContentTypes: Object,
  },
  methods: {
    setCopyCategoryUX() {
      //   return (this.copyCategory = "UX");
      //   console.log("yes");
    },
  },
  mounted() {
    // console.log(this.productContentTypes);
  },
};
</script>
