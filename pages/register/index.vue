<template>
  <div>
    <v-app-bar color="primary" dense flat dark>
      <v-toolbar-title>ลงทะเบียน</v-toolbar-title>
    </v-app-bar>
    <v-container class="pt-0 pb-0">
      <v-row>
        <v-col cols="12">
          <div class="mt-8 text-primary text-title text-center">Step 1 of 2</div>
        </v-col>
        <v-col cols="12" class="text-center pt-0 pb-0">
          <img class="image-cropper" src="~/assets/images/profile.jpg" alt width="155" />
        </v-col>
        <v-col cols="12" class="text-center pt-2 pb-0">Display Name</v-col>
        <v-col>
          <v-form>
            <v-text-field v-model="form.firstname" dense label="ชื่อ" required></v-text-field>
            <v-text-field v-model="form.lastname" dense label="นามสกุล" required></v-text-field>
            <div class="type-group d-flex mt-3">
              <p>ประเภท</p>
              <div class="circle">
                <span
                  class="icon icon-shop"
                  :class="form.type == 1 ? 'active' : ''"
                  @click="chooseType(1)"
                ></span>
              </div>
              <p>ร้านค้า</p>
              <div class="circle">
                <span
                  class="icon icon-consumer"
                  :class="form.type == 2 ? 'active' : ''"
                  @click="chooseType(2)"
                ></span>
              </div>
              <p>ผู้ซื้อ</p>
            </div>
            <v-btn rounded color="primary" dark class="w-100 mt-9 my-btn" @click="next">ถัดไป</v-btn>
          </v-form>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      form: {
        firstname: this.$store.getters.getRegister.firstname,
        lastname: this.$store.getters.getRegister.lastname,
        type: this.$store.getters.getRegister.type,
      }
    };
  },
  methods: {
    chooseType(type) {
      this.form.type = type;
    },
    validate() {
      let validated = true;
      const errors = [];
      const validatorField = ["firstname", "lastname"];
      validatorField.forEach(field => {
        if (this.form[field] == "") {
          validated = false;
          errors.push(`กรุณาใส่ข้อมูล ${field}`);
        }
      });
      if (!validated) {
        this.dialog = true;
        this.$store.dispatch('setDialog',{
          isShow:true,
          title:'คำเตือน',
          message:errors.map(error => error + "<br/>").join("")
        })
      }
      return validated;
    },
    next() {
      if (this.validate()) {
        this.$store.dispatch("setRegister", this.form);
        this.$router.push("/register/step2");
      }
    }
  }
};
</script>
<style lang="scss" scoped>
.image-cropper {
  width: 150px;
  height: 150px;
  position: relative;
  overflow: hidden;
  border-radius: 50%;
  border: 1px solid gray;
}

img {
  display: inline;
  margin: 0 auto;
  height: 100%;
  width: auto;
}
.v-form {
  padding: 0 10px;
}

.type-group {
  p {
    margin-bottom: 0;
    align-self: center;
    margin-right: 20px;
  }
  .circle {
    width: 45px;
    height: 45px;
    margin-right: 7px;
  }
}

.icon {
  display: inline-block;
  width: 45px;
  height: 45px;
  background-size: cover;
}
.icon-shop {
  background-image: url("../../assets/icons/shop.svg");
}
.icon-shop.active {
  background-image: url("../../assets/icons/shop-active.svg");
}
.icon-consumer {
  background-image: url("../../assets/icons/consumer.svg");
}
.icon-consumer.active {
  background-image: url("../../assets/icons/consumer-active.svg");
}
.my-btn {
  font-size: 20px !important;
  text-transform: none !important;
  height: auto !important;
  padding: 10px 0 !important;
  font-weight: bold;
}
</style>
