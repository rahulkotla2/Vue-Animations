<template>
  <router-view v-slot="slotProps">
    <transition name="fade-button" mode="out-in">
      <component :is="slotProps.Component"></component>
    </transition>
  </router-view>
  <!-- <div class="container">
    <users-data></users-data>
  </div>
  <div class="container">
    <div class="block" :class="{ animate: animatedBlock }"></div>
    <button @click="animate">Animate</button>
  </div>
  <div class="container">
    <transition :css="false" @before-enter="beforeEnter" @enter="enter" @after-enter="afterEnter"
      @before-leave="beforeLeave" @leave="leave" @after-leave="afterLeave" @enter-cancelled="enterCancelled"
      @leave-cancelled="leaveCancelled">
      <p v-if="paraIsVisible">This is Sometimes Visible</p>
    </transition>
    <button @click="toggleParagraph">toggle paragraph</button>
  </div>
  <div class="container">
    <transition name="fade-button" mode="out-in">
      <button @click="showDetails" v-if="!detailsAreVsisible">Show Details</button>
      <button @click="hideDetails" v-else>Hide Details</button>
    </transition>
  </div>
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div> -->
</template>  

<script>
// import UsersData from './components/UsersData.vue'
export default {
  components: {
    // UsersData,
  },
  data() {
    return {
      dialogIsVisible: false,
      animatedBlock: false,
      paraIsVisible: false,
      detailsAreVsisible: false,
      enterInterval: null,
      leaveInterval: null,
    };
  },
  methods: {
    enterCancelled() {
      clearInterval(this.enterInterval);
    },
    leaveCancelled() {
      clearInterval(this.leaveInterval);
    },
    beforeEnter(el) {
      console.log('before Enter');
      el.style.opacity = 0;
    },
    enter(el, done) {
      console.log("enter");
      let round = 1;
      this.enterInterval = setInterval(() => {
        el.style.opacity = round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.enterInterval);
          done();
        }
      }, 20);
    },
    afterEnter(el) {
      console.log("After Enter");
      console.log(el);
    },
    beforeLeave(el) {
      console.log("Before Leave");
      el.style.opacity = 1;
    },
    leave(el, done) {
      console.log("Leave");
      let round = 1;
      this.leaveInterval = setInterval(() => {
        el.style.opacity = 1 - round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.leaveInterval);
          done();
        }
      }, 20)
    },
    afterLeave(el) {
      console.log("After Leave");
      console.log(el);
    },
    showDetails() {
      this.detailsAreVsisible = true;
    },
    hideDetails() {
      this.detailsAreVsisible = false;
    },
    toggleParagraph() {
      this.paraIsVisible = !this.paraIsVisible;
    },
    animate() {
      this.animatedBlock = true;
    },
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
}

button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}

.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  transition: transform 0.3s ease-out;
}

.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}

.animate {
  /* transform: translateX(-150px); */
  animation: slide-scale 0.3s ease-out forwards;
}

@keyframes slide-scale {
  0% {
    transform: translateX(0) scale(1);
  }

  70% {
    transform: translateX(-120px) scale(1.1);
  }

  100% {
    transform: translateX(-150px) scale(1);
  }
}

.para-enter-from {
  /* transform: translateY(-50px);
  opacity: 0; */
}

.para-enter-active {
  /* transition: all 0.3s ease-out; */
  animation: slide-scale 0.3s ease-out;
}

.para-enter-to {
  /* transform: translateY(0);
  opacity: 1; */
}

.para-leave-from {
  /* transform: translateY(0);
  opacity: 1; */
}

.para-leave-active {
  /* transition: all 0.3s ease-out; */
  animation: slide-scale 0.3s ease-out;
}

.para-leave-to {
  /* transform: translateY(50px);
  opacity: 0; */
}

.fade-button-enter-from,
.fade-button-leave-to {
  opacity: 0;
}

.fade-button-enter-active {
  transition: opacity 0.3s ease-out;
}

.fade-button-leave-active {
  transition: opacity 0.3s ease-out;
}

.fade-button-enter-to,
.fade-button-leave-from {
  opacity: 1;
}
</style>