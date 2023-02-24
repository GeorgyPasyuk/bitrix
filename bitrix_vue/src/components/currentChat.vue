<template>
  <div class="main">
    <div class="header"></div>
    <div class="messageContainer">
      <span
        class="messageItems"
        v-for="(item, index) in sentMessages.message"
        v-bind:key="item"
      >
        <div class="messageAvatar"></div>
        <div class="sentMessage">
          {{ item }}
          <div class="infoContainer">
            <div class="likes">
              {{ sentMessages.likes[index] }}
              <img @click="liked" src="./images/like.svg" alt="" />
            </div>
            <div class="currentTime">
              {{ sentMessages.time[index] }}
            </div>
          </div>
        </div>
      </span>
    </div>
    <div class="inputContainer">
      <textarea
        name=""
        id="textarea"
        cols="30"
        rows="10"
        class="textInput"
        v-on:keydown.enter="getMessage"
        v-model="this.input"
      ></textarea>
      <div class="icons">
        <img src="./images/icons/addFiles.svg" alt="" />
        <img src="./images/icons/person.svg" alt="" />
        <img src="./images/icons/square.svg" alt="" />
        <img src="./images/icons/smile.svg" alt="" />
        <img src="./images/icons/double.svg" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "currentChat",
  data() {
    return {
      input: "",
      sentMessages: { message: [], time: [], likes: [] },
    };
  },
  methods: {
    getMessage() {
      this.splitMessage();
      this.sentMessages.message.push(this.input);
      this.getTime();
      this.input = "";
    },
    splitMessage() {
      let symbol = [...this.input];
      if (symbol > 130) {
        this.input.push(`\n`);
      }
    },
    getTime() {
      let date = new Date();
      let hours = date.getHours();
      let minutes = date.getMinutes();
      this.sentMessages.time.push(hours + ":" + minutes);
    },
    liked() {
      this.sentMessages.likes.push(1);
    },
  },
};
</script>

<style>
@import "chatStyles.scss";
</style>
