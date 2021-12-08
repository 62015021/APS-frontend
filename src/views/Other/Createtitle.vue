<template>
  <!-- ส่วนจัดเเสดง -->
  <div id="Formmanagement">
    <NavbarOF />
    <v-card class="cardshow">
      <h1>
        จัดการคำร้อง/ยื่นเรื่อง
        <v-divider></v-divider>
      </h1>
      <!-- ส่วนเเสดงการสร้างฟอร์ม -->
      <v-stepper v-model="e1">
        <v-stepper-header>
          <v-stepper-step :complete="e1 > 1" step="1">
            หัวเรื่อง
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step :complete="e1 > 2" step="2">
            ใส่ผู้อนุมัติ
          </v-stepper-step>

          <v-divider></v-divider>

          <v-stepper-step step="3"> ตัวอย่าง </v-stepper-step>
        </v-stepper-header>

        <v-stepper-items>
          <v-stepper-content step="1">
            <!-- กรอกข้อมูลเอกสาร -->
            <v-form class="cardshow">
              <v-text-field
                placeholder="หัวเรื่อง....."
                outlined
                v-model="forms.title"
              ></v-text-field>
              เลื่อนสวิตซ์ หากต้องการเก็บข้อมูลเฉพาะ
              <v-switch
                          inset
                          v-model="heard.hasSpecificsDetail"
                          
                        ></v-switch>
              {{heard.hasSpecificsDetail}}
              <!-- <v-divider></v-divider> -->
              <v-row v-if="heard.hasSpecificsDetail = heard.hasSpecificsDetail">
                <v-col>
                  <h3>ชื่อข้อมูลเฉพาะ</h3>
                  <v-row v-for="(form, index) in forms" :key="index">
                    <v-col>
                      <div v-html="renderForm(form.name)"></div>
                    </v-col>
                  </v-row>

                  <div v-for="(form, index) in forms" :key="index"></div>

                  <v-row>
                    <v-col align="center">
                      <v-btn icon outlined @click="addForm()"
                        ><v-icon>mdi-plus</v-icon></v-btn
                      >
                      <h3>กดเครื่องหมายเพื่อเพิ่มข้อมูลเฉพาะ</h3>
                    </v-col>
                  </v-row>
                </v-col>
              </v-row>
            </v-form>

            <v-btn color="primary" @click="e1 = 2"> ถัดไป </v-btn>

            <v-btn text to="/OfficerPetitionManagement"> ยกเลิก </v-btn>
          </v-stepper-content>

          <v-stepper-content step="2">
            <!-- กรอกข้อมูลเอกสาร -->
            <v-form class="cardshow">
              <v-text-field
                placeholder="หัวเรื่อง....."
                outlined
                v-model="forms.title"
              ></v-text-field>
              <!-- <v-divider></v-divider> -->
              <h3>เพิ่มผู้อนุมัติ</h3>
              <v-row v-for="(form, index) in forms" :key="index">
                <v-col>
                  <div v-html="renderForm(form.name)"></div>
                </v-col>
              </v-row>

              <div v-for="(form, index) in forms" :key="index"></div>

              <v-row>
                <v-col align="center">
                  <v-btn icon outlined @click="addForm()"
                    ><v-icon>mdi-plus</v-icon></v-btn
                  >
                  <h3>กดเครื่องหมายเพื่อเพิ่มผู้อนุมัติ</h3>
                </v-col>
              </v-row>
            </v-form>

            <v-btn color="primary" @click="e1 = 3"> ถัดไป </v-btn>

            <v-btn text @click="e1 = 1"> Cancel </v-btn>
          </v-stepper-content>

          <v-stepper-content step="3">
            <!-- หน้าเเสดงพรีวิว -->

            <h1 v-for="heard in heard" :key="heard" style="text-align: center">
              {{ heard.title }}
            </h1>
            <v-form v-model="valid" v-for="profile in profile" :key="profile">
              <v-container>
                <v-row>
                  <v-col cols="12" md="4">
                    <v-text-field
                      v-model="profile.Fname"
                      :rules="nameRules"
                      :counter="10"
                      label="ชื่อ"
                      required
                      disabled
                    ></v-text-field>
                  </v-col>

                  <v-col cols="12" md="4">
                    <v-text-field
                      v-model="profile.Lname"
                      :rules="nameRules"
                      :counter="10"
                      label="นามสกุล"
                      required
                      disabled
                    ></v-text-field>
                  </v-col>

                  <v-col cols="12" md="4">
                    <v-text-field
                      v-model="profile.gender"
                      :rules="emailRules"
                      label="เพศ"
                      required
                      disabled
                    ></v-text-field>
                  </v-col>
                </v-row>

                <v-row>
                  <v-col>
                    <v-text-field
                      v-model="profile.email"
                      :rules="emailRules"
                      label="E-mail"
                      required
                      disabled
                    ></v-text-field>
                  </v-col>
                </v-row>

                <v-row>
                  <v-col>
                    <v-text-field
                      v-model="profile.tell"
                      :rules="emailRules"
                      label="เบอร์โทร"
                      required
                      disabled
                    ></v-text-field>
                  </v-col>
                </v-row>

                <v-row>
                  <v-col>
                    <v-text-field
                      v-model="profile.addess"
                      :rules="emailRules"
                      label="ที่อยู่"
                      required
                      disabled
                    ></v-text-field>
                  </v-col>
                </v-row>

                <v-row v-for="heard in heard" :key="heard">
                  <v-col align="center" v-if="heard.hasSpecificsDetail">
                    <v-row v-for="specifics in specifics" :key="specifics">
                      <v-col>
                        {{ specifics.titleheard }}
                        <v-text-field
                          v-model="specifics.specificsdetail"
                          :rules="emailRules"
                          label="ใส่ข้อมูลลงที่นี้"
                          required
                        >
                        </v-text-field>
                      </v-col>
                    </v-row>
                  </v-col>
                </v-row>

                <v-row>
                  <v-col align="center">
                    <v-btn class="ma-2" color="success"> ส่งคำร้อง </v-btn>
                  </v-col>

                  <v-col align="center">
                    <v-btn class="ma-2" outlined color="error">
                      ย้อนกลับ
                    </v-btn>
                  </v-col>
                </v-row>
              </v-container>
            </v-form>

            <!-- หน้าเเสดงพรีวิว -->

            <v-btn color="primary" @click="e1 = 1"> Continue </v-btn>

            <v-btn text @click="e1 = 2"> Cancel </v-btn>
          </v-stepper-content>
        </v-stepper-items>
      </v-stepper>

      <!-- ส่วนเเสดงการสร้างฟอร์ม -->
    </v-card>
  </div>
  <!-- ส่วนจัดเเสดง -->
</template>

<script>
import NavbarOF from "../../components/NavbarOfficer.vue";
export default {
  name: "Createtitle",
  components: {
    NavbarOF,
  },
  data() {
    return {
      formName: "",

      e1: 1,
      forms: [],
      profile: [
        {
          Fname: "ณัฐภูมิ",
          Lname: "ผาจิต",
          gender: "ชาย",
          email: "62015011@kmit.ac.th",
          tell: "0856937521",
          addess:
            "เลขที่ 1 ซอยฉลองกรุง 1แขวงลาดกระบัง เขตลาดกระบังกรุงเทพฯ 10520",
        },
      ],
      heard: [
        {
          title: "การขอสอบย้อนหลัง",
          hasSpecificsDetail: null, //ตัวกำหนดว่าเป็นฟอรมต้องใส่รายละเอียดเพิ่ม
        },
      ],
      specifics: [
        { titleheard: "ข้อมูลรายวิชา", specificsdetail: "" },
        { titleheard: "เหตุผล", specificsdetail: "" },
        { titleheard: "เหตุผล", specificsdetail: "" },
        { titleheard: "เหตุผล", specificsdetail: "" },
      ],
    };
  },
  methods: {
    addForm: function () {
      let form = {
        name: this.formName,
      };
      this.forms.push(form);
      this.formName = "";
    },
    renderForm: function (name) {
      return `
      <div class="mb-3">
      <input type="text"id="${name}" v-model="forms" class="form-control" ></input>
      </div>
      

      
      `;
    },
    submit: function () {},
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
  padding: 10px;
}
.cardshow {
  margin: 2%;
}
.btn-margin {
  margin: 3%;
}
h3 {
  margin: 2%;
}
</style>
