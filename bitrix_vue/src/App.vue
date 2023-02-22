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
          <span class="lupa"></span>
          <span class="cross"></span>
          <input class="input_search" placeholder="Поиск" type="text" />
        </div>
        <div class="chats_container">
          <div class="chat_item" @click="chatWindow">
            <div class="avatar_box">
              <div class="avatar"></div>
            </div>
            <div class="chat_info">
              <div class="name">{{ current_name }}</div>
              <div class="latest_message">{{ latest_message }}</div>
              <div class="latest_time">{{ latest_time }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="empty_dialogue">
        <div class="empty_dialogue_text">
          Начните диалог, выбрав контакт из списка слева.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current_name: "Дмитрий Дмитривич",
      latest_message: "привет",
      latest_time: "12:30",
      chatWindow: "",
    };
  },
  components: {},
  methods: {
    addDialogue() {},
  },
};
</script>
<style>
@import "stylesheet.scss";
</style>
