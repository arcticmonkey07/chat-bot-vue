<template>
  <div class="container">
    <ul class="chat-list">
      <Message :allMessages="allMessages" />
      <li class="typing">{{ dots }}</li>
    </ul>
    <div class="buttons" v-show="showButtons">
      <button
        class="button"
        v-for="userMessage in userMessages"
        :key="userMessage"
        @click="userEnterMessage(userMessage)"
      >
        {{ userMessage }}
      </button>
    </div>
  </div>
</template>

<script>
import Message from './components/Message.vue';

export default {
  components: {
    Message,
  },
  data() {
    return {
      allMessages: [],
      userMessages: [
        "Заказать пиццу",
        "Установить будильник",
        "Вывести погоду",
      ],
      dots: "",
      showButtons: false,
    };
  },
  methods: {
    delay(ms) {
      return new Promise((resolve) => {
        setTimeout(resolve, ms);
      });
    },
    userEnterMessage(message) {
      this.typing();
      this.delay(2000).then(() => {
        this.allMessages.push({ text: message, who: "user" });
      });
      this.delay(2000).then(() => {
        this.dots = "";
      });
      this.showButtons = false;
      this.botResponds(message);
    },
    botResponds(message) {
      if (message === "Заказать пиццу") {
        setTimeout(() => {
          this.allMessages.push({ text: "Сейчас же закажу" });
        }, 3500);
      } else if (message === "Установить будильник") {
        setTimeout(() => {
          this.allMessages.push({ text: "Установил!" });
        }, 3500);
      } else if (message === "Вывести погоду") {
        setTimeout(() => {
          this.allMessages.push({ text: "В Москве сейчас -10" });
        }, 3500);
      }
    },
    typing() {
      setTimeout(() => {
        this.dots = ".";
      }, 200);
      setTimeout(() => {
        this.dots = "..";
      }, 800);
      setTimeout(() => {
        this.dots = "...";
      }, 1200);
      // this.delay(500).then(() => (this.dots = "."));
      // this.delay(1000).then(() => (this.dots = ".."));
      // this.delay(1500).then(() => (this.dots = "..."));
    },
  },
  mounted() {
    new Promise((resolve) => {
      setTimeout(() => {
        resolve(this.allMessages.push({ text: "Добро пожаловать в чатбот!" }));
      }, 1000);
    })
      .then(() => {
        return new Promise((resolve) => {
          setTimeout(() => {
            resolve(
              this.allMessages.push({
                text: "Привет! Что я могу для Вас сделать?",
              })
            );
          }, 1000);
        });
      })
      .then(() => {
        setTimeout(() => {
          this.showButtons = true;
        }, 1500);
      });
  },
};
</script>

<style>
body {
  font-family: monospace;
  background: linear-gradient(to right, #f3d9a0, #57572c);
}

.container {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 300px;
  height: 413px;
  padding: 10px;
  transform: translate(-50%, -50%);
  border-radius: 15px;
  background-color: #fff;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 12px 24px 0px;
}

.chat-list {
  display: flex;
  flex-direction: column;
  align-items: start;
  padding: 0;
  list-style: none;
}

.buttons {
  display: flex;
  flex-direction: column;
  align-items: start;
}

.button {
  margin: 0 0 5px 0;
  padding: 12px;
  font-size: 14px;
  color: #000;
  background: #f3d9a0;
  border: none;
  border-radius: 22px;
  box-shadow: rgba(0, 0, 0, 0.15) 0px 1px 2px 0px;
  cursor: pointer;
  transition: all 0.2s;
}

.button:hover {
  color: #474444;
  background: #dec48b;
}

.typing {
  margin-left: auto;
  font-size: 20px;
}

@media screen and (max-width: 360px) {
  .container {
    width: 220px;
  }

  .chat-list__message {
    font-size: 12px;
  }

  .button {
    font-size: 12px;
  }
}
</style>
