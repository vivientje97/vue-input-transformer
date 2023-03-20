<template>
  <div>
  <h2>Transformer input</h2>
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
      default: ''
    },
    switchThreshold: {
      type: Number,
      default: 15
    },
    maxlength: {
      type: Number,
      default: 250
    }
  },
  data() {
    return {
      text: this.initialText,
      useInput: true
    };
  },
  methods: {
    checkForSwitch() {
      if (this.text.length >= this.switchThreshold && this.useInput) {
        this.useInput = false;
        this.$nextTick(() => {
          this.$refs.textarea.focus();
        });
      } else if (this.text.length < this.switchThreshold && !this.useInput) {
        this.useInput = true;
        this.$nextTick(() => {
          this.$refs.input.focus();
        });
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
textarea {
  height: 100px;
}

input{

}

input, textarea{
  width: 300px;
  padding: 12px 20px;
  box-sizing: border-box;
  border: 2px solid #ccc;
  border-radius: 4px;
  background-color: #f8f8f8;
  font-size: 16px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
