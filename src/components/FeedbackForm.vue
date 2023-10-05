<template>
  <form class="form">
    <h1 class="form__title">Стать партнером</h1>
    <p class="form__description">
      Мы с радостью проконсультируем Вас по продукту и предложим подходящий
      варинат решения!
    </p>

    <fieldset class="form__fieldset form__fieldset_inputs">
      <label class="form__label">
        Фамилия
        <input
          class="form__input"
          type="text"
          name="surname"
          placeholder="Иванов"
        />
      </label>

      <label class="form__label">
        Имя
        <input class="form__input" type="text" name="name" placeholder="Иван" />
      </label>

      <label class="form__label">
        Отчество
        <input
          class="form__input"
          type="text"
          name="fatherName"
          placeholder="Иванович"
        />
      </label>

      <label class="form__label form__label_city">
        Город
        <input
          class="form__input"
          type="text"
          name="city"
          placeholder="Выберете город"
        />
      </label>

      <label class="form__label">
        Телефон
        <input
          class="form__input"
          type="tel"
          name="tel"
          placeholder="Выберете город"
        />
      </label>
    </fieldset>

    <fieldset class="form__fieldset form__fieldset_files">
      <button class="form__add-files" type="button">
        Прикрепить документы о мед образовании
      </button>
    </fieldset>

    <fieldset class="form__fieldset form__fieldset_checkbox">
      <input class="form__checkbox" type="checkbox" name="checkbox" checked />
      <span class="form__checkbox-custom"></span>
      <p class="form__text">
        Нажимая кнопку «отправить», вы даете согласие на обработку
        <a class="form__link" href="#" target="_blank">персональных данных.</a>
      </p>
    </fieldset>

    <button class="form__submit" type="submit">Отправить</button>
  </form>
</template>

<script>
export default {
  name: "FeedbackForm",
};
</script>

<style lang="scss">
.form {
  flex-grow: 1;
  width: auto;
  max-width: 437px;
  height: 95%;
  display: flex;
  flex-direction: column;
  align-items: start;
  justify-content: space-between;
  box-sizing: border-box;

  @media screen and (max-width: 1024px) {
    padding: 0 32px;
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
    }

    &_files {
      flex-direction: row;
      align-items: center;
      justify-content: space-between;
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

    &_city::after {
      display: block;
      content: "";
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
  }

  &__input {
    width: 100%;
    border: 1px solid #ababab;
    border-radius: 5px;
    box-sizing: border-box;
    padding: 15px 20px;

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

    &__checkbox:checked + &__checkbox-custom::before {
      display: block;
    }
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
    font-weight: 300;
    font-size: 20px;
    font-style: normal;
    line-height: 24px;
    box-sizing: border-box;
    padding: 11px auto;
    cursor: pointer;

    &:hover {
      opacity: 0.5;
    }

    @media screen and (max-width: 1024px) {
      width: 100%;
    }
  }
}
</style>
