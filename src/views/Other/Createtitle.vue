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
              <!-- <v-divider></v-divider> -->
              <h3>ชื่อข้อมูลเฉพาะ</h3>
              <v-row v-for="(form, index) in forms" :key="index">
                <v-col>
                  <div v-html="renderForm(form.name)"></div>
                </v-col>
              </v-row>

              <div v-for="(form, index) in forms" :key="index"></div>
                {{forms}}

              <v-row>
                <v-col align="center">
                  <v-btn icon outlined @click="addForm()"
                    ><v-icon>mdi-plus</v-icon></v-btn
                  >
                  <h3>กดเครื่องหมายเพื่อเพิ่มข้อมูลเฉพาะ</h3>
                </v-col>
              </v-row>
            </v-form>
            
            <v-btn color="primary" @click="e1 = 2"> ถัดไป </v-btn>

            <v-btn text to="/OfficerPetitionManagement"> ยกเลิก </v-btn>
          </v-stepper-content>

          <v-stepper-content step="2">
            <v-card
              class="mb-12"
              color="grey lighten-1"
              height="200px"
            ></v-card>

            <v-btn color="primary" @click="e1 = 3"> ถัดไป </v-btn>

            <v-btn text @click="e1 = 1"> Cancel </v-btn>
          </v-stepper-content>

          <v-stepper-content step="3" >
            <v-card
              class="mb-12"
              color="grey lighten-1"
              height="200px"
            ></v-card>

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
      formName : "",
      
      e1: 1,
      forms: [
        
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
