<template>
  <div class="main">
    <div class="header">
      <div class="messageAvatar"></div>
      <div class="headerInfo">
        <div class="headerFullname">
          <div class="headerName">{{ items[currentIndex].account_name }}</div>
          <div class="headerTime">
            Заходил сегодня в {{ latestTime[currentIndex] }}
          </div>
        </div>
        <div class="headerBg">пользователь</div>
      </div>
      <div class="headerButtons">
        <button class="callBtn">Видеозвонок HD</button>
        <button class="inviteBtn">+ Пригласить</button>
        <button class="findBtn">
          <img src="./images/icons/lupa.svg" alt="" />
        </button>
      </div>
    </div>
    <div class="messageContainer">
      <div class="previousContainer">
        <span class="previousMsg">Загрузить более ранние сообщения</span>
        <a href="#" class="previousDate">сегодня</a>
      </div>

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
              <img
                @click="liked"
                src="./images/like.svg"
                alt=""
                class="likedMsg"
              />
            </div>
            <div class="currentTime">
              Нравится {{ sentMessages.time[index] }}
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
        placeholder="Введите сообщение"
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
  props: ["items", "currentIndex", "latestTime"],
  data() {
    return {
      input: "",
      sentMessages: { message: [], time: [], likes: [] },
      formattedMessages: "",
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
    sendEmit(currentTime) {
      let latestMessage = {
        index: "",
        message: "",
        time: "",
      };
      latestMessage.index = this.currentIndex;
      latestMessage.message = this.input;
      latestMessage.time = currentTime;
      this.$emit("customChange", latestMessage);
    },
    splitMessage() {
      let i = 0;
      while (i < this.input.length) {
        let next = this.input.substr(i, 90);
        this.formattedMessages += `${next}\n`;
        i += 130;
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
    getMessage() {
      this.splitMessage();
      this.sentMessages.message.push(this.formattedMessages);
      this.getTime();
      this.storageManagerSet();
      this.input = "";
    },
  },
};
</script>

<style>
@import "chatStyles.scss";
</style>
