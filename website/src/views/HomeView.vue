<template>
  <div class="mt-10">
    <HelloWorld class="text-2xl font-bold text-indigo-900" msg="ยินดีต้อนรับเข้าสู่ : เว็บตรวจสอบสถานะระดับน้ำ" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
  },
};
</script>
