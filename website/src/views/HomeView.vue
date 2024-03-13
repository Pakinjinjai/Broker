<template>
  <div class="mt-10">
    <HelloWorld class="text-red-600" msg="ยินดีต้อนรับเข้าสู่ : เว็บตรวจสอบสถานะระดับน้ำ" />
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
