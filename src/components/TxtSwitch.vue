<template>
  <div ref="wrapper" class="textTransformer">
    <input
      v-if="useInput"
      type="text"
      v-model="text"
      @input="checkForSwitch"
      ref="input"
      :maxlength="maxlength"
    />
    <textarea
      v-else
      v-model="text"
      @input="checkForSwitch"
      ref="textarea"
      :maxlength="maxlength"
    ></textarea>
  </div>
</template>

<script>
export default {
  props: {
    initialText: {
      type: String,
      default: '',
    },
    switchThreshold: {
      type: Number,
      default: 15,
    },
    maxlength: {
      type: Number,
      default: 250,
    },
  },
  data() {
    return {
      text: this.initialText,
      useInput: true,
    };
  },
  mounted() {
    // Call checkForSwitch when the component is mounted to select the correct input/textarea element
    this.checkForSwitch();
  },
    methods: {
      checkForSwitch() {
      const inputOrTextarea = this.useInput ? this.$refs.input : this.$refs.textarea;
      const isOverflowing = inputOrTextarea.scrollWidth > this.$refs.wrapper.offsetWidth;

      console.log(this.$refs.wrapper.offsetWidth)
      console.log('text length:', this.text.length);
      console.log('useInput:', this.useInput);
      console.log('isOverflowing:', isOverflowing);

      if (this.text.length >= this.switchThreshold && isOverflowing) {
        // Switch to textarea
        this.useInput = false;
        this.$nextTick(() => {
          this.$refs.textarea.focus();
        });
      } else if (this.text.length < this.switchThreshold && !isOverflowing) {
        // Switch to input
        this.useInput = true;
        this.$nextTick(() => {
          this.$refs.input.focus();
        });
      }
    },
  },
};
</script>

<style scoped>
.textTransformer input,
.textTransformer textarea {
  padding: 10px 10px;
  border: 2px solid #ddd;
  background-color: #f8f8f8;
  font-size: 14px;
  font-family: Helvetica, Arial, sans-serif;
}

.textTransformer{
  width: 200px;
}
</style>