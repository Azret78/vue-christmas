<template>
  <ul class="lightrope" v-if="allElement">
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
  <div class="tree">
    <div class="tree__stvol">
      <div class="tree__complect">
        <div
          v-for="(toy, idx) in toys"
          :key="idx"
          class="tree__toy"
          :class="toy.color.length !== 0 ? toy.color : '_dashed'"
          @click="openForm(idx)"
          :id="idx + 1"
        >
          <div class="tree__toy-ushko">
            <picture>
              <img src="../../public/ushko.png" alt="" />
            </picture>
          </div>
          <p>{{ toy.description }}</p>
        </div>
      </div>
    </div>
  </div>
  <div v-show="openForma" class="tree__forma">
    <div class="tree__form">
      <div class="tree__form-title">
        <h5>Создайте новогоднюю игрушку</h5>
      </div>
      <div class="tree__pole">
        <label for="color">Выберите цвет новогодней игрушки</label>
        <select id="color" v-model="selectedToy.color">
          <option disabled selected value="">Выберите цвет</option>
          <option value="_red">Красный</option>
          <option value="_blue">Синий</option>
          <option value="_green">Зелёный</option>
          <option value="_yellow">Жёлтый</option>
          <option value="_light-blue">Голубой</option>
          <option value="_orange">Оранжевый</option>
          <option value="_fiolet">Фиолетовый</option>
        </select>
      </div>
      <div class="tree__pole">
        <label for="opisaniye"
          >Введите текст, который отобразится на игрушке (не больше 5
          слов)</label
        >
        <input
          type="text"
          id="opisaniye"
          v-model="selectedToy.description"
          placeholder="Текст на игрушке"
        />
      </div>
      <small v-show="errorMessage"
        >Заполните обязательные поля !!! <br />Другого выхода нет</small
      >
      <button class="tree__btn" @click="createToy()">Создать игрушку</button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      toys: Array.from({ length: 12 }, () => ({ color: '', description: '' })),
      openForma: false,
      selectedToy: {},
      selectedToyIndex: null,
      errorMessage: false
    }
  },
  computed: {
    allElement () {
      return this.toys.every((toy) => toy.color && toy.description)
    }
  },
  watch: {
    allElement (newValue) {
      if (newValue) {
        console.log(newValue)
      }
    }
  },
  methods: {
    openForm (index) {
      this.selectedToyIndex = index
      this.selectedToy = this.toys[index]
      this.openForma = true
    },
    closeForm () {
      this.openForma = false
    },
    createToy () {
      if (
        this.selectedToy.description.length !== 0 &&
        this.selectedToy.color !== ''
      ) {
        this.toys[this.selectedToyIndex] = { ...this.selectedToy }
        this.openForma = false
        this.errorMessage = false
      } else {
        this.errorMessage = true
      }
    }
  }
}
</script>
<style lang="scss">
.tree {
  width: 100%;
  min-height: 100vh;
  background: url("../../public/tree.webp") repeat-y,
    url("../../public/tree-root.webp") no-repeat;
  background-size: 100% auto, 100% auto;
  background-position: bottom, bottom;
  background-origin: content-box, padding-box;
  background-clip: content-box, padding-box;
  background-attachment: scroll, scroll;
  padding-bottom: calc(13% - 1px);
  filter: drop-shadow(10px 10px 10px black);
}
.tree__stvol {
  display: flex;
  flex-direction: column-reverse;
  padding: 0 10px;
  height: 100%;
}
.tree__complect {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  height: 100%;
  justify-content: center;
  align-items: stretch;
  gap: 150px 30px;
  padding-top: 150px;
}
.tree__toy {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 350px;
  height: 350px;
  border-radius: 50%;
  box-shadow: 5px 20px 50px 10px rgb(0, 0, 0);
  position: relative;
  background: #80808048;
  border: 2px #80808048 dashed;
  cursor: pointer;
  animation: toy 5s 0s infinite;
  animation-direction: alternate;
  &:nth-child(4n + 1) {
    animation: toy 5s 0s infinite;
    animation-direction: alternate;
  }
  &:nth-child(3n + 2) {
    animation: toy 7s infinite;
    animation-direction: alternate;
  }
  &:nth-child(2n + 3) {
    animation: toy 9s infinite;
    animation-direction: alternate;
  }
  p {
    color: #fff;
    font-size: 56px;
    line-height: 100%;
    text-align: center;
    font-family: "Great Vibes", serif;
    font-weight: 400;
    font-style: normal;
    margin: 0;
    padding: 0 20px;
  }
  &:nth-child(odd) {
    margin-top: 60px;
  }
  &:first-child {
    margin-top: 20px;
  }
  --red: radial-gradient(
    circle,
    rgba(255, 94, 94, 1) 0%,
    rgba(121, 9, 9, 1) 65%
  );
  --blue: radial-gradient(
    circle,
    rgba(94, 103, 255, 1) 0%,
    rgba(19, 26, 152, 1) 65%
  );
  --green: radial-gradient(
    circle,
    rgb(140, 255, 89, 1) 0%,
    rgb(8, 89, 26, 1) 65%
  );
  --yellow: radial-gradient(
    circle,
    rgba(252, 255, 137, 1) 14%,
    rgba(174, 181, 1, 1) 65%
  );
  --light-blue: radial-gradient(
    circle,
    rgba(147, 225, 255, 1) 14%,
    rgba(20, 118, 186, 1) 65%
  );
  --orange: radial-gradient(
    circle,
    rgba(255, 216, 108, 1) 14%,
    rgba(180, 93, 0, 1) 65%
  );
  --fiolet: radial-gradient(
    circle,
    rgba(218, 149, 255, 1) 14%,
    rgba(110, 0, 157, 1) 65%
  );
}
.tree__toy-ushko {
  position: absolute;
  top: 8%;
  left: 50%;
  transform: translate(-50%, -100%);
  width: 25%;
  &::before {
    position: absolute;
    content: "";
    width: calc(100% - 5px);
    height: 25%;
    bottom: 0;
    left: 50%;
    transform: translate(-50%, 0%);
    border-radius: 30px 30px 50% 50%;
    z-index: -1;
  }
  img {
    width: 100%;
    height: 100%;
  }
}
.tree__toy._red {
  background: var(--red);
  .tree__toy-ushko {
    &::before {
      background: var(--red);
    }
  }
}
.tree__toy._blue {
  background: var(--blue);
  .tree__toy-ushko {
    &::before {
      background: var(--blue);
    }
  }
}
.tree__toy._green {
  background: var(--green);
  .tree__toy-ushko {
    &::before {
      background: var(--green);
    }
  }
}
.tree__toy._yellow {
  background: var(--yellow);
  .tree__toy-ushko {
    &::before {
      background: var(--yellow);
    }
  }
}
.tree__toy._light-blue {
  background: var(--light-blue);
  .tree__toy-ushko {
    &::before {
      background: var(--light-blue);
    }
  }
}
.tree__toy._orange {
  background: var(--orange);
  .tree__toy-ushko {
    &::before {
      background: var(--orange);
    }
  }
}
.tree__toy._fiolet {
  background: var(--fiolet);
  .tree__toy-ushko {
    &::before {
      background: var(--fiolet);
    }
  }
}
.tree__forma {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
}
.tree__form {
  background: #fff;
  padding: 20px;
  border-radius: 20px;
  font-family: "Open Sans", serif;
  small {
    color: red;
    font-size: 18px;
    font-family: "Open Sans", serif;
    margin-bottom: 10px;
    display: block;
  }
}
.tree__form-title {
  font-size: 36px;
  margin-bottom: 30px;
  display: flex;
  align-items: start;
  justify-content: space-between;
  gap: 20px;
  h5 {
    margin: 0;
    font-weight: 600;
  }
  p {
    height: 30px;
    width: 30px;
    font-size: 30px;
    font-weight: 600;
    cursor: pointer;
    padding: 10px;
    border: 2px solid #e03636d0;
    color: #e03636d0;
    border-radius: 50%;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.5s;
    &:hover {
      background: #e03636d0;
      color: #fff;
    }
  }
}
.tree__pole {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
  select {
    height: 40px;
    border: 2px solid #000;
    font-size: 18px;
    border-radius: 10px;
    padding: 0 10px;
  }
  label {
    font-size: 18px;
  }
  input {
    height: 40px;
    font-size: 18px;
    border: 2px solid #000;
    border-radius: 10px;
    padding: 0 10px;
  }
}
.tree__btn {
  width: 100%;
  background: #8cd8fc;
  height: 48px;
  border-radius: 15px;
  color: #1c274c;
  border: 2px solid #1c274c;
  font-size: 18px;
  font-weight: 600;
  cursor: pointer;
}
@keyframes toy {
  0% {
    transform: rotate(-10deg) translate(20%);
  }
  20% {
    transform: rotate(-15deg) translate(30%);
  }
  50% {
    transform: rotate(15deg) translate(-30%);
  }
  // 75% {
  //   transform: rotate(15deg) translate(-30%);
  // }
  80% {
    transform: rotate(-15deg) translate(30%);
  }
  100% {
    transform: rotate(10deg) translate(-20%);
  }
}

.lightrope {
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  z-index: 1;
  margin: -15px 0 0 0;
  padding: 0;
  pointer-events: none;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
}
.lightrope li {
  position: relative;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  -webkit-animation-iteration-count: infinite;
  animation-iteration-count: infinite;
  list-style: none;
  margin: 0;
  padding: 0;
  display: block;
  width: 18px;
  height: 36px;
  border-radius: 50%;
  margin: 20px;
  display: inline-block;
  background: #248b0a;
  box-shadow: 0px 4.66667px 24px 3px #248b0a;
  -webkit-animation-name: flash-1;
  animation-name: flash-1;
  -webkit-animation-duration: 2s;
  animation-duration: 2s;
}
.lightrope li:nth-child(2n + 1) {
  background: #0011ff;
  box-shadow: 0px 4.66667px 24px 3px #0011ff;
  -webkit-animation-name: flash-2;
  animation-name: flash-2;
  -webkit-animation-duration: 0.4s;
  animation-duration: 0.4s;
}
.lightrope li:nth-child(4n + 2) {
  background: #f70000;
  box-shadow: 0px 4.66667px 24px 3px #f70000;
  -webkit-animation-name: flash-3;
  animation-name: flash-3;
  -webkit-animation-duration: 1.1s;
  animation-duration: 1.1s;
}
.lightrope li:nth-child(odd) {
  -webkit-animation-duration: 1.8s;
  animation-duration: 1.8s;
}
.lightrope li:nth-child(3n + 1) {
  -webkit-animation-duration: 1.4s;
  animation-duration: 1.4s;
}
.lightrope li:before {
  content: "";
  position: absolute;
  background: #222;
  width: 10px;
  height: 9.33333px;
  border-radius: 3px;
  top: -4.66667px;
  left: 1px;
}
.lightrope li:after {
  content: "";
  top: -14px;
  left: 9px;
  position: absolute;
  width: 52px;
  height: 18.66667px;
  border-bottom: solid #222 2px;
  border-radius: 50%;
}
.lightrope li:last-child:after {
  content: none;
}
.lightrope li:first-child {
  margin-left: -40px;
}
@-webkit-keyframes flash-1 {
  0%,
  100% {
    background: #248b0a;
    box-shadow: 0px 4.66667px 24px 3px #248b0a;
  }
  50% {
    background: rgba(0, 247, 165, 0.4);
    box-shadow: 0px 4.66667px 24px 3px rgba(0, 247, 165, 0.2);
  }
}
@keyframes flash-1 {
  0%,
  100% {
    background: #248b0a;
    box-shadow: 0px 4.66667px 24px 3px #248b0a;
  }
  50% {
    background: rgb(36, 139, 10, 0.6);
    box-shadow: 0px 4.66667px 24px 3px rgba(0, 247, 165, 0.2);
  }
}
@-webkit-keyframes flash-2 {
  0%,
  100% {
    background: #0011ff;
    box-shadow: 0px 4.66667px 24px 3px #0011ff;
  }
  50% {
    background: rgb(0, 17, 255, 0.4);
    box-shadow: 0px 4.66667px 24px 3px rgba(0, 255, 255, 0.2);
  }
}
@keyframes flash-2 {
  0%,
  100% {
    background: #0011ff;
    box-shadow: 0px 4.66667px 24px 3px #0011ff;
  }
  50% {
    background: rgb(0, 17, 255, 0.4);
    box-shadow: 0px 4.66667px 24px 3px rgba(0, 255, 255, 0.2);
  }
}
@-webkit-keyframes flash-3 {
  0%,
  100% {
    background: #f70000;
    box-shadow: 0px 4.66667px 24px 3px #f70000;
  }
  50% {
    background: rgba(247, 0, 0, 0.4);
    box-shadow: 0px 4.66667px 24px 3px rgba(247, 0, 148, 0.2);
  }
}
@keyframes flash-3 {
  0%,
  100% {
    background: #f70000;
    box-shadow: 0px 4.66667px 24px 3px #f70000;
  }
  50% {
    background: rgba(247, 0, 0, 0.4);
    box-shadow: 0px 4.66667px 24px 3px rgba(247, 0, 148, 0.2);
  }
}
</style>
