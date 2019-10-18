<template>
  <div class="animated fadeIn">
    <nav class="navbar">
      <a class="navbar-brand">
        <h4>
          <b>開發人員資料</b>
        </h4>
      </a>
    </nav>

    <b-card no-body class="card-default">
      <b-card-body>
        <form>
          <div class="form-group row">
            <label for="inputName" class="col-sm-2 col-form-label">名字</label>
            <div class="col-sm-10">
              <input
                type="text"
                class="form-control"
                id="inputName"
                placeholder="Name"
                required
                v-model="name"
              />
            </div>
          </div>

          <div class="form-group row">
            <label for="inputUser" class="col-sm-2 col-form-label">身分證字號</label>
            <div class="col-sm-10">
              <input
                type="text"
                class="form-control"
                id="inputUser"
                placeholder="請輸入身分證"
                pattern="^[A-Z][1,2]\d{8}$"
                required
                v-model="idNumber"
              />
            </div>
          </div>

          <div class="form-group row">
            <label
              for="inputPhone"
              class="col-sm-2 col-form-label"
            >電話</label>
            <div class="col-sm-10">
              <input
                type="text"
                class="form-control"
                id="inputPhone"
                placeholder="09xxxxxxxx"
                pattern="^09\d{8}$"
                required
                v-model="phone"
              />
                <!-- name="phone"
                v-bind:class="{ 'is-invalid': phoneError }" -->
              <!-- <div class="invalid-feedback">
                {{ phoneErrMsg }}
              </div> -->
            </div>
          </div>

          <div class="form-group row">
            <label for="inputEmail" class="col-sm-2 col-form-label">E-mail</label>
            <div class="col-sm-10">
              <input
                type="email"
                class="form-control"
                id="inputEmail"
                placeholder="xxx@gmail.com"
                pattern="^.*@gmail\.com$"
                required
                v-model="email"
              />
            </div>
          </div>

          <div class="form-group row">
            <label for="inputPsw" class="col-sm-2 col-form-label">密碼</label>
            <div class="col-sm-10">
              <input
                type="password"
                class="form-control"
                id="inputPsw"
                placeholder="至少8-12位英數的密碼限制"
                pattern="[a-zA-Z0-9]{8,12}"
                required
                v-model="password"
              />
                <!-- name="password"
                v-bind:class="{ 'is-invalid': passwordError }" -->
              <!-- <div class="invalid-feedback">
                {{ passwordErrMsg }}
              </div> -->

            </div>
          </div>

          <div style="text-align: center">
            <button type="submit" class="btn btn-primary" @click="submitButton">確認送出</button>
          </div>
        </form>
      </b-card-body>
    </b-card>
  </div>
</template>
<script>
import EventService from "@/service/EventService.js";
export default {
  data() {
    return {
      // input: {
        name: "",
        // nameOk: "",
        phone: "",
        // phoneError: false,
        // phoneErrMsg: "",
        email: "",
        idNumber: "",
        password: "",
        // passwordError: false,
        // passwordErrMsg: "",
      // }
    };
  },
  // computed: {
  //   nameOk() {
  //     return this.name;
  //   }
  // },
  // watch: {
  //       password: function () {
  //           var isText = /^[a-zA-Z0-9]+$/;
  //           var inclde = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,15}$/;
  //           // if (!isText.test(this.password)) {
  //           //     this.passwordError = true;
  //           //     this.passErrMsg = '請勿包含特殊字元';
  //           // }
  //           if (this.password.length < 8) {
  //               this.passwordError = true;
  //               // this.passErrMsg = '請勿少於6個字';
  //           }
  //           else if (this.password.length > 12) {
  //               this.passwordError = true;
  //               // this.passErrMsg = '請勿超過15個字';
  //           }
  //           else if (!isText.test(this.password)) {
  //               this.passwordError = true;
  //               // this.passErrMsg = '至少包括一個大小寫字母或數字';
  //           }
  //           else {
  //               this.passwordError = false;
  //           }
  //       },
  // },
  methods: {
    submitButton() {

      // var nameR = /required/;
      var phoneR = /^09\d{8}$/;
      var emailR = /^.*@gmail\.com$/;
      var idNumberR = /^[A-Z][1,2]\d{8}$/;
      // var passwordR = /[a-zA-Z0-9]{8,12}/
      // var passwordR = /[a-zA-Z0-9]/;
      var passwordR = /^[a-zA-Z0-9]{8,12}$/

      // console.log(this.input.name);
      // console.log(this.input.phone);
      // console.log(this.input.email);
      // console.log(this.input.idNumber);
      // console.log(this.input.password);
      // let { name, phone, email, idNumber, password } = this.input;
      // category

      // if(this.name != 0 && phoneR.test(this.phone) && emailR.test(this.email) && idNumberR.test(this.idNumber) && passwordR.test(this.password)) {
      // if(this.name != 0 && phoneR.test(this.phone) && emailR.test(this.email) && idNumberR.test(this.idNumber) && passwordR.test(this.password) && 7 < this.password.length < 13) {
      if(this.name != 0 && phoneR.test(this.phone) && emailR.test(this.email) && idNumberR.test(this.idNumber) && passwordR.test(this.password)) {
        this.axios
          .post("http://127.0.0.1:8000/api/Admin/newDeveloper", {name:this.name, phone:this.phone, email:this.email, idNumber:this.idNumber, password:this.password})
          .then(res => {
            console.log(res.data);
            this.name = "";
            this.phone = "";
            this.email = "";
            this.idNumber = "";
            this.password = "";
          })
          .catch(error => {
            console.log(error);
          });
        alert("新增開發者成功");
      }

    }
  }
};
</script>