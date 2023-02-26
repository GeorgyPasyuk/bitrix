<template>
  <div class="window">
    <div class="main_nav_bar"></div>
    <div class="msg_box">
      <div class="msg_nav_bar">
        <div class="icons_items">
          <img src="./images/icons/msg.svg" alt="#" class="msg_icons" />
          <img src="./images/icons/lines.svg" alt="#" class="msg_icons" />
          <img
            src="./images/icons/notifications.svg"
            alt="#"
            class="msg_icons"
          />
          <img src="./images/icons/calls.svg" alt="#" class="msg_icons" />
          <img src="./images/icons/settings.svg" alt="#" class="msg_icons" />
          <img src="./images/icons/news.svg" alt="#" class="msg_icons" />
        </div>
      </div>
      <div class="chats">
        <div class="search">
          <span class="lupa" @click="getChildVariable"></span>
          <span class="cross" @click="clearInput"></span>
          <input
            class="input_search"
            id="searchInput"
            placeholder="Поиск"
            type="text"
            v-model="inputModel"
          />
        </div>
        <div class="chats_container">
          <div
            class="chat_item"
            @click="sendChatId(index)"
            v-for="(item, index) in items"
            v-bind:key="item.account_id"
          >
            <div class="avatar_box">
              <div class="avatar" :style="avatarCol[index]">
                {{ Array.from(item.account_name)[0] }}
              </div>
            </div>
            <div class="chat_info">
              <div class="name">{{ item.account_name }}</div>
              <div class="latest_message">
                {{ latestEvents.latestMessage[index] }}
              </div>
              <div class="latest_time">
                {{ latestEvents.latestTime[index] }}
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="empty_dialogue">
        <current-chat
          v-if="this.currentIndex === 0"
          :items="items"
          :currentIndex="currentIndex"
          @customChange="logChange"
        />
        <current-chat
          v-if="this.currentIndex === 1"
          :items="items"
          :currentIndex="currentIndex"
          @customChange="logChange"
        />
        <current-chat
          v-if="this.currentIndex === 2"
          :items="items"
          :currentIndex="currentIndex"
          @customChange="logChange"
        />
        <current-chat
          v-if="this.currentIndex === 3"
          :items="items"
          :currentIndex="currentIndex"
          @customChange="logChange"
        />
        <current-chat
          v-if="this.currentIndex === 4"
          :items="items"
          :currentIndex="currentIndex"
          @customChange="logChange"
        />
        <div class="empty_dialogue_text" v-if="this.currentIndex === ''">
          Начните диалог, выбрав контакт из списка слева.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import currentChat from "@/components/currentChat";

export default {
  name: "App",
  props: ["sentMessages"],
  data() {
    return {
      items: [
        {
          account_id: "1",
          account_name: "Alex",
        },
        {
          account_id: "2",
          account_name: "Brad",
        },
        {
          account_id: "3",
          account_name: "Chad",
        },
        {
          account_id: "4",
          account_name: "Darla",
        },
        {
          account_id: "5",
          account_name: "Katyushka",
        },
      ],
      currentIndex: "",
      latestEvents: {
        latestMessage: {
          0: "",
          1: "",
          2: "",
          3: "",
          4: "",
          5: "",
        },
        latestTime: {
          0: "",
          1: "",
          2: "",
          3: "",
          4: "",
          5: "",
        },
      },
      inputModel: "",
      avatarCol: {
        0: {
          backgroundColor: "",
        },
        1: {
          backgroundColor: "",
        },
        2: {
          backgroundColor: "",
        },
        3: {
          backgroundColor: "",
        },
        4: {
          backgroundColor: "",
        },
      },
    };
  },
  mounted() {
    for (let i = 0; i < localStorage.length; i++) {
      let storage = JSON.parse(localStorage.getItem(i));
      for (let j = 0; j < storage.message.length; j++) {
        this.latestEvents.latestMessage[i] = storage.message[j];
        this.latestEvents.latestTime[i] = storage.time[j];
      }
    }
  },
  created() {
    for (let i = 0; i < 5; i++) {
      this.avatarCol[i].backgroundColor =
        "#" + Math.floor(Math.random() * 16777215).toString(16);
    }
  },
  components: { currentChat },
  methods: {
    clearInput() {
      const input = document.getElementById("searchInput");
      return (input.value = "");
    },
    sendChatId(index) {
      this.currentIndex = index;
    },
    logChange(sentMessage) {
      this.latestEvents.latestMessage[sentMessage.index] = sentMessage.message;
      this.latestEvents.latestTime[sentMessage.index] = sentMessage.time;
    },
  },
};
</script>
<style>
@import "stylesheet.scss";
</style>
<!--
[1] - нормальное отображение последних сообщений - Done
[2] - нормальное отображение аватаров
[3] - верстка макета
[4] - адаптивность
[5] - рабочий поиск
[6] - рабочие кнопки
[7] - удаление сообщений
-->
