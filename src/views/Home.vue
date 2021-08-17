<template>
  <div class="home">
    <h1>DropZone</h1>
    <DropZone @drop.prevent="drop" @change="selectedFile" />
    <div class="info-wrapper" v-if="dropzoneFile">
      <span class="file-info">File : {{ dropzoneFile.name }}</span>
      <span class="file-info">Size : {{ fileSize }} bytes</span>
      <img src="" :alt="dropzoneFile.name" id="image" width="100px" height="100px">
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import DropZone from "@/components/DropZone.vue";
import { ref } from "vue";

export default {
  name: "Home",
  components: {
    DropZone,
  },

  setup() {
    let dropzoneFile = ref("");
    let fileSize = ref("");

    // Drop ile yğkleme
    const drop = (event) => {
      console.log(event.dataTransfer.files[0])
      let file = event.dataTransfer.files[0]

      dropzoneFile.value = file;
      sizeCalc(file)
    };

   
    // Input change olduğunda
    const selectedFile =  async () => {
      let file = document.querySelector(".dropzoneFile").files[0]

      dropzoneFile.value = document.querySelector(".dropzoneFile").files[0];

      sizeCalc(file)
    };

    const sizeCalc = (file) => {
       let sizeCalc = file.size / 1024 / 1024;
       sizeCalc = sizeCalc.toFixed(2);

       fileSize.value = sizeCalc
    }

    return {
      dropzoneFile,
      drop,
      fileSize,
      selectedFile,
      sizeCalc
    };
  },
};
</script>

<style lang="scss" scoped>
.home {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #f1f1f1;

  h1 {
    font-size: 40px;
    margin-bottom: 32px;
  }

  .info-wrapper {
    margin-top: 20px;
    display: flex;
    flex-direction: column;

    .file-info {
      margin-top: 10px;
    }
  }
}
</style>
