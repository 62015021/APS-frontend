<template>
  <div id="UserPetition" class="bg-color">
    <NavbarUser />
    <v-card class="cardmargin text-center">
      <h1>
        เลือกแบบคำร้อง / ยื่นเรื่อง
        <v-divider></v-divider>
      </h1>

      <v-data-iterator
        :items="items"
        :items-per-page.sync="itemsPerPage"
        :page.sync="page"
        :search="search"
        :sort-by="sortBy.toLowerCase()"
        :sort-desc="sortDesc"
        hide-default-footer
        class="cardmargin"
      >
        <template v-slot:header>
          <v-text-field
            v-model="search"
            dense
            filled
            rounded
            label="ค้นหาเอกสาร"
            class="cardshow"
          ></v-text-field>
        </template>

        <template v-slot:default="name">
          <v-row
            v-for="item in name.items"
            :key="item.name"
            router
            :to="item.route"
            class="cardshow"
          >
            <v-col>
              <v-btn block height="200" router :to="item.route">
                <v-row>
                  <v-col align="center">
                    <v-btn color="primary" width="100" height="100">
                      <v-icon>mdi-{{ item.icon }}</v-icon>
                    </v-btn>
                    
                  </v-col>
                  <v-col>
                    <h2>{{ item.name }}</h2>
                    <h2>{{ item.detail }}</h2>
                  </v-col>
                </v-row>
              </v-btn>
            </v-col>
          </v-row>
        </template>
      </v-data-iterator>
    </v-card>
  </div>
</template>

<script>
import NavbarUser from "../../components/NavbarUser.vue";
export default {
  name: "UserPetition",
  components: {
    NavbarUser,
  },
  data() {
    return {
      search: "",
      filter: {},
      sortDesc: false,
      page: 1,
      itemsPerPage: 4,
      sortBy: "name",
      keys: ["Name"],
      items: [
        {
          name: "เอกสารความกก้าวหน้า",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอสอบย้อนหลัง",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอเลื่อนตำเเหน่ง",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องลดหย่อนภาษี",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอเบิกเงินเดือน",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องลาพักร้อน",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอลาออก",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอ ลาป่วย",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอทำงานล่วงเวลา",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
        {
          name: "คำร้องขอลงทุ่น",
          route: "/Sentpentition",
          icon: "file-document-outline",
          detail:"ส่งความก้าวหน้าการทำโครงการ",
        },
      ],
    };
  },
};
</script>

<style scoped>
.bg-color {
  background: #f0f0f0;
  height: 100%;
}
.cardmargin {
  margin: 2%;
}
</style>
