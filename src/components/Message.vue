<template>
  <li
    class="chat-list__message"
    :class="[{ userMessage: botMessage.who }]"
    v-for="botMessage in allMessages"
    :key="botMessage.text"
  >
    {{ botMessage.text }}
  </li>
</template>

<script>
export default {
  props: ["allMessages"],
};
</script>

<style scoped>
.chat-list__message {
  display: inline-block;
  margin: 0 0 7px 0;
  padding: 12px;
  font-size: 14px;
  background: #929254;
  border-radius: 0 22px 22px 22px;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 12px 24px 0px;
}

.userMessage {
  margin-left: auto;
  border-radius: 22px 0 22px 22px;
}
</style>
