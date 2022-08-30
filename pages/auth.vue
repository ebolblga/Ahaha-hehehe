<script setup lang="ts">
import { useI18n } from 'vue-i18n';

const { t } = useI18n()
const title = computed(() => t("title"))
useHead({ title });
const supabase = useSupabaseClient()

const email = ref('')
const message = ref("")
const isError = ref(false)
const Auth = async () => {
  try {
    isError.value = false
    message.value = t("loading")
    const { error } = await supabase.auth.signIn({ email: email.value })
    if (error) throw error
    message.value = t("okText")
  } catch (error) {
    isError.value = true
    let text = error.error_description || error.message
    if(text == "You must provide either an email, phone number, a third-party provider or OpenID Connect.")
      text = t("errorText")
    message.value = text
  } 
}

</script>

<template>
  <div>
    <div class="authForm">
      <div class="flex justify-center"><img src="/Logo.png"></div>
      <auth-input type="email" v-model="email" :placeholder="t('emailPlaceholder')" />
      <auth-button :value="t('signIn')" @click="Auth" />
      <div class="text-md mt-3" :class="{'text-red-600':isError,'text-green-400':!isError}">{{message}}</div>
    </div>
  </div>
</template>

<i18n>
  {
    "en":{
      "title":"Authorization",
      "emailPlaceholder":"Enter Email",
      "signIn":"Sign In",
      "okText":"Check your email for the login link!",
      "errorText":"You must provide either an email, phone number, a third-party provider or OpenID Connect.",
      "loading":"loading..."
    },
    "ru":{
      "title":"Авторизация",
      "emailPlaceholder":"Введите email",
      "signIn":"Войти",
      "okText":"Проверьте email, туда отправлена ссылка для авторизации",
      "errorText":"Вы должны указать либо адрес электронной почты, номер телефона, стороннего поставщика услуг, либо OpenID Connect.",
      "loading":"загрузка..."
    }
  }
</i18n>
<style scoped lang="scss">
.authForm {
  width: 21.5vw;
  /*height: 29.3vw;*/
  margin-left: 39.2vw;
  margin-top: 10.7vw;
  background: #FFFFFF;
  -webkit-box-shadow: 0.1vw 0.2vw 0.4vw rgba(0, 0, 0, 0.25);
  box-shadow: 0.1vw 0.2vw 0.4vw rgba(0, 0, 0, 0.25);
  border-radius: 1vw;
  padding: 1.87vw;
  line-height: 1;

  input {
    width: 17.78vw;
    height: 3.47vw;
    border-radius: 1.735vw;
    margin-top: 1.46vw;
    border: 0.1vw solid #797979;
    -webkit-box-sizing: border-box;
    box-sizing: border-box;
    border-radius: 2vw;
    font-size: 1vw;
    color: rgba(55, 63, 65, 0.61);
    padding: 0vw 1vw;
  }
}


input[type=button],
input[type=submit] {
  background: #79D4FC;
  -webkit-box-shadow: 0.1vw 0.2vw 0.4vw rgba(0, 0, 0, 0.25);
  box-shadow: 0.1vw 0.2vw 0.4vw rgba(0, 0, 0, 0.25);
}

.authForm img {
  width: 12.3vw;
  margin-bottom: 0.5vw;
}
</style>