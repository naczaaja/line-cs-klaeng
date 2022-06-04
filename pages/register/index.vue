<template>
  <div>
    <v-app-bar color="primary" dense flat dark>
      <v-toolbar-title>ลงทะเบียน</v-toolbar-title>
    </v-app-bar>

    <v-container>
      <v-row>
        <v-col cols="12">
          <div class="stepsBox text-primary text-title text-center">
            ขั้นตอนที่ 1 จาก 2
          </div>
        </v-col>
        <v-col cols="12" class="profilePadTop text-center">
          <img src="~/assets/profile.png" alt="" width="155">
        </v-col>
        <v-col cols="12" class="text-center">
          Display Name
        </v-col>
        <v-col cols="12">
          <v-form>
            <!-- Firstname input -->
            <v-text-field v-model="form.firstname" dense label="ชื่อ" required>
            </v-text-field>
            <!-- Lastname input -->
            <v-text-field v-model="form.lastname" dense label="สกุล" required>
            </v-text-field>
            <!-- Firstname input -->
            <v-text-field v-model="form.email" dense label="อีเมล">
            </v-text-field>
            <!-- Firstname input -->
            <v-text-field v-model="form.telephone" dense label="เบอร์โทรศัพท์" required>
            </v-text-field>
            <!-- gender field -->
            <div class="gender-group d-flex mt-3">
              <p>เพศ</p>
              <div class="circle" :class="form.gender == 1 ? 'active' : ''" @click="chooseGender(1)">
                <img src="~/assets/male.png" alt="" width="30px">
              </div>
              <p>ชาย</p>
              <div class="circle" :class="form.gender == 2 ? 'active' : ''" @click="chooseGender(2)">
                <img src="~/assets/female.png" alt="" width="30px">
              </div>
              <p>หญิง</p>
            </div>
            <!-- Rounded button -->
            <v-btn rounded color="primary" dark class="w-100 mt-10 my-btn" @click="next()">
              ต่อไป
            </v-btn>
          </v-form>
        </v-col>
      </v-row>
    </v-container>
    <v-dialog v-model="dialog" max-width="290">
      <v-card>
        <v-card-title class="warningPopup">แจ้งเตือน</v-card-title>
        <v-card-text v-html="errorMsg">
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      dialog: false,
      errorMsg: '',
      form: {
        firstname: '',
        lastname: '',
        email: '',
        telephone: '',
        gender: 1
      }
    }
  },
  methods: {
    chooseGender(gender) {
      this.form.gender = gender
    },
    // ตรวจสอบค่าว่างใน input
    validate() {
      let validated = true
      const errors = []
      const validatorField = [
        'firstname',
        'lastname',
        'telephone'
      ]
      validatorField.forEach((field) => {
        if (this.form[field] == '') {
          validated = false
          errors.push(`คุณยังไม่ได้กรอก ${field}`)
        }
      })
      if (!validated) {
        this.errorMsg = errors.map((error) => error + '<br/>').join('')
        this.dialog = true
      }
      return validated
    },
    next() {
      if (this.validate()) {
        this.$router.push('/register/step2')
      }
    }
  },
}
</script>

<style lang="scss" scoped>
.stepsBox {
  padding-top: 38px;
}

.profilePadTop {
  padding-top: 18px;
}

.v-form {
  padding: 0 18px;
}

.gender-group {
  p {
    margin-bottom: 0px;
    align-self: center;
    margin-right: 20px;
  }

}

.circle {
  width: 45px;
  height: 45px;
  color: #ffff;
  border-radius: 50%;
  position: relative;
  background: rgba($color: #000000, $alpha: 0.3);
  margin-right: 7px;

  &.active {
    background: #3c1361;
  }

  img {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
}

.my-btn {
  font-size: 20px;
  text-transform: none;
  height: auto !important;
  padding: 10px 0 !important;
  font-weight: bold;
}

.warningPopup {
  color: red;
  font-weight: bold;
}
</style>
