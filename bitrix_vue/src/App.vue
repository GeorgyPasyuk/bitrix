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
              <div class="avatar"></div>
            </div>
            <div class="chat_info">
              <div class="name">{{ item.account_name }}</div>
              <div class="latest_message">{{ latestMessage }}</div>
              <div class="latest_time">12:30</div>
            </div>
          </div>
        </div>
      </div>
      <div class="empty_dialogue">
        <current-chat
          v-if="this.currentIndex !== ''"
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
      latestMessage: "",
    };
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
    logChange(event) {
      this.latestMessage = event;
    },
  },
};
</script>
<style>
@import "stylesheet.scss";
</style>
