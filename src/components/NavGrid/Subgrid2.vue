<template>
  <div class="page__subgrid2 floating">
    <div
      class="center__children child1__subgrid2 border-4 hover__transition tooltip tooltip-top tooltip-primary"
      @click="router.push('/CV')"
      data-tip="CV"
    >
      <ion-icon size="large" name="document-text"></ion-icon>
    </div>
    <div
      class="center__children border-4 hover__transition tooltip tooltip-top tooltip-primary"
      @click="router.push('/Projects')"
      data-tip="Projects"
    >
      <ion-icon size="large" name="build"></ion-icon>
    </div>
    <div
      class="center__children border-4 hover__transition tooltip tooltip-right tooltip-primary"
      @click="router.push('/Stack')"
      data-tip="My Stack"
    >
      <ion-icon size="large" name="cube"></ion-icon>
    </div>
    <div
      class="center__children border-4 hover__transition tooltip tooltip-bottom tooltip-primary"
      @click="emit('darkChanged')"
      data-tip="Light/Dark Mode"
    >
      <ion-icon size="large" name="contrast"></ion-icon>
    </div>
    <a
      href="https://connectdorset.com/"
      class="center__children border-4 hover__transition tooltip tooltip-bottom tooltip-primary"
      data-tip="My Business - Connect Dorset"
    >
      <ion-icon v-show="business == false" size="large" name="business"></ion-icon>
      <!-- <span class="hover__font" v-show="business">My Business</span> -->
    </a>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const emit = defineEmits(["darkChanged"]);

const router = useRouter();

let business = ref(false);

// function darkToggle() {
//   toggleDark();
//   if (isDark) {
//     emit("darkSwitch");
//   } else {
//     emit("lightSwitch");
//   }
// }

// function exitSequence() {
//     emit('redirect');
// }
</script>

<style lang="scss" scoped>
.hover__font {
  font-size: small;
}
.page__subgrid2 {
  grid-row: 1 / span 2;
  grid-column: 3 / span 1;

  grid-template-columns: auto auto;
  grid-template-rows: auto auto;
  display: grid;
  min-width: 0;
}
.child1__subgrid2 {
  grid-row: 1 / span 2;
  grid-column: 1 / span 1;
  min-width: 0;
}
.floating {
  animation-name: floating;
  animation-duration: 5s;
  animation-iteration-count: infinite;
  animation-timing-function: ease-in-out;
  margin-left: 30px;
  margin-top: 5px;
}

@keyframes floating {
  0% {
    transform: translate(0, 0px);
  }
  50% {
    transform: translate(15px, 15px);
  }
  100% {
    transform: translate(0, -0px);
  }
}
</style>
