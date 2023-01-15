<template>
  <div class="pt-10 flex flex-col items-center">
    <p class="mb-5 text-center">
      Enter the description of the image you want and choose the size you want
      then watch us perform our magic.
    </p>
    <div
      class="flex flex-col md:grid md:grid-cols-2 md:grid-rows-2 md:w-5/12 gap-4"
    >
      <div class="w-full col-span-2">
        <input
          id="input"
          v-model="state.input"
          class="border border-[#990f3d] outline-none h-10 bg-inherit rounded-lg w-full indent-2 shadow-md text-gray-600 font-sora"
          placeholder="e.g., a girl with a cat...."
        />
      </div>
      <div>
        <select
          id="size"
          v-model="state.size"
          class="bg-inherit w-full h-10 border border-[#990f3d] text-gray-600 rounded-lg shadow-md outline-none"
        >
          <option value="">Select a size</option>
          <option value="1024x1024">Large</option>
          <option value="512x512">Medium</option>
          <option value="256x256">Small</option>
        </select>
      </div>
      <div>
        <select
          id="number"
          v-model.number="state.number"
          class="bg-inherit w-full h-10 border border-[#990f3d] text-gray-600 rounded-lg shadow-md outline-none"
        >
          <option value="">Select number of images to generate</option>
          <option>1</option>
          <option>2</option>
          <option>3</option>
          <option>4</option>
          <option>5</option>
          <option>6</option>
          <option>7</option>
          <option>8</option>
          <option>9</option>
          <option>10</option>
        </select>
      </div>
    </div>
    <button
      @click="generateImage"
      class="bg-gradient-to-r from-[#990f3d] to-orange-800 h-10 mt-8 w-8/12 md:w-3/12 shadow-md text-white p-2 rounded-lg"
    >
      <p v-if="!isLoading">Generate Image</p>
      <p v-if="isLoading">Generating.....</p>
    </button>
    <p
      v-if="errors"
      class="mt-4 text-[#990f3d] text-md font-bold text-center p-4"
    >
      {{ errors }}
    </p>
    <div v-if="image_url">
      <div v-for="image in image_url" :key="image.url">
        <img
          class="border-[#990f3d] border-2 rounded-md m-3 shadow-lg"
          :src="image.url"
        />
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from "vue";
import { Configuration, OpenAIApi } from "openai";
export default {
  name: "Main",
  setup() {
    const state = reactive({
      input: "",
      size: "",
      number: "",
    });

    let resp;
    const image_url = ref(null);
    const isLoading = ref(false);
    const errors = ref("");

    const configuration = new Configuration({
      apiKey: import.meta.env.VITE_APP,
    });

    const openai = new OpenAIApi(configuration);

    const generateImage = async () => {

      isLoading.value = true;
      
      if (!state.input || !state.number || !state.size) {
        isLoading.value = false;
        errors.value = "Please ensure all fields are filled";
      } else {
        try {
          errors.value = "";
          resp = await openai.createImage({
            prompt: state.input,
            n: state.number,
            size: state.size,
          });
          image_url.value = resp?.data?.data;
          isLoading.value = false;
          state.input = "";
          state.number = "";
          state.size = "";
        } catch (error) {
          errors.value =
            "Oops... An error occurred while generating the images, please try again.";
          console.log("error don sup o bolaji");
          isLoading.value = false;
        }
      }
    };

    return {
      state,
      generateImage,
      image_url,
      isLoading,
      errors,
    };
  },
};
</script>
