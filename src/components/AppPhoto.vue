<template>
  <div class="appPhoto">
    <div id="photo">
      <div class="container">
        <h3>Image Classification w/ Taqadam</h3>
        <input type="file" @change="onFileChanged" accept="image/*">
        <div>
          <div class="image-preview">
            <img id="kvn" class="preview" :src="inputImage" height="513" width="513">
          </div>
          <div class="score" v-if="inputImage">Score: {{ this.score }}</div>
        </div>
        <button @click="predict_fn">PushFoo</button>
      </div>
    </div>
  </div>
</template>

<script>
import * as tf from "@tensorflow/tfjs";

export default {
  name: "AppPhoto",
  filters: {},
  data() {
    return {
      selectedFile: null,
      score: null,
      model: null,
      inputImage: "",
      foo: null
    };
  },
  methods: {
    placeholderImage() {
      return "../assets/tq_logo.png";
    },
    onFileChanged(event) {
      var input = event.target;
      if (input.files && input.files[0]) {
        var reader = new FileReader();
        reader.onload = e => {
          this.inputImage = e.target.result;
        };
        reader.readAsDataURL(input.files[0]);
      }
    },
    async predict_fn() {
      var image = document.getElementById("kvn");
      console.log("cool prediction", image);
      const mybool = await this.randomFoo();
      console.log("im sloower", mybool);
      console.log("im faster?");
    },
    randomFoo() {
      setTimeout(() => {
        console.log("hi im waiting");
      }, 2000);
      return true;
    }
  },
  mounted() {}
};
</script>

<style lang="scss" scoped>
[v-cloak] {
  display: none;
}

* {
  box-sizing: border-box;
  outline: none;
  transition: all 200ms ease;
}

body {
  background-image: linear-gradient(#3200ff, #00ff7e);
  height: 50vh;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  padding-top: 12px;
  transition: all 0.3s ease-in;
  @media (max-width: 512px) {
    padding: 18px;
    transition: all 0.3s ease-in;
  }
  @media (max-width: 360px) {
    padding: 16px;
    transition: all 0.3s ease-in;
  }
}

h1 {
  text-align: center;
  color: #000;
  margin: 0 0 16px 0;
}

p {
  text-align: center;
  margin-top: 0;
  margin-bottom: 24px;
}

.logo {
  margin-bottom: 24px;
}

.image-container {
  display: flex;
  justify-content: center;
}

.container {
  max-width: 480px;
  margin: 0 auto;
  background-color: #fff;
  padding: 64px;
  box-shadow: 2px 2px 96px #111;
  border-radius: 8px;
  transition: all 0.3s ease-in;
  @media (max-width: 512px) {
    padding: 32px;
    transition: all 0.3s ease-in;
  }
  @media (max-width: 360px) {
    padding: 16px;
    transition: all 0.3s ease-in;
  }
}

label {
  display: inline-block;
  width: 25%;
  min-width: 128px;
  margin-bottom: 8px;
  font-weight: bold;
}

input,
select {
  display: inline-block;
  background-color: #fff;
  color: #888;
  border: 2px solid #888;
  border-radius: 2px;
  height: 56px;
  width: 100%;
  font-size: 12px;
  padding: 16px 16px;
  margin-bottom: 24px;
  margin-bottom: 24px;
  &:focus {
    background-color: #fff;
    color: #3200ff;
    border-color: #3200ff;
    outline: 0;
  }
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

@media (max-height: 700px) {
  body {
    height: 50%;
  }
}

.button {
  border: none;
  background: #7185ec;
  color: #fff;
  font-size: 16px;
  font-weight: 500;
  border-radius: 4px;
  cursor: pointer;
  text-align: center;
  cursor: pointer;
  font-weight: bold;
  box-shadow: 1px 1px 3px 0px rgba(0, 0, 0, 0.2);
  height: 40px;
  width: 100%;
  margin-bottom: 10px;
}

button:hover {
  background-color: #586cd8;
}

button:active {
  position: relative;
  top: 1px;
  left: 1px;
  box-shadow: none;
}

.file-upload-form,
.image-preview {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  padding: 20px;
}

img.preview {
  width: 100%;
}
</style>
