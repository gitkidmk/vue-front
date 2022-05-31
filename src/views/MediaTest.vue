<script lang="ts" allowJs>
export default {
  methods: {
    toBase64: (file: File) =>
      new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => {
          resolve(reader.result);
          // 여기에 api call 하기
        };
        reader.onerror = (error) => reject(error);
      }),
    async uploadImageFile(target: HTMLInputElement) {
      const videoFile: File = target.files![0];
      console.log(videoFile.name, videoFile.type);
      console.log(videoFile.stream());
      await this.toBase64(videoFile);
    },
  },
};
</script>

<template>
  <div class="about">
    <h1>This is for Media Test</h1>
    <input
      ref="imageUploader"
      type="file"
      multiple
      @change="uploadImageFile($event.target)"
    />
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
  }
}
</style>
