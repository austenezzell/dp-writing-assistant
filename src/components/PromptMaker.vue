<template>
  <div>
    <h2>
      Write a numbered list with {{ variants }} variants of {{ copyType }} copy
      for {{ contentType }}. Use a
      {{
        toneOne === "neutral"
          ? this.neutralTone
          : toneOne === "conversational"
          ? this.conversationalTone
          : toneOne === "friendly"
          ? this.friendlyTone
          : this.boldTone
          ? toneOne === "bold"
            ? this.boldTone
            : null
          : null
      }}
      for the following prompt: "{{ copyDescription }}" --
    </h2>
    <h2 v-if="toneTwo">
      Write another numbered list with {{ variants }} variants for the same
      prompt in a
      {{
        toneTwo === "neutral"
          ? this.neutralTone
          : toneTwo === "conversational"
          ? this.conversationalTone
          : toneTwo === "friendly"
          ? this.friendlyTone
          : this.boldTone
          ? toneTwo === "bold"
            ? this.boldTone
            : null
          : null
      }}
      --
    </h2>
    <h2 v-if="toneThree">
      Write another numbered list with {{ variants }} variants for the same
      prompt in a
      {{
        toneThree === "neutral"
          ? this.neutralTone
          : toneThree === "conversational"
          ? this.conversationalTone
          : toneThree === "friendly"
          ? this.friendlyTone
          : this.boldTone
          ? toneThree === "bold"
            ? this.boldTone
            : null
          : null
      }}
      --
    </h2>
    <h3 v-if="maxCharacterCount && maxCharacterCount >= 1">
      Limit the character count of your response to a max of
      {{ maxCharacterCount }} characters.
    </h3>
    <p>
      Rules for writing — Be clear, concise, helpful, and relatable when writing
      for the Dialpad interface. Avoid using second person pronouns. Ignore
      irrelevant information. Use simple words and avoid jargon. Use active
      voice. Be straightforward and honest. Aim for an 8th grade reading level
      or lower. Use sentence case in my responses instead of "capital case". —
      always consider the following list of vocabulary specific to dialpad: Ai
      Notes: Use to refer to our Ai Notes feature in Dialpad Meetings. Because
      this is a branded feature, capitalize both words. Ai Transcript: Use to
      refer to our Ai Transcript feature in Dialpad Meetings. Because this is a
      branded feature, capitalize both words. Ai Suggestion: Use to refer to our
      Ai Suggestion feature in Dialpad Meetings. Because this is a branded
      feature, capitalize both words. Allow: Use instead of enable or enabled.
      Turn on is also acceptable—use what makes sense in context. Copy: Use in
      reference to copying text, images, or other content. Delegate: A user who
      can schedule meetings on behalf of other users. Dialpad: Not DialPad or
      DIALPAD. Dialpad Ai, Ai: Use Dialpad Ai when introducing the feature on a
      screen. Use Ai for all following references and when space is limited.
      Never use Voice Intelligence or Vi. Don’t allow: Use instead of disable.
      Turn off is also acceptable—use what makes sense in context. Duplicate:
      Use in reference to making a copy of entities, like groups or contact
      centers. Avoid clone, as it has a biological connotation. Help Center:
      Capitalize both words. Host, co-host: The person who owns a meeting. They
      have access to host controls. Not organizer. Kilobyte, KB: Use all caps
      when abbreviating: KB. Never kB or Kb. Sign in, sign out: Not log in or
      log out. Turn off, off: Use instead of disable or disabled. Don’t allow is
      also acceptable—use what makes sense in context. Turn on, on: Use instead
      of enable or enabled. Allow is also acceptable—use what makes sense in
      context. Work Beautifully: Our brand essence. Used in most of our brand
      copy. The Good Ai: Ai is our most important feature. We have positioned
      Dialpad Ai as the good Ai.
    </p>
  </div>
</template>

<script>
export default {
  name: "PromptMaker",
  props: {
    variants: String,
    copyType: String,
    contentType: String,
    toneOne: String,
    toneTwo: String,
    toneThree: String,
    copyDescription: String,
    maxCharacterCount: Number,
    neutralTone: String,
    conversationalTone: String,
    friendlyTone: String,
    boldTone: String,
  },
  data() {
    return {
      // data
    };
  },
  methods: {
    // methods
  },
  mounted: function () {
    // console.log(this.contentType);
  },
  computed: {
    // computed
  },
};
</script>
