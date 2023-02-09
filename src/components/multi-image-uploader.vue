<template>
    <div class="images-container" :class="(totalSize === 0 ? 'images-container-empty':'images-container')">
      <div class="image-select" @click="triggerInput()">+ Add Image</div>
      <input class="" ref="images" type="file" @change="getImagesAndPush"  hidden multiple accept="image/*">
      <div class="image" v-for="(image, index) in images" :key="index" >
        <img :src="image.blob" :alt="image.src" :title="image.src">
        <button @click="removeImg(index)">X</button>
        <span>{{this.fileSize(image.size)}}</span>
      </div>
      <div class="image-upload" v-if="images.length > 0">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512" fill="#adadad">
          <path d="M64 0C28.7 0 0 28.7 0 64V448c0 35.3 28.7 64 64 64H320c35.3 0 64-28.7 64-64V160H256c-17.7 0-32-14.3-32-32V0H64zM256 0V128H384L256 0zM216 408c0 13.3-10.7 24-24 24s-24-10.7-24-24V305.9l-31 31c-9.4 9.4-24.6 9.4-33.9 0s-9.4-24.6 0-33.9l72-72c9.4-9.4 24.6-9.4 33.9 0l72 72c9.4 9.4 9.4 24.6 0 33.9s-24.6 9.4-33.9 0l-31-31V408z"/>
        </svg>
        <div>Upload</div>
        <div>{{images.length > 1? images.length  +' images' :  "Image"}}</div>
        <p>{{this.fileSize(totalSize)}}</p>
      </div>
    </div>
</template>

<script>
export default {
  data() {
    return {
      images: [],
      totalSize: 0,
    }
  },
  methods: {
    getImagesAndPush(e) {
      if(e.target.files.length > 0) {
        for(let i=0; i < e.target.files.length; i++) {
          this.images.push({src: e.target.files[i].name, size:e.target.files[i].size, blob: URL.createObjectURL(e.target.files[i]) });
        }
      }
      this.totalFileSize()
    },
    removeImg(index) {
      this.images.splice(index, 1);
      this.totalFileSize()
    },
    triggerInput() {
      this.$refs.images.click()
    },
    fileSize(byte) {
      let kb = byte / 1024
      let mb = byte * 0.00000095367432
      if (mb > 1) {
        return mb.toFixed(2) + " mb"
      } else {
        return Math.floor(kb) + " kb"
      }
    },
    totalFileSize() {
      this.totalSize = 0
      for (let i=0; i < this.images.length; i++) {
        this.totalSize += this.images[i].size
      }
    }
  },
  computed: {

  }
}
</script>
<style scoped>
.images-container {
  width: 500px;
  display: flex;
  flex-wrap: wrap;
  gap:.5rem;
  box-sizing: border-box;
}
.images-container-empty {
  justify-content: center;
}
.images-container > *, .images-container > * > *{
  transition: all .5s;
}
.image, .image-select, .image-upload {
  width: 10rem;
  height: 10rem;
  position: relative;
  border-radius: .5rem;
}
.image-select {
  border:3px dashed #adadad;
  color: #adadad;
  display: grid;
  place-items: center;
  cursor: pointer;
  background: #f5f5f5;
}
.image-select:hover {
  background: #faf0d5;
  color: #777;
}
.image-upload {
  color: #777777;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  background: #f5f5f5;
}
.image-upload:hover {
  background: #fff;
  color: #17ad23;
  border:3px solid #17ad23;
}
.image-upload > svg {
  height: 1.5rem;
  margin:1rem 0 .5rem 0;
}
img {
  width: inherit;
  height: inherit;
  object-fit: cover;
  border-radius: inherit;
}
.image > button {
  position: absolute;
  margin:.5rem;
  top:0;
  right: 0;
  width: 2rem;
  height: 2rem;
  border: none;
  border-radius: inherit;
  cursor: pointer;
}
.image > button:hover {
  background: #fff;
}
span {
  position: absolute;
  font-size: 0.8rem;
  border-radius: inherit;
  background: #eaeaea;
  bottom: 0.5rem;
  left: 0.5rem;
  padding: .2rem .5rem;
}

</style>
