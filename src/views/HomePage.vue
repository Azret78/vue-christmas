<template>
  <button class="index__help" @click="open">?</button>
  <div class="index__alert" v-if="openModal">
    <div class="index__alert-body">
      <div class="index__alert-title">
        <p>
          Добро пожаловать в веб-приложение <br />
          <span>„Новогодняя Ёлка“</span>
        </p>
        <div class="index__alert-close" @click="close">X</div>
      </div>
      <div class="index__alert-text">
        <p>
          Вам предстоит украсить новогодняя ёлку игрушку. У вас будет
          возможность самостоятельно выбрать цвет, а также текст для
          елочной игрушки.
        </p>
        <p>
          Команда ООО <span><i>„Моя Оборона“</i></span> с радостью рассмотрит
          ваши идеи и предложения по улучшению данного приложения. Напишите нам
          в телеграм и опишите вашу идею
        </p>
      </div>
    </div>
  </div>
  <div class="main__index">
    <div class="index__card">
      <div class="index__title">
        <h1>Новогодняя Ёлка</h1>
        <div class="index__img">
          <picture>
            <img src="../../public/head.png" alt="" />
          </picture>
        </div>
      </div>
      <div class="index__text">
        <p>Вы находитесь в приложении по украшению ёлки</p>
        <p>
          Создавайте новогоние игрушки. Выбирайте им цвет, а также текст
        </p>
      </div>
    </div>
    <div class="index__form">
      <div class="index__pole">
        <label for="index__name">Ваше имя: {{ yourName }}</label>
        <input type="text" placeholder="Введите имя" v-model="yourName" />
      </div>
      <small v-if="thankYou"
        >Спасибо, <i>{{ name }}</i
        >, ваши данные сохранены в этом обновлении
        <span
          >Предпреждение !!! При обновлении страницы данные нужно будет вводить
          повторно</span
        ></small
      >
      <div class="index__btns">
        <button
          class="index__btn"
          :class="yourName.length === 0 ? '_blocked' : ''"
          @click="addName"
          :disabled="yourName.length === 0"
        >
          Сохранить
        </button>
        <router-link v-if="thankYou" to="/christmas">Нарядить ёлку</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      yourName: '',
      name: '',
      thankYou: false,
      openModal: false
    }
  },
  methods: {
    addName () {
      if (this.yourName.length !== 0) {
        this.name = this.yourName
        this.thankYou = true
      }
    },
    open () {
      this.openModal = true
    },
    close () {
      this.openModal = false
    }
  }
}
</script>

<style lang="scss" scoped>
.index__card {
  display: flex;
  flex-direction: column;
  padding: 30px 20px 20px 20px;
  border-radius: 20px;
  background: #fff;
  position: relative;
  margin-top: 150px;
  box-shadow: 5px 10px 20px rgba(206, 206, 206, 0.596);
  &::before {
    position: absolute;
    content: "";
    background: url("../../public/girlyanda.png") repeat-x;
    width: 100%;
    height: 150px;
    background-position: top;
    background-size: 50% auto;
    background-origin: content-box;
    background-clip: content-box;
    background-attachment: scroll;
    top: -8px;
    left: 0;
  }
}
.index__title {
  font-family: "Great Vibes", serif;
  font-weight: 400;
  font-style: normal;
  font-size: 65px;
  padding-bottom: 20px;
  position: relative;
}
.index__img {
  position: absolute;
  width: 15%;
  top: 0;
  left: 50%;
  transform: rotateY(180deg) translate(50%, -50%);
  img {
    width: 100%;
    height: auto;
    object-fit: contain;
  }
}
.index__text {
  font-family: "Open Sans", serif;
  font-size: 20px;
  padding-top: 20px;
  border-top: 2px solid #1c274c;
}
.index__help {
  position: fixed;
  right: 20px;
  bottom: 80px;
  width: 80px;
  height: 80px;
  background: #aaebff;
  border-radius: 15px;
  border: 2px solid #1c274c;
  color: #1c274c;
  font-family: "Open Sans", serif;
  font-weight: 600;
  font-size: 36px;
  cursor: pointer;
  transition: all 0.5s;
  &:hover {
    transform: scale(1.05);
    box-shadow: 5px 10px 30px rgba(206, 206, 206, 0.596);
  }
}
.index__form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin: 20px 0;
  font-family: "Open Sans", serif;
  .index__pole {
    display: flex;
    flex-direction: column;
    gap: 10px;
    label {
      font-size: 24px;
      color: #fff;
    }
    input {
      width: 500px;
      padding: 13px 20px 15px 20px;
      font-size: 18px;
      border-radius: 15px;
      border: 2px solid #1c274c;
    }
  }
  .index__btn {
    width: 300px;
    padding: 13px 20px 15px 20px;
    font-size: 18px;
    border-radius: 15px;
    border: 2.5px solid #1c274c;
    color: #1c274c;
    font-weight: 600;
    background: #aaebff;
    cursor: pointer;
  }
  .index__btn._blocked {
    cursor: not-allowed;
    background: rgb(170, 235, 255, 0.8);
  }
  small {
    color: rgb(20, 219, 20);
    font-weight: 600;
    font-size: 14px;
    font-family: "Open Sans", serif;
    padding: 10px 20px;
    border-radius: 10px;
    background: #fff;
    width: 500px;
    border: 2px solid #1c274c;
    span {
      color: red;
    }
  }
}
.index__btns {
  display: flex;
  align-items: center;
  gap: 50px;
  a {
    width: 150px;
    background: #fff;
    padding: 13px 20px 15px 20px;
    text-align: center;
    font-size: 18px;
    border-radius: 15px;
    border: 2px solid #1c274c;
    text-decoration: none;
    font-weight: 600;
    color: #1c274c;
    transition: all 0.5s;
    &:hover {
      background: #fe3636d0;
      color: #fff;
      border: 2px solid #fff;
    }
  }
}
.index__alert {
  display: flex;
  align-items: center;
  justify-content: center;
  background: #00000091;
  position: fixed;
  width: 100%;
  height: 100%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 5;
}
.index__alert-body {
  display: flex;
  flex-direction: column;
  background: #fff;
  padding: 20px;
  border-radius: 20px;
  width: 100%;
  max-width: 1000px;
  font-family: "Open Sans", serif;
  color: #1c274c;
}
.index__alert-title {
  padding-bottom: 20px;
  border-bottom: 2px solid #1c274c;
  font-weight: 600;
  font-size: 36px;
  display: flex;
  align-items: start;
  gap: 20px;
  justify-content: space-between;
  span {
    font-family: "Great Vibes", serif;
    font-style: normal;
    font-size: 65px;
  }
}
.index__alert-close {
  cursor: pointer;
  color: #fe3636d0;
  width: 30px;
  height: 30px;
  min-width: 30px;
  min-height: 30px;
  border: 2px solid #fe3636d0;
  border-radius: 50%;
  font-size: 20px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.5s;
  &:hover {
    color: #fff;
    background: #fe3636d0;
  }
}
.index__alert-text {
  padding-top: 20px;
  font-size: 18px;
  span {
    font-size: 20px;
    font-weight: 600;
  }
}
</style>
