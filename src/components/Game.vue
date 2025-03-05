<template>
  <div class="container">
    <p class="question">Các bạn nữ SotaTeker có xinh đẹp không 🤩</p>
    <img :src="currentIcon" class="icon" alt="emotion icon" />
    <div class="buttons">
      <button class="yes" @click="handleYes">{{ yesText }}</button>
      <button
        class="no"
        ref="noButton"
        @mouseenter="moveNoButton"
        @click="handleNo"
        :style="{ top: noPosition.top + 'px', left: noPosition.left + 'px' }"
      >
        {{ noText }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Game",
  data() {
    return {
      icons: [],
      currentIcon: "",
      yesText: "Yes",
      noText: "No",
      noPosition: { top: 100, left: 300 },
      buttonWidth: 120,
      buttonHeight: 50,
    };
  },
  methods: {
    moveNoButton() {
      const maxTop = window.innerHeight - this.buttonHeight;
      const maxLeft = window.innerWidth - this.buttonWidth;
      this.noPosition = {
        top: Math.random() * maxTop,
        left: Math.random() * maxLeft,
      };

      this.currentIcon =
        this.icons[Math.floor(Math.random() * this.icons.length)];
    },
    handleNo() {
      this.yesText = "Yes";
      this.noText = "Yes";

      setTimeout(() => {
        alert("Là rõ rồi! ❤️");
      }, 500);
    },
    handleYes() {
      alert("Là rõ rồi! ❤️");
    },
    loadIcons() {
      const context = require.context("@/assets/icons", false, /\.png$/);
      this.icons = context.keys().map((key) => context(key));
      if (this.icons.length > 0) {
        this.currentIcon = this.icons[0];
      }
    },
  },
  mounted() {
    this.noPosition = { top: 100, left: 300 };
    this.loadIcons();
  },
};
</script>

<style>
.container {
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  position: relative;
}

.question {
  font-size: 24px;
  margin-bottom: 20px;
}

.icon {
  width: 80px;
  height: 80px;
  margin-bottom: 20px;
}

.buttons {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

button {
  font-size: 18px;
  padding: 10px 20px;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  transition: top 0.5s ease, left 0.5s ease;
}

.yes {
  background-color: #28a745;
  color: white;
}

.no {
  background-color: #dc3545;
  color: white;
  position: absolute;
  transition: top 0.5s ease, left 0.5s ease;
}
</style>
