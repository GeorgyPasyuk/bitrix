<template>
  <div class="window">
    <div class="main_nav_bar"></div>
    <div class="msg_box">
      <div class="msg_nav_bar"></div>
      <div class="chats">
        <div class="search">
          <input class="input_search" type="text" />
        </div>
        <div class="chats_container">
          <div class="chat_item">
            <div class="avatar_box">
              <div class="avatar"></div>
            </div>
            <div class="chat_info">
              <div class="name">{{ current_name }}</div>
              <div class="latest_message">{{ latest_message }}</div>
            </div>
          </div>
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
      latest_message: "был в сети 30 мин. назад",
    };
  },
  components: {},
};
</script>
<style>
@import "stylesheet.scss";
</style>
