<template>
  <v-container fluid class="pa-4" style="background-color: #f5f5f5;">
    <v-row justify="center" class="mb-5">
      <v-col class="box_container" ols="12" md="8" lg="6">
        <v-card class="pa-5 elevation-12 rounded-xl" color="#ffffff">
          <div class="Program">         
                <h4 class="TEXT">Program MQTTX</h4>
          </div>
          <v-row class="mb-4">
            <v-col cols="12" class="text-center">
              <v-btn
                class="ma-2 rounded-pill"
                color="primary"
                large
              >
                {{ status || 'Not Connected' }}
                <v-icon class="ml-2" icon="mdi-checkbox-marked-circle"></v-icon>
              </v-btn>
            </v-col>
          </v-row>

          <v-row class="mb-4">
            <v-col cols="12" md="6" class="text-center">
              <h4 class="font-weight-bold mb-3">SW 1</h4>
              <v-row align="center" justify="center">
                <v-col class="d-flex align-center justify-center" cols="auto">
                  <v-btn class="btn-on mx-1" size="small" @click="on1">ON</v-btn>
                </v-col>
                <v-col class="d-flex align-center" cols="auto">
                  <v-progress-circular :model-value="value1" :rotate="360" :size="100" :width="15" color="#4a148c">
                    <template v-slot:default> {{ value1 }} % </template>
                  </v-progress-circular>
                </v-col>
                <v-col class="d-flex align-center justify-center" cols="auto">
                  <v-btn class="btn-off mx-1" size="small" @click="off1">OFF</v-btn>
                </v-col>
              </v-row>
            </v-col>
            <v-col cols="12" md="6" class="text-center">
              <h4 class="font-weight-bold mb-3">SW 2</h4>
              <v-row align="center" justify="center">
                <v-col class="d-flex align-center justify-center" cols="auto">
                  <v-btn class="btn-on1 mx-1" size="small" @click="on2">ON</v-btn>
                </v-col>
                <v-col class="d-flex align-center" cols="auto">
                  <v-progress-circular :model-value="value2" :rotate="360" :size="100" :width="15" color="red">
                    <template v-slot:default> {{ value2 }} % </template>
                  </v-progress-circular>
                </v-col>
                <v-col class="d-flex align-center justify-center" cols="auto">
                  <v-btn class="btn-off1 mx-1" size="small" @click="off2">OFF</v-btn>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>



<script>
import mqtt from "mqtt";
export default {
  data() {
    return {
      id: 1,
      msg: "",
      status: "",
      value1: 0,
      value2: 0,
      client: null,
    };
  },

  created() {
    this.client = mqtt.connect("ws://broker.emqx.io:8083/mqtt");
    this.client.on("connect", this.onMqttConnect);
    this.client.on("message", this.onMqttMessage);
    this.client.on("reconnect", this.handleOnReConnect);
  },

  beforeDestroy() {
    this.client && this.client.end();
  },

  methods: {
    on1() {
      this.value1 = 69;
      this.client.publish("room/sw01", String("ON"));
    },

    on2() {
      this.value2 = 56;
      this.client.publish("room/sw02", String("ON"));
    },

    off1() {
      this.value1 = 0;
      this.client.publish("room/sw01", String("OFF"))
    },

    off2() {
      this.value2 = 0;
      this.client.publish("room/sw02", String("OFF"));
      
    },

    onMqttConnect() {
      this.status = "Mqtt connected";
      this.client.publish("op", "status");
      this.client.subscribe("status");
      this.client.subscribe("room/sw01");
    },

    onMqttMessage(topic, message) {
      if (topic === "status") {
        this.msg = message.toString();
      }
      if (topic === "room/sw01") {
        this.value = parseInt(message.toString(), 10);
      }
      if (topic === "room/sw02") {
        this.value = parseInt(message.toString(), 10);
      }
    },

    handleOnReConnect() {
      this.status = "Mqtt Reconnecting...";
      if (this.retryTimes > 5) {
        this.client.end();
        this.status = "Mqtt Disconnected";
      }
    },
  },
};
</script>

<style scoped>
/* Global Styles */
/* Global Styles */
/* Global Styles */
body {
  background-color: #1e1e1e; /* ใช้สีเข้มที่ดูดุดัน */
  font-family: 'Poppins', sans-serif; /* Font ที่ดูมีความเป็นเอกลักษณ์ */
  margin: 0;
  padding: 0;
  color: #e0e0e0;
}

/* Box Container */
.box_container {
  transition: transform 0.5s, box-shadow 0.5s, border-radius 0.5s;
  border-radius: 10px;
  padding: 10px;
}

.box_container:hover {
  border-radius: 40px; /* เพิ่มความแปลกใหม่เมื่อ hover */
  box-shadow: 0px 15px 30px rgba(255, 126, 95, 0.5); /* เงาที่ดูมีมิติ */
}

/* Program Header */
.Program {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 30px;
}

.TEXT {
  background-color: #333333;
  color: #ff7e5f;
  padding: 15px 30px;
  border-radius: 50px; /* ใช้ความกลมเพื่อให้แตกต่าง */
  text-transform: uppercase;
  font-weight: bold;
  font-size: 1.8rem;
  transition: 0.5s;
}

.TEXT:hover {
  background-color: #444444;
  box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.5);
  letter-spacing: 2px; /* เพิ่มการขยับของตัวอักษรเมื่อ hover */
}

/* Card Styles */
.v-card {
  border-radius: 20px; /* ใช้รูปทรงกลมกว่าปกติ */
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px); /* เพิ่มความโปร่งใสและเบลอ */
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
  transition: transform 0.4s ease;
  padding: 40px;
}

.v-card:hover {
  transform: scale(1.02);
  box-shadow: 0 18px 30px rgba(0, 0, 0, 0.4); /* เงามืดขึ้นเมื่อ hover */
}

/* Typography */
h4 {
  font-size: 1.5rem;
  color: #ff7e5f;
  text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.2);
  margin-bottom: 1rem;
}

/* Buttons */
.v-btn {
  border-radius: 50px;
  transition: all 0.4s;
  padding: 12px 25px;
  text-transform: uppercase;
  font-weight: 600;
  letter-spacing: 1px;
  position: relative;
  overflow: hidden;
  z-index: 1;
}

.v-btn:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.1);
  z-index: -1;
  transform: scaleX(0);
  transform-origin: left;
  transition: transform 0.4s;
}

.v-btn:hover:before {
  transform: scaleX(1);
}

/* ON Button */
.btn-on {
  background: linear-gradient(135deg, #43cea2, #185a9d);
  color: #fff;
}

.btn-on:hover {
  box-shadow: 0px 0px 15px rgba(67, 206, 162, 0.7);
}

/* OFF Button */
.btn-off {
  background-color: transparent;
  color: #ff7e5f;
  border: 2px solid #ff7e5f;
}

.btn-off:hover {
  background-color: #ff7e5f;
  color: #fff;
  box-shadow: 0px 0px 15px rgba(255, 126, 95, 0.5);
}

.btn-on1 {
  background: linear-gradient(135deg, #43cea2, #185a9d);
  color: #fff;
}

.btn-on1:hover {
  box-shadow: 0px 0px 15px rgba(67, 206, 162, 0.7);
}

/* OFF Button */
.btn-off1 {
  background-color: transparent;
  color: #ff7e5f;
  border: 2px solid #ff7e5f;
}

.btn-off1:hover {
  background-color: #ff7e5f;
  color: #fff;
  box-shadow: 0px 0px 15px rgba(255, 126, 95, 0.5);
}
/* Progress Circular */
.v-progress-circular {
  color: #43cea2;
  border-radius: 50%;
  transition: transform 0.4s ease;
}

.v-progress-circular:hover {
  transform: scale(1.1) rotate(360deg); /* หมุนเมื่อ hover */
}

/* Responsive Design */
@media (max-width: 600px) {
  .v-card {
    padding: 20px;
  }

  .TEXT {
    font-size: 1.2rem;
    padding: 10px;
  }

  .v-btn {
    padding: 8px 16px;
    font-size: 0.875rem;
  }

  .v-progress-circular {
    size: 80;
  }
}


/* Responsive Design */
@media (max-width: 600px) {
  .v-card {
    padding: 2rem; /* Adjust padding for smaller screens */
  }
}
</style>




