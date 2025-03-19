<script setup>
import { ref, computed } from "vue";
import CarpetBad from "@/assets/img/carpet-bad.svg";
import CarpetGood from "@/assets/img/carpet-good.svg";

import BlindsBad from "@/assets/img/blinds-bad.svg";
import BlindsGood from "@/assets/img/blinds-good.svg";

import ChairBad from "@/assets/img/chair-bad.svg";
import ChairGood from "@/assets/img/chair-good.svg";

import ClosetBad from "@/assets/img/closet-bad.svg";
import ClosetGood from "@/assets/img/closet-good.svg";

import DoorBad from "@/assets/img/door-bad.svg";
import DoorGood from "@/assets/img/door-good.svg";

import MonitorBad from "@/assets/img/monitor-bad.svg";
import MonitorGood from "@/assets/img/monitor-good.svg";

import BoxesBad from "@/assets/img/boxes-bad.svg";

import ExtensionBad from "@/assets/img/extension-bad.svg";
import ExtensionGood from "@/assets/img/extension-good.svg";

import WiresBad from "@/assets/img/wires-bad.svg";
import WiresGood from "@/assets/img/wires-good.svg";

import HeaterBad from "@/assets/img/heater-bad.svg";
import HeaterGood from "@/assets/img/heater-good.svg";

import CloseIco from "@/assets/img/close-ico.svg";
import ResultIco from "@/assets/img/game-result-ico.svg";

const foundElements = ref([]);
const descriptionText = ref("");
const currentFindElementId = ref(null);
const gameStart = ref(false);
const time = ref(0);
const showResult = ref(false);
let timer = null;

const formattedTime = computed(() => {
  const minutes = Math.floor(time.value / 60);
  const seconds = time.value % 60;
  return `${String(minutes).padStart(2, "0")} : ${String(seconds).padStart(
    2,
    "0"
  )}`;
});
const textData = {
  1: "Неусточивое положение коробок может привести к их паденю на голову коллег",
  2: "Открытый огонь от свечи может привести в возгоранию",
  3: "Стул",
  4: "Открытые дверки шкафа травмоопасны",
  5: "Загроможденный выход может помешать эвакуации при ЧС!",
  6: "Не должен быть слишком близко, чтобы не вредить глазам",
  7: "Неусточивое положение коробок может привести к их паденю на голову коллег",
  8: "Перегруженный удлинитель может вызвать короткое замыкание и как следствие к пожару",
  9: "Плохо смонтирование розетки могут ударить током",
  10: "Перегруженный удлинитель может вызвать короткое замыкание и как следствие к пожару",
};

const handleClick = (event, svgId) => {
  const targetSvg = event.target.closest("svg");
  if (targetSvg) {
    foundElements.value.push(svgId);
    currentFindElementId.value = svgId;
    descriptionText.value = textData[svgId];
  }
};

const startTimer = () => {
  gameStart.value = true;
  if (!timer) {
    timer = setInterval(() => {
      time.value++;
    }, 1000);
  }
};

const stopTimer = () => {
  clearInterval(timer);
  timer = null;
  showResult.value = true;
};

const resetGame = () => {
  foundElements.value = [];
  showResult.value = false;
  time.value = 0;
  startTimer();
};
</script>

<template>
  <div class="game-container">
    <div class="game-inner">
      <div class="game-inner__content">
        <Transition name="fade">
          <div class="find-item capter bad" v-if="!foundElements.includes(1)">
            <CarpetBad
              class="svg-item"
              @click.capture="handleClick($event, 1)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item capter good" v-if="foundElements.includes(1)">
            <CarpetGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item blinds bad" v-if="!foundElements.includes(2)">
            <BlindsBad
              class="svg-item"
              @click.capture="handleClick($event, 2)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item blinds good" v-if="foundElements.includes(2)">
            <BlindsGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item chair bad" v-if="!foundElements.includes(3)">
            <ChairBad
              class="svg-item"
              @click.capture="handleClick($event, 3)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item chair good" v-if="foundElements.includes(3)">
            <ChairGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item closet bad" v-if="!foundElements.includes(4)">
            <ClosetBad
              class="svg-item"
              @click.capture="handleClick($event, 4)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item closet good" v-if="foundElements.includes(4)">
            <ClosetGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item door bad" v-if="!foundElements.includes(5)">
            <DoorBad class="svg-item" @click.capture="handleClick($event, 5)" />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item door good" v-if="foundElements.includes(5)">
            <DoorGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item monitor bad" v-if="!foundElements.includes(6)">
            <MonitorBad
              class="svg-item"
              @click.capture="handleClick($event, 6)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item monitor good" v-if="foundElements.includes(6)">
            <MonitorGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item boxes bad" v-if="!foundElements.includes(7)">
            <BoxesBad
              class="svg-item"
              @click.capture="handleClick($event, 7)"
            />
          </div>
        </Transition>

        <Transition name="fade">
          <div
            class="find-item extension bad"
            v-if="!foundElements.includes(8)"
          >
            <ExtensionBad
              class="svg-item"
              @click.capture="handleClick($event, 8)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div
            class="find-item extension good"
            v-if="foundElements.includes(8)"
          >
            <ExtensionGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item wires bad" v-if="!foundElements.includes(9)">
            <WiresBad
              class="svg-item"
              @click.capture="handleClick($event, 9)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item wires good" v-if="foundElements.includes(9)">
            <WiresGood class="svg-item" />
          </div>
        </Transition>

        <Transition name="fade">
          <div class="find-item heater bad" v-if="!foundElements.includes(10)">
            <HeaterBad
              class="svg-item"
              @click.capture="handleClick($event, 10)"
            />
          </div>
        </Transition>
        <Transition name="fade">
          <div class="find-item heater good" v-if="foundElements.includes(10)">
            <HeaterGood class="svg-item" />
          </div>
        </Transition>
      </div>
      <div
        class="overlay"
        :class="{
          show: currentFindElementId || showResult,
          dark: showResult,
        }"
      ></div>
      <Transition name="fadeScale">
        <div
          class="description-modal"
          v-if="currentFindElementId"
          :data-modal-id="currentFindElementId"
        >
          <div
            class="description-modal__close"
            @click="currentFindElementId = null"
          >
            <CloseIco />
          </div>
          <div class="description-modal__title">Правильно!</div>
          <div class="description-modal__text">{{ descriptionText }}</div>
        </div>
      </Transition>

      <Transition name="fade">
        <div
          class="check-btn"
          v-if="foundElements.length > 0"
          @click="stopTimer"
        >
          Готово. Узнать результат
        </div>
      </Transition>
      <Transition name="fade">
        <div class="start-modal" v-if="!gameStart">
          <div class="start-modal__inner">
            <div class="start-modal__btn" @click="startTimer">Начать игру!</div>
          </div>
        </div>
      </Transition>
      <Transition name="fade">
        <div class="result-modal" v-if="showResult">
          <div class="result-modal__ico"><ResultIco /></div>
          <div class="result-modal__text">
            Вот вы молодец! Прошли игру и теперь знаете как поддерживать порядок
          </div>
          <div class="result-modal__block">
            <div class="result-modal__block-title">Время прохождения</div>
            <div class="result-modal__block-data">{{ formattedTime }}</div>

            <div class="result-modal__block-title">Обнаружено элементов</div>
            <div class="result-modal__block-data">
              {{ foundElements.length }} / 10
            </div>
          </div>
          <div class="start-modal__btn" @click="resetGame">пройти заново</div>
        </div>
      </Transition>
    </div>
  </div>
</template>

<style lang="scss">
.overlay {
  z-index: 3;
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease-in-out;
  &.show {
    opacity: 1;
    visibility: visible;
  }
  &.dark {
    background-color: rgba(0, 0, 0, 0.3);
  }
}
.find-item {
  &.capter.bad {
    bottom: -0.1%;
    left: 16.7%;
    width: 34%;
    height: 18%;
  }

  &.capter.good {
    bottom: -0.1%;
    left: 9.7%;
    width: 37%;
    height: 17.3%;
  }

  &.blinds.bad {
    top: 10.7%;
    left: 28.5%;
    width: 27%;
    height: 21%;
  }

  &.blinds.good {
    top: 10.7%;
    left: 28.5%;
    width: 27.2%;
    height: 36.2%;
  }

  &.chair.bad {
    bottom: 3%;
    left: 20%;
    width: 19%;
    height: 42%;
  }

  &.chair.good {
    bottom: 3%;
    left: 20%;
    width: 19%;
    height: 42%;
  }

  &.closet.bad {
    bottom: 18%;
    left: 60.4%;
    width: 16.9%;
    height: 18%;
  }

  &.closet.good {
    bottom: 20%;
    left: 60.4%;
    width: 16.9%;
    height: 16%;
  }

  &.door.bad {
    top: 32.2%;
    right: 0%;
    width: 12%;
    height: 51%;
  }

  &.door.good {
    top: 31.9%;
    right: 0%;
    width: 11.7%;
    height: 37.3%;
  }

  &.monitor.bad {
    top: 45.2%;
    left: 32%;
    width: 12%;
    height: 17%;
  }

  &.monitor.good {
    top: 45%;
    left: 33.5%;
    width: 12%;
    height: 17%;
  }

  &.boxes.bad {
    top: 8.5%;
    left: 59.5%;
    width: 26.5%;
    height: 17%;
  }

  &.extension.bad {
    top: 45.2%;
    left: 45%;
    width: 42%;
    height: 44%;
  }

  &.extension.good {
    top: 45.2%;
    left: 82.5%;
    width: 3%;
    height: 9.5%;
  }

  &.wires.bad {
    top: 66.5%;
    left: 39.5%;
    width: 8.5%;
    height: 17%;
  }

  &.wires.good {
    top: 66.5%;
    left: 42%;
    width: 6.5%;
    height: 6.5%;
  }

  &.heater.bad {
    bottom: 7%;
    left: 1%;
    width: 16.5%;
    height: 48.6%;
  }

  &.heater.good {
    top: 48.5%;
    left: 1.8%;
    width: 4.3%;
    height: 7.9%;
  }
}
</style>
