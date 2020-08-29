<template>
  <div>
    <form v-on:submit.prevent="submitForm">
      <div>
        <label for="username">ID:</label>
        <input
          id="username"
          type="text"
          v-model="username"
          class="username-input"
          v-bind:class="{ 'error': isError }"
        />
      </div>
      <div>
        <label for="password">PW:</label>
        <input id="password" type="password" v-model="password" />
      </div>
      <button v-bind:disabled="!isUsernameValid" type="submit">로그인</button>
    </form>

    <p v-if="isError">올바르지 않은 ID입니다.</p>
    <p v-if="isUsernameValid">이메일 형식이 맞습니다.</p>
  </div>
</template>

<script>
function validateEmail(email) {
  const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

  return re.test(String(email).toLowerCase());
}
export default {
  data() {
    return {
      username: "",
      password: "",
      isError: false,
      isSuccess: false, //1)
    };
  },
  computed: {
    isUsernameValid() {
      return validateEmail(this.username);
    },
  },
  methods: {
    submitForm() {
      console.log("로그인");
      this.isSuccess = true; //1-1)
      // this.isError = true;
      //this.initForm();
    },
    initForm() {
      this.username = "";
      this.password = "";
    },
  },
};

/*
1) submitForm을 했을때, 완료되었음을 추가
  1-1)에 true로 변경해줌
  ⇒ 브라우저에서 vue devtool에서 보면, 로그인 버튼 누르면 data에 isSuccess가 true로 변경되는걸 볼 수 있음
2) components폴더에 popup UI를 만들어서 App.vue에서 사용해줌
  + 일반적으로 vue에서의 컴포넌트는 components폴더 밑에 데이터의 성격 / 페이지나 도메인별로 구별해서 폴더별로 만들어서 정리함. 
  ⇒ 여기서는 components > ToastPopup.vue 파일을 만들어서 작성함(ToastPopup.vue에서 계속)



6) script태그 밑에서 vim을 입력하면 snippet에 의해 import할수있는 명령어가 생성됨 
  ⇒ import New from '@/components/New.vue';
  6-1) ToastPopup파일을 불러와서 ToastPopup이라는 변수안에 넣어줬다는 의미임
  ⇒ 이게 바로 es6의 import구문임
7) export default()에 components로 ToastPopup을 등록해줌
  ⇒ 원래는 'ToastPopup' : ToastPopup 형태인데,  (문자열 : 변수 형태)
  객체에서 key의 경우 문자열은 ''없이 작성해도 되고, 그러면 ToastPopup:ToastPopup으로 같은 문자가 되므로 ES6에서는 축약해도 됨
8) 화면에 표시하기 위해 ToastPopup 마크업해줌
  ⇒ HTML이 대소문자를 구분하지 않으므로 <toast-popup></toast-popup>으로 작성해도 됨 
  ⇒ 브라우저에 토스트팝업이라는 텍스트가 보여짐
*/
</script>

<style scoped>
.username-input {
  outline: none;
}
.username-input.error {
  border: 1px solid red;
}
</style>
