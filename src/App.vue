<template>
  <div class="m-0 p-0 min-h-screen bg-gray-200">
    <NavbarVue />
    <Main />
  </div>
</template>

<script>
import NavbarVue from "./component/Navbar.vue";
import Main from "./component/Main.vue";
export default {
  name: "App",
  components: { NavbarVue, Main },
  setup() {},
};
</script>
