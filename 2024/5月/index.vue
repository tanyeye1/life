<template>
  <div class="login">
    <div class="night">
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
      <div class="shooting_star"></div>
    </div>
    <div
      class="form-wrapper"
      v-loading="loading"
      element-loading-text="拼命加载中"
      element-loading-spinner="el-icon-loading"
    >
      <div class="header">
        mall-admin-web
      </div>
      <div class="input-wrapper">
        <div class="border-wrapper">
          <input
            type="text"
            name="username"
            placeholder="请输入用户名"
            class="border-item"
            autocomplete="off"
            v-model="loginForm.username"
          />
        </div>
        <div class="border-wrapper">
          <input
            :type="pwdType"
            name="password"
            placeholder="请输入密码"
            class="border-item"
            autocomplete="off"
            v-model="loginForm.password"
          />
          <span @click="showPwd" class="eye">
            <svg-icon icon-class="eye" class="color-main "></svg-icon>
          </span>
        </div>
      </div>
      <div class="action">
        <div class="btn" @click="handleLogin">
          登录
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { setCookie, getCookie } from "@/utils/support";
export default {
  data() {
    return {
      loginForm: {
        username: "",
        password: ""
      },
      loading: false,
      pwdType: "password"
    };
  },
  created() {
    this.loginForm.username = getCookie("username");
    this.loginForm.password = getCookie("password");
    if (
      this.loginForm.username === undefined ||
      this.loginForm.username == null ||
      this.loginForm.username === ""
    ) {
      this.loginForm.username = "admin";
    }
    if (
      this.loginForm.password === undefined ||
      this.loginForm.password == null
    ) {
      this.loginForm.password = "";
    }
  },
  methods: {
    handleLogin() {
      const { username, password } = this.loginForm;
      if (!username) {
        this.$message({
          message: "请输入用户名",
          type: "warning"
        });
        return;
      }
      if (!password) {
        this.$message({
          message: "请输入密码",
          type: "warning"
        });
        return;
      }
      this.loading = true;
      this.$store
        .dispatch("Login", this.loginForm)
        .then(() => {
          this.loading = false;
          setCookie("username", this.loginForm.username, 15);
          setCookie("password", this.loginForm.password, 15);
          this.$router.push({ path: "/" });
        })
        .catch(() => {
          this.loading = false;
        });
    },
    showPwd() {
      console.log("?");
      if (this.pwdType === "password") {
        this.pwdType = "";
      } else {
        this.pwdType = "password";
      }
    }
  }
};
</script>
<style scoped>
.login {
  height: 100vh;
  overflow: hidden;
  font-family: JetBrains Mono Medium;
  display: flex;
  align-items: center;
  justify-content: center;
  /* background-color: #0e92b3; */
  background: url("../../assets/images/bg1.jpg") no-repeat;
  background-size: 100% 100%;
}
.form-wrapper {
  position: absolute;
  width: 350px;
  background-color: rgba(41, 45, 62, 0.8);
  color: #fff;
  border-radius: 16px;
  padding: 50px;
  overflow: hidden;
}

.form-wrapper .header {
  text-align: center;
  font-size: 30px;
  /* text-transform: uppercase; */
  line-height: 100px;
}

.form-wrapper .input-wrapper input {
  background-color: rgb(41, 45, 62);
  border: 0;
  width: 100%;
  text-align: center;
  font-size: 15px;
  color: #fff;
  outline: none;
}

.form-wrapper .input-wrapper input::placeholder {
  text-transform: uppercase;
}

.form-wrapper .input-wrapper .border-wrapper {
  background-image: linear-gradient(to right, #e8198b, #0eb4dd);
  width: 100%;
  height: 50px;
  margin-bottom: 20px;
  border-radius: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}
.eye {
  position: absolute;
  right: 14px;
}
.form-wrapper .input-wrapper .border-wrapper .border-item {
  height: calc(100% - 4px);
  width: calc(100% - 4px);
  border-radius: 30px;
}

.form-wrapper .action {
  display: flex;
  justify-content: center;
}

.form-wrapper .action .btn {
  width: 60%;
  text-transform: uppercase;
  border: 2px solid #0e92b3;
  text-align: center;
  line-height: 50px;
  border-radius: 30px;
  cursor: pointer;
}

.form-wrapper .action .btn:hover {
  background-image: linear-gradient(120deg, #84fab0 0%, #8fd3f4 100%);
}

.form-wrapper .icon-wrapper {
  text-align: center;
  width: 60%;
  margin: 0 auto;
  margin-top: 20px;
  border-top: 1px dashed rgb(146, 146, 146);
  padding: 20px;
}

.form-wrapper .icon-wrapper i {
  font-size: 20px;
  color: rgb(187, 187, 187);
  cursor: pointer;
  border: 1px solid #fff;
  padding: 5px;
  border-radius: 20px;
}

.form-wrapper .icon-wrapper i:hover {
  background-color: #0e92b3;
}
.night {
  position: relative;
  width: 100%;
  height: 100%;
  -webkit-transform: rotateZ(45deg);
  transform: rotateZ(45deg);
  -webkit-animation: sky 200000ms linear infinite;
  animation: sky 200000ms linear infinite;
}

.shooting_star {
  position: absolute;
  left: 50%;
  top: 50%;
  height: 2px;
  background: linear-gradient(-45deg, #5f91ff, rgba(0, 0, 255, 0));
  border-radius: 999px;
  -webkit-filter: drop-shadow(0 0 6px #699bff);
  filter: drop-shadow(0 0 6px #699bff);
  -webkit-animation: tail 3000ms ease-in-out infinite,
    shooting 3000ms ease-in-out infinite;
  animation: tail 3000ms ease-in-out infinite,
    shooting 3000ms ease-in-out infinite;
}

.shooting_star::before,
.shooting_star::after {
  content: "";
  position: absolute;
  top: calc(50% - 1px);
  right: 0;
  height: 2px;
  background: linear-gradient(
    -45deg,
    rgba(0, 0, 255, 0),
    #5f91ff,
    rgba(0, 0, 255, 0)
  );
  -webkit-transform: translateX(50%) rotateZ(45deg);
  transform: translateX(50%) rotateZ(45deg);
  border-radius: 100%;
  -webkit-animation: shining 3000ms ease-in-out infinite;
  animation: shining 3000ms ease-in-out infinite;
}

.shooting_star::after {
  -webkit-transform: translateX(50%) rotateZ(-45deg);
  transform: translateX(50%) rotateZ(-45deg);
}

.shooting_star:nth-child(1) {
  top: calc(50% - 185px);
  left: calc(50% - 150px);
  -webkit-animation-delay: 8971ms;
  animation-delay: 8971ms;
}

.shooting_star:nth-child(1)::before,
.shooting_star:nth-child(1)::after,
.shooting_star:nth-child(1)::after {
  -webkit-animation-delay: 8971ms;
  animation-delay: 8971ms;
}

.shooting_star:nth-child(2) {
  top: calc(50% - 50px);
  left: calc(50% - 179px);
  -webkit-animation-delay: 9256ms;
  animation-delay: 9256ms;
}

.shooting_star:nth-child(2)::before,
.shooting_star:nth-child(2)::after,
.shooting_star:nth-child(2)::after {
  -webkit-animation-delay: 9256ms;
  animation-delay: 9256ms;
}

.shooting_star:nth-child(3) {
  top: calc(50% - -146px);
  left: calc(50% - 135px);
  -webkit-animation-delay: 8700ms;
  animation-delay: 8700ms;
}

.shooting_star:nth-child(3)::before,
.shooting_star:nth-child(3)::after,
.shooting_star:nth-child(3)::after {
  -webkit-animation-delay: 8700ms;
  animation-delay: 8700ms;
}

.shooting_star:nth-child(4) {
  top: calc(50% - -77px);
  left: calc(50% - 157px);
  -webkit-animation-delay: 3147ms;
  animation-delay: 3147ms;
}

.shooting_star:nth-child(4)::before,
.shooting_star:nth-child(4)::after,
.shooting_star:nth-child(4)::after {
  -webkit-animation-delay: 3147ms;
  animation-delay: 3147ms;
}

.shooting_star:nth-child(5) {
  top: calc(50% - -183px);
  left: calc(50% - 8px);
  -webkit-animation-delay: 6588ms;
  animation-delay: 6588ms;
}

.shooting_star:nth-child(5)::before,
.shooting_star:nth-child(5)::after,
.shooting_star:nth-child(5)::after {
  -webkit-animation-delay: 6588ms;
  animation-delay: 6588ms;
}

.shooting_star:nth-child(6) {
  top: calc(50% - -29px);
  left: calc(50% - 195px);
  -webkit-animation-delay: 8009ms;
  animation-delay: 8009ms;
}

.shooting_star:nth-child(6)::before,
.shooting_star:nth-child(6)::after,
.shooting_star:nth-child(6)::after {
  -webkit-animation-delay: 8009ms;
  animation-delay: 8009ms;
}

.shooting_star:nth-child(7) {
  top: calc(50% - 95px);
  left: calc(50% - 69px);
  -webkit-animation-delay: 5420ms;
  animation-delay: 5420ms;
}

.shooting_star:nth-child(7)::before,
.shooting_star:nth-child(7)::after,
.shooting_star:nth-child(7)::after {
  -webkit-animation-delay: 5420ms;
  animation-delay: 5420ms;
}

.shooting_star:nth-child(8) {
  top: calc(50% - -59px);
  left: calc(50% - 70px);
  -webkit-animation-delay: 9378ms;
  animation-delay: 9378ms;
}

.shooting_star:nth-child(8)::before,
.shooting_star:nth-child(8)::after,
.shooting_star:nth-child(8)::after {
  -webkit-animation-delay: 9378ms;
  animation-delay: 9378ms;
}

.shooting_star:nth-child(9) {
  top: calc(50% - 76px);
  left: calc(50% - 238px);
  -webkit-animation-delay: 2845ms;
  animation-delay: 2845ms;
}

.shooting_star:nth-child(9)::before,
.shooting_star:nth-child(9)::after,
.shooting_star:nth-child(9)::after {
  -webkit-animation-delay: 2845ms;
  animation-delay: 2845ms;
}

.shooting_star:nth-child(10) {
  top: calc(50% - 83px);
  left: calc(50% - 6px);
  -webkit-animation-delay: 5205ms;
  animation-delay: 5205ms;
}

.shooting_star:nth-child(10)::before,
.shooting_star:nth-child(10)::after,
.shooting_star:nth-child(10)::after {
  -webkit-animation-delay: 5205ms;
  animation-delay: 5205ms;
}

.shooting_star:nth-child(11) {
  top: calc(50% - -137px);
  left: calc(50% - 267px);
  -webkit-animation-delay: 808ms;
  animation-delay: 808ms;
}

.shooting_star:nth-child(11)::before,
.shooting_star:nth-child(11)::after,
.shooting_star:nth-child(11)::after {
  -webkit-animation-delay: 808ms;
  animation-delay: 808ms;
}

.shooting_star:nth-child(12) {
  top: calc(50% - 12px);
  left: calc(50% - 8px);
  -webkit-animation-delay: 2406ms;
  animation-delay: 2406ms;
}

.shooting_star:nth-child(12)::before,
.shooting_star:nth-child(12)::after,
.shooting_star:nth-child(12)::after {
  -webkit-animation-delay: 2406ms;
  animation-delay: 2406ms;
}

.shooting_star:nth-child(13) {
  top: calc(50% - 148px);
  left: calc(50% - 47px);
  -webkit-animation-delay: 7566ms;
  animation-delay: 7566ms;
}

.shooting_star:nth-child(13)::before,
.shooting_star:nth-child(13)::after,
.shooting_star:nth-child(13)::after {
  -webkit-animation-delay: 7566ms;
  animation-delay: 7566ms;
}

.shooting_star:nth-child(14) {
  top: calc(50% - -28px);
  left: calc(50% - 75px);
  -webkit-animation-delay: 7634ms;
  animation-delay: 7634ms;
}

.shooting_star:nth-child(14)::before,
.shooting_star:nth-child(14)::after,
.shooting_star:nth-child(14)::after {
  -webkit-animation-delay: 7634ms;
  animation-delay: 7634ms;
}

.shooting_star:nth-child(15) {
  top: calc(50% - -37px);
  left: calc(50% - 203px);
  -webkit-animation-delay: 7743ms;
  animation-delay: 7743ms;
}

.shooting_star:nth-child(15)::before,
.shooting_star:nth-child(15)::after,
.shooting_star:nth-child(15)::after {
  -webkit-animation-delay: 7743ms;
  animation-delay: 7743ms;
}

.shooting_star:nth-child(16) {
  top: calc(50% - 41px);
  left: calc(50% - 256px);
  -webkit-animation-delay: 2888ms;
  animation-delay: 2888ms;
}

.shooting_star:nth-child(16)::before,
.shooting_star:nth-child(16)::after,
.shooting_star:nth-child(16)::after {
  -webkit-animation-delay: 2888ms;
  animation-delay: 2888ms;
}

.shooting_star:nth-child(17) {
  top: calc(50% - -35px);
  left: calc(50% - 121px);
  -webkit-animation-delay: 5864ms;
  animation-delay: 5864ms;
}

.shooting_star:nth-child(17)::before,
.shooting_star:nth-child(17)::after,
.shooting_star:nth-child(17)::after {
  -webkit-animation-delay: 5864ms;
  animation-delay: 5864ms;
}

.shooting_star:nth-child(18) {
  top: calc(50% - 73px);
  left: calc(50% - 225px);
  -webkit-animation-delay: 7883ms;
  animation-delay: 7883ms;
}

.shooting_star:nth-child(18)::before,
.shooting_star:nth-child(18)::after,
.shooting_star:nth-child(18)::after {
  -webkit-animation-delay: 7883ms;
  animation-delay: 7883ms;
}

.shooting_star:nth-child(19) {
  top: calc(50% - -69px);
  left: calc(50% - 47px);
  -webkit-animation-delay: 3339ms;
  animation-delay: 3339ms;
}

.shooting_star:nth-child(19)::before,
.shooting_star:nth-child(19)::after,
.shooting_star:nth-child(19)::after {
  -webkit-animation-delay: 3339ms;
  animation-delay: 3339ms;
}

.shooting_star:nth-child(20) {
  top: calc(50% - 162px);
  left: calc(50% - 129px);
  -webkit-animation-delay: 7963ms;
  animation-delay: 7963ms;
}

.shooting_star:nth-child(20)::before,
.shooting_star:nth-child(20)::after,
.shooting_star:nth-child(20)::after {
  -webkit-animation-delay: 7963ms;
  animation-delay: 7963ms;
}

@-webkit-keyframes tail {
  0% {
    width: 0;
  }

  30% {
    width: 100px;
  }

  100% {
    width: 0;
  }
}

@keyframes tail {
  0% {
    width: 0;
  }

  30% {
    width: 100px;
  }

  100% {
    width: 0;
  }
}

@-webkit-keyframes shining {
  0% {
    width: 0;
  }

  50% {
    width: 30px;
  }

  100% {
    width: 0;
  }
}

@keyframes shining {
  0% {
    width: 0;
  }

  50% {
    width: 30px;
  }

  100% {
    width: 0;
  }
}

@-webkit-keyframes shooting {
  0% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }

  100% {
    -webkit-transform: translateX(300px);
    transform: translateX(300px);
  }
}

@keyframes shooting {
  0% {
    -webkit-transform: translateX(0);
    transform: translateX(0);
  }

  100% {
    -webkit-transform: translateX(300px);
    transform: translateX(300px);
  }
}

@-webkit-keyframes sky {
  0% {
    -webkit-transform: rotate(45deg);
    transform: rotate(45deg);
  }

  100% {
    -webkit-transform: rotate(405deg);
    transform: rotate(405deg);
  }
}

@keyframes sky {
  0% {
    -webkit-transform: rotate(45deg);
    transform: rotate(45deg);
  }

  100% {
    -webkit-transform: rotate(405deg);
    transform: rotate(405deg);
  }
}
</style>
