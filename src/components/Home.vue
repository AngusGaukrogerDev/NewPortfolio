<template class="home__default">
  <Loader @complete="ready = true" />

  <div v-if="ready" id="FlipCard" class="flip-card bg-white dark:bg-black">
    <div id="CardInner" class="flip-card-inner">
      <div
        id="CardFront"
        class="flip-card-front w-screen bg-white dark:bg-black h-screen page__grid"
      >
        <div></div>
        <div></div>
        <div></div>
        <div></div>
        <TransitionRoot
          appear
          :show="isShowing"
          as="template"
          enter="transform transition duration-[800ms]"
          enter-from="opacity-0 rotate-[-120deg] scale-50"
          enter-to="opacity-100 rotate-0 scale-100"
          leave="transform duration-200 transition ease-in-out"
          leave-from="opacity-100 rotate-0 scale-100 "
          leave-to="opacity-0 scale-95 "
        >
          <div class="border-4 flex row justify-center items-center">
            <div class="">
              <h1 class="dark:bg-black dark:text-white">Angus Gaukroger</h1>
              <h2 class="">Full-Stack Software Developer</h2>
            </div>
          </div>
        </TransitionRoot>
      </div>

      <div
        id="CardBack"
        class="flip-card-back w-screen h-screen bg-white dark:bg-black page__grid"
      >
        <SubGrid1 />
        <Subgrid2 @dark-changed="darkSwitcher" />
        <Subgrid4 @contact-view="contactViewSwitch()" />
        <Subgrid3 v-bind:Check="contactSwitcher" />
      </div>
    </div>
  </div>
</template>

<script setup>
import SubGrid1 from "./NavGrid/Subgrid1.vue";
import Subgrid2 from "./NavGrid/Subgrid2.vue";
import Subgrid3 from "./NavGrid/Subgrid3.vue";
import Subgrid4 from "./NavGrid/Subgrid4.vue";
import Loader from "./Loader.vue";

import { TransitionRoot } from "@headlessui/vue";
import { onMounted, ref } from "vue";
import { useDark, useToggle } from "@vueuse/core";

let colorScheme = ref("linear-gradient(to left, white 50%, black 50%) right");
let hoverColor = ref("white");
let ready = ref(false);
let contactSwitcher = ref(false);

const isDark = useDark();
const toggleDark = useToggle(isDark);

function darkSwitcher() {
  toggleDark();
  if (isDark.value) {
    colorScheme.value = "linear-gradient(to left, black 50%, white 50%) right";
    hoverColor.value = "black";
    console.log(isDark);
  } else {
    colorScheme.value = "linear-gradient(to left, white 50%, black 50%) right";
    hoverColor.value = "white";
    console.log(isDark);
  }
}

function contactViewSwitch(){
  if(contactSwitcher.value == false)
  {
    contactSwitcher.value = true;
  }
  else
  {
    contactSwitcher.value = false;
  }
}

onMounted(() => {
  if (isDark.value) {
    colorScheme.value = "linear-gradient(to left, black 50%, white 50%) right";
    hoverColor.value = "black";
    // console.log(isDark);
  } else {
    colorScheme.value = "linear-gradient(to left, white 50%, black 50%) right";
    hoverColor.value = "white";
    // console.log(isDark);
  }
});
let isShowing = ref(true);
// let clearDOM = ref(true);

// function changeHoverDark() {
//   colorScheme.value = "linear-gradient(to left, black 50%, white 50%) right";
//   hoverColor.value = "black";
// }
// function changeHoverLight() {
//   colorScheme.value = "linear-gradient(to left, white 50%, black 50%) right";
//   hoverColor.value = "white";
// }
</script>
<style lang="scss" scoped>
.home__default {
  overflow: hidden;
}
.page__grid {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-template-rows: auto auto auto;
  padding-left: 10%;
  padding-right: 10%;
  padding-top: 5%;
  padding-bottom: 5%;
  grid-column-gap: 2%;
  grid-row-gap: 2%;
}
</style>
<style>
.floating {
  animation-name: floating;
  animation-duration: 8s;
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
    transform: translate(-15px, -15px);
  }
  100% {
    transform: translate(0, -0px);
  }
}

.scrolling__text {
  overflow: hidden; /* Ensures the content is not revealed until the animation */
  border-right: 0.15em solid black; /* The typwriter cursor */
  white-space: nowrap; /* Keeps the content on a single line */
  margin: 0 auto; /* Gives that scrolling effect as the typing happens */
  letter-spacing: 0.1em; /* Adjust as needed */
  animation: typing 5s steps(38, end), blink-caret 1.5s step-end infinite;
}
@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 80%;
  }
}

/* The typewriter cursor effect */
@keyframes blink-caret {
  from,
  to {
    border-color: white;
  }
  50% {
    border-color: black;
  }
}

.hover__transition {
  display: inline-block;
  padding: 1em 2em;
  text-align: center;
  /*color: v-bind(hoverColor);*/
  /*background: v-bind(hoverColor);*/

  /* "to left" / "to right" - affects initial color */
  background: v-bind(colorScheme);
  background-size: 250%;
  object-fit: cover;
  transform: scale(1.03);
  transition: 0.5s ease-out;
}
.hover__transition:hover {
  background-position: left;
  cursor: pointer;
  color: v-bind(hoverColor);
}

.flip-card {
  /* background-color: transparent; */
  width: 100vw;
  height: 100vh;
  border: 1px solid black;
  perspective: 1000px; /* Remove this if you don't want the 3D effect */
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front,
.flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden; /* Safari */
  backface-visibility: hidden;
}

.flip-card-front {
  background-color: white;
}

/* Style the back side */
.flip-card-back {
  background-color: white;
  /* color: white; */
  transform: rotateY(180deg);
}

.center__children {
  display: flex;
  direction: row;
  justify-content: center;
  align-items: center;
  padding: 5% 5% 5% 5%;
  border-color: #f3f4f6;
}

.floating__borders {
  border-color: 8px solid #4b5563;
  border-radius: 25px;
}
.center__content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
