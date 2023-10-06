<template>
  <div v-if="!formSubmited" class="form__container">
    <form class="form" @submit.prevent="sumbitHandler">
      <h1 class="form__title">Стать партнером</h1>
      <p class="form__description">
        Мы с радостью проконсультируем Вас по продукту и предложим подходящий
        варинат решения!
      </p>

      <fieldset class="form__fieldset form__fieldset_inputs">
        <label class="form__label">
          Фамилия
          <input
            type="text"
            name="surname"
            placeholder="Иванов"
            v-model="surname"
            :class="{
              form__input: surname.length === 0,
              'form__input form__input_active': surname.length !== 0,
            }"
          />
        </label>

        <label class="form__label">
          Имя
          <input
            class="form__input"
            type="text"
            name="name"
            placeholder="Иван"
            v-model="name"
            :class="{
              form__input: name.length === 0,
              'form__input form__input_active': name.length !== 0,
            }"
          />
        </label>

        <label class="form__label">
          Отчество
          <input
            class="form__input"
            type="text"
            name="fatherName"
            placeholder="Иванович"
            v-model="fatherName"
            :class="{
              form__input: fatherName.length === 0,
              'form__input form__input_active': fatherName.length !== 0,
            }"
          />
        </label>

        <label class="form__label form__label_city">
          Город
          <input
            class="form__input"
            type="text"
            name="city"
            placeholder="Выберете город"
            v-model="city"
            :class="{
              form__input: city.length === 0,
              'form__input form__input_active': city.length !== 0,
            }"
            :mask="Number"
          />
          <button
            type="button"
            class="form__button-select"
            @click="toggleSelectList"
          ></button>
          <ul
            :class="{
              'form__city-list': !isSelectListOpen,
              'form__city-list form__city-list_open': isSelectListOpen,
            }"
          >
            <li
              class="form__city"
              v-for="city in cities"
              :key="city.id"
              @click="selectCityHandler(city.name)"
            >
              {{ city.name }}
            </li>
          </ul>
        </label>

        <label class="form__label">
          Телефон
          <input
            class="form__input"
            type="tel"
            name="tel"
            v-model="tel"
            placeholder="+7 (XXX) XXX XX - XX"
            :class="{
              form__input: tel.length === 0,
              'form__input form__input_active': tel.length !== 0,
            }"
            @input="formatPhone"
            v-imask="mask"
          />
          <span
            class="error error_phone"
            v-if="numberErrorMessage.length > 0"
            >{{ numberErrorMessage }}</span
          >
        </label>
      </fieldset>

      <fieldset class="form__fieldset form__fieldset_files">
        <button class="form__add-files" type="button">
          Прикрепить документы о мед образовании
        </button>
      </fieldset>

      <fieldset class="form__fieldset form__fieldset_checkbox">
        <input
          class="form__checkbox"
          type="checkbox"
          name="checkbox"
          v-model="isChecked"
        />
        <span class="form__checkbox-custom" @click="checkBoxHandler"></span>
        <p class="form__text">
          Нажимая кнопку «отправить», вы даете согласие на обработку
          <a class="form__link" href="#" target="_blank"
            >персональных данных.</a
          >
        </p>
      </fieldset>

      <span class="error" v-if="errorMessage.length > 0">{{
        errorMessage
      }}</span>
      <button
        :class="{
          'form__submit form__submit_disabled': !isFormValidate,
          form__submit: isFormValidate,
        }"
        type="submit"
      >
        Отправить
      </button>
    </form>
  </div>
  <div v-else>
    <p class="form__submited-title">Заявка отправлена</p>
  </div>
</template>

<script>
import { IMaskDirective } from "vue-imask";

export default {
  name: "FeedbackForm",
  data: () => ({
    surname: "",
    name: "",
    fatherName: "",
    city: "",
    tel: "",
    isChecked: false,
    errorMessage: "",
    numberErrorMessage: "",
    formSubmited: false,
    isSelectListOpen: false,
    cities: [
      { id: 1, name: "Москва" },
      { id: 2, name: "Санкт-Петербург" },
      { id: 3, name: "Екатеринбург" },
    ],
    mask: {
      mask: "+7(000)-000-00-00",
    },
  }),
  computed: {
    isFormValidate() {
      return (
        this.surname.length !== 0 &&
        this.name.length !== 0 &&
        this.fatherName.length !== 0 &&
        this.tel.length === 17 &&
        this.city !== 0 &&
        this.isChecked
      );
    },
  },
  directives: {
    imask: IMaskDirective,
  },
  methods: {
    sumbitHandler() {
      this.formSubmited = true;
    },
    checkBoxHandler() {
      this.isChecked = !this.isChecked;
    },
    toggleSelectList() {
      this.isSelectListOpen = !this.isSelectListOpen;
    },
    selectCityHandler(city) {
      this.city = city;
      this.toggleSelectList();
    },
    formatPhone() {
      console.log(this.tel.length)
      const hasLetters = /[a-zA-Z]/.test(this.tel);

      if (hasLetters) {
        this.numberErrorMessage = "Телефон введен некорректно";
      }

      if (!hasLetters) {
        this.numberErrorMessage = "";
      }
    },
  },
};
</script>

<style scoped lang="scss">
.form {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: space-between;

  @media screen and (max-width: 1024px) {
    padding: 0 32px;
    max-height: 770px;
  }

  @media screen and (max-width: 600px) {
    padding-top: 53px;
    justify-content: start;
    max-height: 100%;
  }

  &__container {
    flex-grow: 1;
    width: auto;
    height: 90%;
    max-width: 437px;
    box-sizing: border-box;
    display: flex;
    align-items: center;
    justify-content: center;

    @media screen and (max-width: 1024px) {
      height: 100%;
    }

    @media screen and (max-width: 600px) {
      height: auto;
    }
  }

  &__title {
    text-align: left;
    color: #000000;
    font-weight: 300;
    font-size: 55px;
    font-style: normal;
    margin: 0;
    line-height: 72px;

    @media screen and (max-width: 1024px) {
      font-size: 35px;
      line-height: 46px;
    }
  }

  &__fieldset {
    width: 100%;
    padding: 0;
    border: 0;
    margin: 0;
    display: flex;
    margin: 5px 0;

    &_inputs {
      flex-direction: column;
      align-items: start;
      justify-content: space-between;
      height: 57%;

      @media screen and (max-width: 600px) {
        justify-content: start;
        height: auto;
        gap: 24px;
      }
    }

    &_files {
      flex-direction: row;
      align-items: center;
      justify-content: space-between;

      @media screen and (max-width: 600px) {
        margin: 21px 0 26px;
      }
    }

    &_checkbox {
      margin: 0;
      flex-direction: row;
      align-items: center;
      gap: 11px;
      position: relative;
    }
  }

  &__description {
    text-align: left;
    color: #000000;
    font-weight: 300;
    font-size: 15px;
    font-style: normal;
    line-height: 20px;

    @media screen and (max-width: 600px) {
      margin: 10px 0 27px;
    }
  }

  &__text {
    margin: 0;
    width: 80%;
    font-weight: 300;
    font-size: 15px;
    font-style: normal;
    line-height: 20px;
  }

  &__label {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 9px;
    font-weight: 400;
    font-size: 15px;
    font-style: normal;
    line-height: 20px;
    position: relative;
  }

  &__button-select {
    border: none;
    background-color: transparent;
    padding: 0;
    background-image: url(../assets/select.svg);
    background-repeat: no-repeat;
    background-size: contain;
    width: 28px;
    height: 10px;
    position: absolute;
    top: 48px;
    right: 10px;
    cursor: pointer;
  }

  &__city-list {
    width: auto;
    height: auto;
    position: absolute;
    top: 50%;
    right: 0;
    border: 1px solid #00bcd0;
    padding: 10px;
    list-style: none;
    z-index: 2;
    background-color: white;
    display: none;
    flex-direction: column;
    gap: 3px;
    border-radius: 5px;
    box-shadow: 5px 5px 12px 9px rgba(34, 60, 80, 0.2);

    &_open {
      display: flex;
    }
  }

  &__city {
    width: 100%;
    color: black;
    font-family: "Ubuntu";
    font-weight: 300;
    font-size: 12px;
    font-style: normal;
    line-height: 20px;
    cursor: pointer;
  }

  &__input {
    width: 100%;
    border: 1px solid #ababab;
    border-radius: 5px;
    box-sizing: border-box;
    padding: 15px 20px;

    &_active {
      border: 1px solid #00bcd0;
    }

    &:focus {
      border: 1px solid #00bcd0;
    }

    &:active {
      border: 1px solid #00bcd0;
    }
  }

  &__checkbox {
    background-color: transparent;
    border: none;
    height: 0;
    opacity: 0;
    width: 0;
    margin: 0;
    padding: 0;
    position: absolute;
    top: 0;
    left: 0;
  }

  &__checkbox-custom {
    display: block;
    width: 22px;
    height: 22px;
    border: 1px solid #000000;
    border-radius: 5px;
    position: relative;
    cursor: pointer;

    &::before {
      content: "";
      background-image: url(../assets/check.svg);
      background-repeat: no-repeat;
      background-size: contain;
      width: 16px;
      height: 12px;
      position: absolute;
      top: 5px;
      left: 3px;
      display: none;
    }
  }

  .form__checkbox:checked + .form__checkbox-custom::before {
    display: block;
  }

  &__link {
    color: #00bcd0;
    cursor: pointer;
    text-decoration: underline;
  }

  &__add-files {
    border: none;
    background-color: transparent;
    padding: 0;
    font-weight: 300;
    font-size: 15px;
    font-style: normal;
    line-height: 20px;
    text-decoration: underline;
    display: flex;
    flex-direction: row;
    gap: 13px;
    align-items: center;
    justify-content: center;
    text-align: start;
    cursor: pointer;

    &::before {
      content: "";
      background-image: url(../assets/clip.svg);
      background-size: contain;
      background-repeat: no-repeat;
      display: block;
      width: 29px;
      height: 15px;
    }
  }

  &__submit {
    width: 200px;
    height: 45px;
    background-color: transparent;
    border: 1px solid #00bcd0;
    border-radius: 5px;
    font-family: Ubuntu;
    font-weight: 300;
    font-size: 20px;
    font-style: normal;
    line-height: 24px;
    box-sizing: border-box;
    padding: 11px auto;
    cursor: pointer;

    &:hover {
      border: 2px solid #00bcd0;
    }

    &_disabled {
      opacity: 0.5;
      pointer-events: none;
    }

    @media screen and (max-width: 1024px) {
      width: 100%;
    }

    @media screen and (max-width: 600px) {
      margin: 37px 0 0;
    }
  }

  &__submited-title {
    text-align: center;
    font-weight: 300;
    font-size: 50px;
    line-height: 66px;
  }
}

.error {
  color: red;
  font-family: "Ubuntu";
  font-weight: 300;
  font-size: 12px;
  font-style: normal;
  line-height: 20px;
  position: absolute;
  bottom: -17px;
}
</style>
