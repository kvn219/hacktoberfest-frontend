<template>
  <div class="appCalculator">
    <div id="calculator">
      <div class="container">
        <div class="image-container">
          <img class="logo" src="../assets/logo.png">
          <img class="logo" src="../assets/tf_logo.svg.png">
        </div>
        <form action="">
          <h2>House Calculator</h2>
          <label for="rooms"># of Rooms</label>
          <input autofocus autocomplete="off" type="number" name="rooms" v-model.number="numRooms" />
          <br />
          <label for="sqaure-footage">Square Footage</label>
          <input type="number" name="sqaure-footage" v-model.number="squareFootage" />
          <br />
        </form>
        <button class="button" @click="train()" type="button">Train</button>
        <button class="button" @click="predict()" type="button">Predict</button>
        <div class="price">Predicted Price: {{ predictedPrice }}</div>
      </div>
    </div>
  </div>
</template>

<script>
  import * as tf from '@tensorflow/tfjs'
  export default {
    name: 'AppCalulator',
    filters: {
      displayNum(x) {
        return Math.round(x * 1000) / 1000
      }
    },
    data() {
      return {
        predictedPrice: null,
        squareFootage: null,
        numRooms: null,
        trained: false,
      }
    },
    methods: {
      async train() {
        const model = this.model = tf.sequential()
        model.add(tf.layers.dense({
          units: 1,
          inputShape: [2]
        }))
        model.compile({
          loss: 'meanSquaredError',
          optimizer: 'sgd'
        })
        const xs = tf.tensor2d([
          [1, 2],
          [3, 4],
          [3, 5],
          [3, 10],
          [1, 1]
        ])
        const ys = tf.tensor2d([
          [1],
          [1],
          [3],
          [6],
          [8]
        ])

        const epochs = 10

        for (let i=1; i<epochs+1; i++) {
          const results = await model.fit(xs, ys, {batchSize: 1, epochs: epochs})
          const loss = results.history.loss[0]
          console.log(`Loss ${i}/${epochs}:\t${loss}`)
        }

      },
      predict() {
        return tf.tidy(() => {
          const inputs = [
            [this.numRooms, this.squareFootage]
          ]
          this.predictedPrice = this.model.predict(
            tf.tensor2d(inputs, [1, 2])
          ).dataSync()[0]
        })
      }
    }
  }
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
  height: 150px;
  width: 150px;
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
</style>
