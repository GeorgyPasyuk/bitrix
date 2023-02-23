<template>
  <div class="main">
    <div class="header"></div>
    <div class="messageContainer">
      <span
        class="messageItems"
        v-for="sentMessage in sentMessages"
        v-bind:key="sentMessage"
      >
        <div class="messageAvatar"></div>
        <div class="sentMessage">
          {{ sentMessage }}
          <div class="infoContainer">
            <div class="likes">1</div>
            <div class="currentTime">{{ sentMessages.time }}</div>
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
        v-model="this.messages"
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
      messages: "",
      sentMessages: { message: "", time: "" },
    };
  },
  methods: {
    getMessage() {
      const textarea = document.getElementById("textarea");
      this.splitMessage();
      console.log(this.messages);
      console.log(this.sentMessages);
      this.sentMessages.message = this.messages;
      this.getTime();
      textarea.value = "";
      this.messages = "";
    },
    splitMessage() {
      let symbol = [...this.messages];
      if (symbol > 130) {
        this.messages.push(`\n`);
      }
    },
    getTime() {
      let date = new Date();
      let hours = date.getHours();
      let minutes = date.getMinutes();
      this.sentMessages.time = hours + ":" + minutes;
    },
  },
};
</script>

<style>
@import "chatStyles.scss";
</style>
