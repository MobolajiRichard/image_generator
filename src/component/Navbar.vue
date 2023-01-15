<template>
  <div
    class="relative bg-gradient-to-r from-[#990f3d] to-orange-800 h-12 flex items-center text-white justify-between font-caveat text-xl p-2"
  >
    <p class="text-3xl font-caveat">
      <span class="text-yellow-400 font-bold">I</span>mage<span
        class="text-yellow-400 font-bold"
        >G</span
      >enerator
    </p>
    <p @click="openAbout" class="cursor-pointer">About</p>
    <div
      v-if="open"
      class="absolute right-0 top-12 w-full md:w-1/4 text-black bg-white shadow-lg rounded-b-md font-outfit text-sm p-2"
    >
      <p class="text-center">
        This is an images generator application built on the OpenAi DALL.E API.
      </p>
      <p class="my-4 text-justify">
        The application is very simple to use, enter the description of the
        image you want, select the size and the numbers of image you want to
        generate
      </p>
      <p class="text-center">
        Please note that any image generated is the property of OpenAi and may
        be subjected to copyright.
      </p>
      <div class="flex justify-center mt-4">
        <a href="https://github.com/MobolajiRichard" class="mr-2">
          <Icon width="30" color="" icon="mdi:github" />
        </a>
        <a
          href="https://www.linkedin.com/in/mobolaji-richard-oginni-7314b2230/"
        >
          <Icon width="30" color="#0072b1" icon="mdi:linkedin" />
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import { Icon } from "@iconify/vue";
export default {
  name: "Navbar",
  components: { Icon },
  setup() {
    const open = ref(false);

    const openAbout = () => {
      open.value = !open.value;
    };
    return {
      open,
      openAbout,
    };
  },
};
</script>
