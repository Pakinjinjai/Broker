<template>
  <div class="flex flex-col items-center justify-start h-screen">
    <h1 class="text-3xl font-bold mb-4">ยินดีต้อนรับเข้าสู่</h1>
    <h2 class="text-2xl font-semibold mb-8">เว็บตรวจสอบสถานะระดับน้ำ</h2>
    <div 
      class="flex items-center justify-center bg-gray-100 p-6 rounded-lg shadow-lg"
      >
      <p class="text-lg" v-if="water">{{ water }}</p>
      <p class="text-lg" v-if="!water">กำลังรอสถานะโปรดรอสักครู่</p>
    </div>
    <h1 class="text-3xl font-bold mt-8">Real-time : {{ currentTime }}</h1>
    <h1 
      v-if="!currentTime"
      class="text-3xl font-bold mt-8">Real-time : กรุณนารอสักครู่</h1>
  </div>
</template>

<script>
import mqtt from "mqtt";

export default {
  name: "HomePage",
  props: {
    msg: String,
  },
  data() {
    return {
      water: "", // เก็บข้อมูลระดับน้ำที่ได้รับมาจาก MQTT server
      currentTime: "" // เก็บค่าเวลาปัจจุบัน
    };
  },
  mounted() {
    const client = mqtt.connect("ws://localhost:8883");

    client.on("connect", () => {
      client.subscribe("water_level"); // Subscribe topic water_level เท่านั้น
      console.log("MQTT Connected");
    });

    client.on("message", (topic, message) => {
      // เมื่อมีข้อมูลมาใหม่จาก MQTT server
      if (topic === "water_level") {
        this.water = message.toString(); // กำหนดค่าของ water ใหม่
        console.log(topic, message.toString());
      }
    });

    // อัพเดทค่าเวลาทุกๆ 1 วินาที
    setInterval(() => {
      this.updateTime();
    }, 0);
  },
  methods: {
    updateTime() {
      const now = new Date();
      const hours = now.getHours().toString().padStart(2, "0");
      const minutes = now.getMinutes().toString().padStart(2, "0");
      const seconds = now.getSeconds().toString().padStart(2, "0");
      this.currentTime = `${hours}:${minutes}:${seconds}`;
    }
  }
};
</script>

<style scoped>
</style>
