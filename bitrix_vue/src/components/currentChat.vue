<template>
  <div class="main">
    <div class="header">
      {{ items[currentIndex].account_name }}
    </div>
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
  props: ["items", "currentIndex"],
  data() {
    return {
      input: "",
      sentMessages: { message: [], time: [], likes: [] },
    };
  },
  mounted() {
    const storageObject = JSON.parse(
      localStorage.getItem(`${this.currentIndex}`)
    );
    if (storageObject === null) {
      return;
    } else {
      for (let i = 0; i < storageObject.message.length; i++) {
        this.sentMessages.message.push(storageObject.message[i]);
        this.sentMessages.time.push(storageObject.time[i]);
        this.sentMessages.likes.push(storageObject.likes[i]);
      }
      this.sentMessages.index = this.currentIndex;
    }
  },
  methods: {
    getMessage() {
      this.splitMessage();
      this.sentMessages.message.push(this.input);
      this.getTime();
      this.storageManagerSet();
      this.input = "";
    },
    sendEmit(currentTime) {
      let latestMessage = {
        index: "",
        message: "",
        time: "",
      };
      latestMessage.index = this.currentIndex;
      latestMessage.message = this.input;
      latestMessage.time = currentTime;
      console.log(latestMessage);
      this.$emit("customChange", latestMessage);
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
      let currentTime = hours + ":" + minutes;
      this.sentMessages.time.push(currentTime);
      this.sendEmit(currentTime);
    },
    liked() {
      this.sentMessages.likes.push(1);
    },
    storageManagerSet() {
      localStorage.setItem(
        `${this.currentIndex}`,
        JSON.stringify(this.sentMessages)
      );
    },
  },
};
</script>

<style>
@import "chatStyles.scss";
</style>
