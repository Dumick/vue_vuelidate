<template>
  <div class="regist">
    <h2 class="regist__title">Заполните данные</h2>
    <form class="regist__form" @submit.prevent="submitForm">
      <h3 class="regist__form-subtitle">Персональные данные</h3>
      <span class="regist__form-line"></span>

      <section class="regist__form-section">
        <div class="row">
          <v-input
            v-model="person.name.value"
            :text="person.name.title"
            :id="person.name.id"
            :error="msgError.name"
          />
          <v-input
            v-model="person.lastname.value"
            :text="person.lastname.title"
            :id="person.lastname.id"
            :error="msgError.lastname"
          />
        </div>

        <div class="row">
          <v-input
            v-model="person.surname.value"
            :text="person.surname.title"
            :id="person.surname.id"
          />
          <v-input
            v-model="person.birthday.value"
            :text="person.birthday.title"
            :id="person.birthday.id"
            :inputType="person.birthday.type"
          />
        </div>

        <div class="row">
          <v-input
            v-model="person.phone.value"
            :text="person.phone.title"
            :id="person.phone.id"
          />

          <div class="radio_btn">
            <label>
              <input
                type="radio"
                name="gender"
                id="male"
                @change="this.person.gender.value = 'Мужчина'"
              />
              Мужчина
            </label>
            <label>
              <input
                type="radio"
                name="gender"
                id="female"
                @change="this.person.gender.value = 'Женщина'"
              />
              Женщина
            </label>
          </div>
        </div>

        <div class="row">
          <v-select
            v-model="person.doctor.value"
            :options="person.doctor.options"
            :title="person.doctor.title"
          />

          <v-select
            v-model="person.clients.value"
            :isMulty="true"
            :options="person.clients.options"
            :title="person.clients.title"
          />
        </div>

        <label for="SMS" class="SMS">
          <input
            type="checkbox"
            name="SMS"
            id="SMS"
            @change="this.person.SMS = !this.person.SMS"
          />
          Не отправлять SMS
        </label>
      </section>

      <h3 class="regist__form-subtitle">Адрес</h3>
      <span class="regist__form-line"></span>

      <section class="regist__form-section">
        <div class="row">
          <v-input
            v-model="adres.index.value"
            :text="adres.index.title"
            :id="adres.index.id"
          />
          <v-input
            v-model="adres.country.value"
            :text="adres.country.title"
            :id="adres.country.id"
          />
        </div>

        <div class="row">
          <v-input
            v-model="adres.region.value"
            :text="adres.region.title"
            :id="adres.region.id"
          />
          <v-input
            v-model="adres.city.value"
            :text="adres.city.title"
            :id="adres.city.id"
          />
        </div>

        <div class="row">
          <v-input
            v-model="adres.street.value"
            :text="adres.street.title"
            :id="adres.street.id"
          />
          <v-input
            v-model="adres.home.value"
            :text="adres.home.title"
            :id="adres.home.id"
          />
        </div>
      </section>

      <h3 class="regist__form-subtitle">Паспорт</h3>
      <span class="regist__form-line"></span>

      <section class="regist__form-section">
        <div class="row">
          <v-select
            v-model="passport.document.value"
            :options="passport.document.options"
            :title="passport.document.title"
          />
        </div>

        <div class="row">
          <v-input
            v-model="passport.series.value"
            :text="passport.series.title"
            :id="passport.series.id"
          />
          <v-input
            v-model="passport.number.value"
            :text="passport.number.title"
            :id="passport.number.id"
          />
        </div>

        <div class="row">
          <v-input
            v-model="passport.who.value"
            :text="passport.who.title"
            :id="passport.who.id"
          />
          <v-input
            v-model="passport.when.value"
            :text="passport.when.title"
            :id="passport.when.id"
          />
        </div>
      </section>

      <button type="submit">Отправить</button>
    </form>
  </div>
</template>

<script>
import vInput from "./components/v-input.vue";
import vSelect from "./components/v-select.vue";

import useVuelidate from "@vuelidate/core";
import { required, maxLength } from "@vuelidate/validators";

export default {
  name: "App",
  components: {
    vInput,
    vSelect,
  },
  setup: () => ({ v$: useVuelidate() }),
  data() {
    return {
      person: {
        name: {
          id: "name",
          value: "",
          title: "Имя",
        },
        lastname: {
          id: "lastname",
          value: "",
          title: "Фамиля",
        },
        surname: {
          id: "surname",
          value: "",
          title: "Отчество",
        },
        birthday: {
          id: "birthday",
          value: "",
          title: "Дата рождения",
          type: "date",
        },
        phone: {
          id: "phone",
          value: "",
          title: "Номер телефона",
        },
        gender: {
          id: "gender",
          value: "",
          title: "Пол",
        },
        clients: {
          id: "clients",
          options: { vip: "VIP", problems: "Проблемные", OMS: "ОМС" },
          value: [],
          title: "Группа клиентов",
        },
        doctor: {
          id: "doctor",
          options: {
            ivanov: "Иванов",
            zaharov: "Захаров",
            chenisheva: "Ченышева",
          },
          value: "",
          title: "Лечащий врач",
        },
        SMS: false,
      },
      adres: {
        index: {
          id: "index",
          value: "",
          title: "Индекс",
        },
        country: {
          id: "country",
          value: "",
          title: "Страна",
        },
        region: {
          id: "region",
          value: "",
          title: "Область",
        },
        city: {
          id: "city",
          value: "",
          title: "Город",
        },
        street: {
          id: "street",
          value: "",
          title: "Улица",
        },
        home: {
          id: "home",
          value: "",
          title: "Дом",
        },
      },
      passport: {
        document: {
          id: "document",
          options: {
            passport: "Паспорт",
            birthday: "Свидетельство о рождении",
            draving: "Вод. удостоверение",
          },
          value: "",
          title: "Документ",
        },
        series: {
          id: "series",
          value: "",
          title: "Серия",
        },
        number: {
          id: "number",
          value: "",
          title: "Номер",
        },
        who: {
          id: "who",
          value: "",
          title: "Кем выдан",
        },
        when: {
          id: "when",
          value: "",
          title: "Дата выдачи",
        },
      },
      msgError: {
        name: "",
        lastname: "",
        surname: "",
        birthday: "",
        phone: "",
        clients: "",
        city: "",
        document: "",
        series: "",
        number: "",
        when: "",
      },
    };
  },
  /*computed: {
    nameError() {
      if (this.v$.person.name.hasCirilikSymbol.$invalid)
        this.msgError.name = "Можно использовать только кирилицу";

      if (this.v$.person.name.required.$invalid)
        this.msgError.name = "Этот поле обязательно для заполнения";
    },
    lastnameError() {
      if (this.v$.person.lastname.required.$invalid)
        this.msgError.lastname = "Этот поле обязательно для заполнения";

      if (this.v$.person.lastname.hasCirilikSymbol.$invalid)
        this.msgError.lastname = "Можно использовать только кирилицу";
    },
    surnameError() {
      if (this.v$.person.surname.hasCirilikSymbol.$invalid)
        this.msgError.surname = "Можно использовать только кирилицу";
    },
    birthdayError() {
      if (this.v$.person.birthday.required.$invalid)
        this.msgError.birthday = "Этот поле обязательно для заполнения";
    },
    phoneError() {
      if (this.v$.person.phone.required.$invalid)
        this.msgError.phone = "Этот поле обязательно для заполнения";

      if (this.v$.person.phone.hasCirilikSymbol.$invalid)
        this.msgError.phone = "Можно использовать только кирилицу";
    },
    clientsError() {
      if (this.v$.person.clients.required.$invalid)
        this.msgError.clients = "Этот поле обязательно для заполнения";
    },
    cityError() {
      if (this.v$.adres.city.required.$invalid)
        this.msgError.city = "Этот поле обязательно для заполнения";
    },
    documentError() {
      if (this.v$.passport.document.required.$invalid)
        this.msgError.document = "Этот поле обязательно для заполнения";
    },
    seriesError() {
      if (this.v$.passport.series.maxLength.$invalid)
        this.msgError.document = "Серия паспотра должен состоять из 4 цифр";
    },
    numberError() {
      if (this.v$.passport.number.maxLength.$invalid)
        this.msgError.document = "Номер паспотра должен состоять из 6 цифр";
    },
    whenError() {
      if (this.v$.passport.when.required.$invalid)
        this.msgError.when = "Этот поле обязательно для заполнения";
    },
  },*/

  validations() {
    const hasNumberPhone = (val) =>
      /(^7)((\d{10})|(\s\(\d{3}\)\s\d{3}\s\d{2}\s\d{2}))/.test(val);
    const hasCirilikSymbol = (val) => /[а-яА-Я]/.test(val);

    return {
      person: {
        name: { required, hasCirilikSymbol },
        lastname: { required, hasCirilikSymbol },
        surname: { hasCirilikSymbol },
        birthday: { required },
        phone: { required, hasNumberPhone },
        clients: { required },
      },
      adres: {
        city: { required },
      },
      passport: {
        document: { required },
        series: { maxLength: maxLength(4) },
        number: { maxLength: maxLength(6) },
        when: { required },
      },
    };
  },
  methods: {
    submitForm() {
      this.v$.$validate();

      if (this.v$.$error) console.log("Form not valid");
      else console.log("Form valid");
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,400;0,500;1,400&family=Rubik&display=swap");

$main_bgc: #252525;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Roboto", sans-serif;
  background-color: $main_bgc;
}
.regist {
  width: 1100px;
  padding: 20px;
  margin: 20px auto;

  color: #fff;
  text-align: center;

  &__form-subtitle {
    margin-top: 40px;
  }

  &__form-line {
    width: 60%;
    height: 2px;
    display: block;

    margin: 10px auto;
    background-color: #fff;
  }

  &__form-section {
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;

    .row {
      width: 60%;
      display: flex;
      justify-content: space-around;

      margin-top: 30px;
    }

    .radio_btn {
      display: flex;
      align-items: center;
      justify-content: space-around;
      width: 250px;
    }
    .SMS {
      margin-top: 40px;
    }
  }
  button[type="submit"] {
    cursor: pointer;
    margin-top: 20px;
    padding: 8px 24px;
    font-size: 18px;
    border: none;
    border-radius: 4px;
    transition: 0.2s;

    &:hover {
      background-color: rgb(99, 127, 255);
    }
  }
}
</style>
