<template>
  <div class="container">
    <div class="col">
      <div>
        <header>
          <h1>{{ title }}</h1>
          <p>{{ description }}</p>
        </header>
        <div>
          <p>Select your copywriting use case:</p>
        </div>
        <input
          type="radio"
          id="product-copy"
          value="UX"
          v-model="ask.copyType"
        />
        <label for="product-copy">Product</label>
        <input
          type="radio"
          id="marketing-copy"
          value="Marketing"
          v-model="ask.copyType"
        />
        <label for="marketing-copy">Marketing</label>
      </div>
      <div :class="{ error: contentTypeError }">
        <div>
          <p>Select where the copy will appear:</p>
        </div>
        <div v-if="ask.copyType === 'UX'">
          <select v-model="ask.contentType" @change="setProductIndex()">
            <option disabled value="">Please select one</option>
            <option
              v-for="(productContentType, index) in productContentTypes"
              :key="index"
            >
              {{ productContentTypes[index].copyLocation }}
            </option>
          </select>
        </div>
        <div v-if="ask.copyType === 'Marketing'">
          <select v-model="ask.contentType" @change="setMarketingIndex()">
            <option disabled value="">Please select one</option>
            <option
              v-for="(marketingContentType, index) in marketingContentTypes"
              :key="index"
            >
              {{ marketingContentTypes[index].copyLocation }}
            </option>
          </select>
        </div>
      </div>
      <div :class="{ error: copyDescriptionError }">
        <span>Enter a copy draft or description of the copy need:</span><br />
        <textarea
          v-model="ask.copyDescription"
          placeholder="Fill in placeholder copy"
        ></textarea>
      </div>
    </div>
    <div>
      <span>Set a max character count (optional):</span><br />
      <input type="number" v-model.number="ask.maxCharacterCount" />
    </div>

    <div>
      <b-button></b-button>
      <button @click="handleSubmit">Generate and copy prompt</button>
    </div>

    <div class="col output">
      <div v-if="!showPrompt" class="prompt-placeholder">
        <img alt="logo" src="./assets/peace.svg" />
      </div>
      <div v-if="showPrompt" class="prompt">
        <PromptMaker
          :variants="ask.variants"
          :copyType="ask.copyType"
          :contentType="ask.contentType"
          :toneOne="ask.toneOne"
          :toneTwo="ask.toneTwo"
          :toneThree="ask.toneThree"
          :copyDescription="ask.copyDescription"
          :maxCharacterCount="ask.maxCharacterCount"
          :neutralTone="neutralTone"
          :conversationalTone="conversationalTone"
          :friendlyTone="friendlyTone"
          :boldTone="boldTone"
        />
      </div>
    </div>
  </div>
  <IntroModule v-if="showIntro" :headline="title" />
</template>

<script>
// import UserConfig from "./components/User-config.vue";
import IntroModule from "./components/IntroModule.vue";
import PromptMaker from "./components/PromptMaker.vue";

export default {
  name: "App",
  components: {
    // UserConfig,
    IntroModule,
    PromptMaker,
  },
  data() {
    return {
      title: "Dialpad Writing Assistant",
      description:
        "Build a prompt to write in Dialpad's voice and context specific tone.",
      showIntro: false,
      showPrompt: false,
      contentTypeError: false,
      copyDescriptionError: false,
      ask: {
        variants: null,
        contentType: null,
        contentTypeIndex: null,
        copyType: "UX",
        toneOne: null,
        toneTwo: null,
        toneThree: null,
        maxCharacterCount: null,
        copyDescription: null,
      },
      neutralTone: "neutral tone with no room for doubt or emotion",
      friendlyTone:
        "relatable and friendly tone with unexpected, clever, or naturally fun personality",
      conversationalTone: "Conversational tone with warmth and guidance",
      boldTone: "Bold and expressive tone with clever personality",
      marketingContentTypes: [
        {
          copyLocation: "Dialbot",
          toneOne: "conversational",
          toneTwo: "neutral",
          toneThree: "friendly",
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Headline",
          toneOne: "bold",
          toneTwo: "friendly",
          toneThree: "neutral",
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Body Copy",
          toneOne: "conversational",
          toneTwo: "friendly",
          toneThree: "neutral",
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
      ],
      productContentTypes: [
        {
          copyLocation: "Banner",
          toneOne: "neutral",
          toneTwo: null,
          toneThree: null,
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Billing section of the dialpad app",
          toneOne: "neutral",
          toneTwo: null,
          toneThree: null,
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Dialbot",
          toneOne: "conversational",
          toneTwo: "neutral",
          toneThree: "friendly",
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Error Messages",
          toneOne: "neutral",
          toneTwo: null,
          toneThree: null,
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Help Center",
          toneOne: "neutral",
          toneTwo: null,
          toneThree: null,
          maxCharacterCountRecommendation: null,
          variants: 3,
        },
        {
          copyLocation: "Notification",
          toneOne: "neutral",
          toneTwo: null,
          toneThree: null,
          maxCharacterCountRecommendation: null,
          variants: 10,
        },
        {
          copyLocation: "Onboarding",
          toneOne: "conversational",
          toneTwo: "neutral",
          toneThree: "",
          maxCharacterCountRecommendation: "",
          variants: 10,
        },
        {
          copyLocation: "Supporting Copy",
          toneOne: "neutral",
          toneTwo: "friendly",
          toneThree: "",
          maxCharacterCountRecommendation: "",
          variants: 10,
        },
        {
          copyLocation: "Tool Tips",
          toneOne: "neutral",
          toneTwo: null,
          toneThree: null,
          maxCharacterCountRecommendation: 30,
          variants: 10,
        },
      ],
    };
  },
  computed: {},
  methods: {
    // methods
    setProductIndex() {
      this.contentTypeIndex = this.productContentTypes.findIndex(
        (x) => x.copyLocation === this.ask.contentType
      );
      // Set variants
      this.ask.variants =
        this.productContentTypes[this.contentTypeIndex].variants;
      // Set tone one
      this.productContentTypes[this.contentTypeIndex].toneOne
        ? (this.ask.toneOne =
            this.productContentTypes[this.contentTypeIndex].toneOne)
        : null;

      this.productContentTypes[this.contentTypeIndex].toneTwo
        ? (this.ask.toneTwo =
            this.productContentTypes[this.contentTypeIndex].toneTwo)
        : null;

      this.productContentTypes[this.contentTypeIndex].toneThree
        ? (this.ask.toneThree =
            this.productContentTypes[this.contentTypeIndex].toneThree)
        : null;
    },
    setMarketingIndex() {
      this.contentTypeIndex = this.marketingContentTypes.findIndex(
        (x) => x.copyLocation === this.ask.contentType
      );
      // Set variants
      this.ask.variants =
        this.marketingContentTypes[this.contentTypeIndex].variants;
      // Set tone one
      this.marketingContentTypes[this.contentTypeIndex].toneOne
        ? (this.ask.toneOne =
            this.marketingContentTypes[this.contentTypeIndex].toneOne)
        : null;

      this.marketingContentTypes[this.contentTypeIndex].toneTwo
        ? (this.ask.toneTwo =
            this.marketingContentTypes[this.contentTypeIndex].toneTwo)
        : null;

      this.marketingContentTypes[this.contentTypeIndex].toneThree
        ? (this.ask.toneThree =
            this.marketingContentTypes[this.contentTypeIndex].toneThree)
        : null;
    },
    handleSubmit() {
      !this.ask.contentType
        ? (this.contentTypeError = true)
        : (this.contentTypeError = false);
      !this.ask.copyDescription
        ? (this.copyDescriptionError = true)
        : (this.copyDescriptionError = false);
      this.ask.contentType && this.ask.copyDescription
        ? ((this.showPrompt = true),
          (this.contentTypeError = false),
          (this.copyDescriptionError = false))
        : null;
      console.log(this.contentTypeError);
    },
    mounted() {
      // mounted
    },
    updated() {},
  },
};
</script>

<style lang="less">
@import "./index.less";
@import "../node_modules/@dialpad/dialtone/lib/build/less/dialtone.less";
</style>
