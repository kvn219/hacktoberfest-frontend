<template>
  <div class="appCalculator">
    <div id="calculator">
      <div class="container">
          <div class="image-container">
            <img alt="Vue logo" src="../assets/logo.png">
            <img alt="" src="../assets/tf_logo.svg.png" class="tf">
          </div>
        <form action="">

          <h1>House Calculator</h1>
          <p>Estimated price.</p>
          <label for="rooms"># of Rooms</label>
          <input type="number" name="rooms" v-model.number="numRooms" />
          <br />
          <label for="sqaure-footage">Square Footage</label>
          <input type="number" name="sqaure-footage" v-model.number="squareFootage" />
          <br />
        </form>
        <div class="price">Predicted House Price: {{ price }}</div>
        <div>{{foo(this.numRooms, this.squareFootage)}}</div>

      </div>
    </div>
  </div>
</template>

<script>
  import * as tf from '@tensorflow/tfjs'
  export default {
    name: 'AppCalulator',
    data() {
      return {
        price: '',
        squareFootage: '',
        numRooms: ''
      }
    },
    computed: {},
    methods: {
      foo(numRooms, squareFootage) {
        return tf.tidy(()=>{
          const a = tf.tensor([Number.parseInt(numRooms)])
          const b = tf.variable(tf.scalar(Number.parseInt(squareFootage)))
          return a.mul(b);
      });
    }
  }
}
</script>

<style lang="scss" scoped>
* {
  box-sizing: border-box;
}

html {
  font-family: "proxima-nova", "Helvetica Neue", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
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

.tf {
  height: 170px;
  width: 170px;
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
  font-size: 24px;
  padding: 0 16px;
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

.payment {
  color: #000;
  font-size: 24px;
  text-align: center;
  font-weight: bold;
  transition: all 0.3s ease-in;
  @media (max-width: 512px) {
    font-size: 40px;
    transition: all 0.3s ease-in;
  }
  @media (max-width: 400px) {
    font-size: 32px;
    transition: all 0.3s ease-in;
  }
}

@media (max-height: 750px) {
  body {
    height: 50%;
  }
}
</style>
