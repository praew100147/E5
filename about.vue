<template>
  <v-container fluid class="pa-5" style="background-color: #f5f5f5;">
    <v-row justify="center">
      <v-col cols="12" md="8">
        <v-card class="elevation-3" max-width="2000px">
          <v-img
            src="https://scontent.fbkk7-2.fna.fbcdn.net/v/t39.30808-6/418298730_1788093858373888_2545157505706341693_n.jpg?stp=cp6_dst-jpg&_nc_cat=110&ccb=1-7&_nc_sid=833d8c&_nc_ohc=wAM5N71cn08Q7kNvgET9dI4&_nc_ht=scontent.fbkk7-2.fna&_nc_gid=AZKoeMZcKkZ7RzBpSNhQrUz&oh=00_AYA7AGISQkcvkvP-XTKJdG4u7SQx6ri31JQ1jGDFAQEeAQ&oe=66DDC1EF"
            alt="About Us Image"
            height="300px"
            class="elevation-1"
          ></v-img>

          <v-card-title class="headline text-center py-4" style="color: #1e88e5;">
             เกี่ยวกับเรา
          </v-card-title>

          <v-divider></v-divider>

          <v-card-text class="px-5 py-3">
            <v-row>
              <v-col cols="12">
                <p>
                  สวัสดีค่ะ! ฉันชื่อ อุมาพร ทองประศรี หรือเรียกสั้น ๆ ว่า "อุมาพร" ก็ได้ค่ะ เป็นคนที่มีความหลงใหลในการเรียนรู้และสำรวจสิ่งใหม่ ๆ ในชีวิตอยู่เสมอ ไม่ว่าจะเป็นการพัฒนาทักษะส่วนตัว การทำงาน หรือการเชื่อมโยงกับผู้คนรอบข้าง ฉันเชื่อมั่นในพลังของการพัฒนาตนเอง และความสำคัญของการเติบโตทั้งในด้านความคิดและการใช้ชีวิต
                </p>
                <p>
                  นอกจากนี้ ฉันยังเป็นคนที่ให้ความสำคัญกับความสัมพันธ์ที่ดีและการสนับสนุนกันและกันในทุก ๆ ด้าน ไม่ว่าคุณจะมีคำถาม ข้อสงสัย หรือแค่ต้องการใครสักคนที่รับฟัง ฉันก็พร้อมที่จะเป็นคนนั้นเสมอค่ะ
                  ฉันเชื่อว่าในทุกโอกาสมีความท้าทาย แต่ก็มีความเป็นไปได้ในการเติบโตและเรียนรู้เช่นกัน ยินดีมากที่ได้รู้จักทุกคนค่ะ และหากมีอะไรที่ฉันสามารถช่วยเหลือหรือแลกเปลี่ยนความรู้ประสบการณ์ได้ ก็ยินดีอย่างยิ่งที่จะทำเช่นนั้นค่ะ! 😊
                </p>
              </v-col>

              <v-col cols="12">
                <v-card class="elevation-2" color="#e3f2fd" outlined>
                  <v-card-title class="headline" style="color: #1976d2;">
                    Our Mission
                  </v-card-title>
                  <v-card-text>
                    พันธกิจของเราคือการสร้างแพลตฟอร์ม E-commerce ที่เข้าถึงง่ายและทรงพลัง ซึ่งช่วยให้ผู้ใช้สามารถควบคุมประสบการณ์การช้อปปิ้งของตนได้อย่างเต็มที่ด้วยเทคโนโลยีที่ใช้งานง่ายและเชื่อถือได้
                  </v-card-text>
                </v-card>
              </v-col>

              <v-col cols="12" class="text-center pt-4">
                <v-btn color="primary" @click="home" class="mr-4" large>ไปยังหน้าหลัก</v-btn>
                <v-btn color="secondary" @click="contactUs" large>ติดต่อเรา</v-btn>
              </v-col>
            </v-row>
          </v-card-text>

          <v-divider></v-divider>

          <v-card-actions class="justify-center py-4">
            <v-btn icon @click="share">
              <v-icon>mdi-share-variant</v-icon>
            </v-btn>
            <v-btn icon @click="like">
              <v-icon>mdi-thumb-up</v-icon>
            </v-btn>
            <v-btn icon @click="follow">
              <v-icon>mdi-account-plus</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  methods: {
    home() {
      this.$router.push("/home");
    },
    contactUs() {
      alert("Contact us at: contact@example.com");
    },
    share() {
      alert("Share this page!");
    },
    like() {
      alert("You liked this page!");
    },
    follow() {
      alert("You are now following us!");
    },
  },
};
</script>

<style scoped>
.v-card {
  border-radius: 12px;
}

.v-card-title {
  font-weight: bold;
}

.v-card-text p {
  font-size: 1.2rem;
  line-height: 1.8;
}

.v-btn {
  text-transform: none;
}

.v-card-actions {
  background-color: #f5f5f5;
}

.v-btn v-icon {
  color: #1976d2;
}
</style>
