<template>
  <div class="appCalculator">
    <div id="calculator">
      <div class="container">
        <div class="image-container">
          <img src="../assets/logo.png">
          <img class="tf_logo" src="../assets/tf_logo.svg.png">
        </div>
        <form action="">

          <h1>House Calculator</h1>
          <button @click="nux">Button</button>
          <label for="rooms"># of Rooms</label>
          <input type="number" name="rooms" v-model.number="numRooms" />
          <br />
          <label for="sqaure-footage">Square Footage</label>
          <input type="number" name="sqaure-footage" v-model.number="squareFootage" />
          <br />
        </form>
        <div class="price">Predicted House Price: {{ price }}</div>
        <div>{{foo(this.numRooms, this.squareFootage)}}</div>
        <div class="price">TF Predicted House Price: {{ predictedPrice }}</div>
        <!-- <div>{{bar(this.numRooms, this.squareFootage)}}</div> -->
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
        price: 0,
        squareFootage: 0,
        numRooms: 0,
        predictedPrice: 0,
      }
    },
    computed: {},
    methods: {
      nux() {
        tf.tensor([1, 2, 3, 4]).print();
      },
      foo(numRooms, squareFootage) {
        return tf.tidy(() => {
          const a = tf.tensor([Number.parseInt(numRooms)])
          const b = tf.variable(tf.scalar(Number.parseInt(squareFootage)))
          const results = a.add(b);
          results.data().then(results => {
            this.price = results[0]
          })
        });
      },
      // bar(numRooms, squareFootage) {
      //   return tf.tidy(() => {
      //     const model = tf.sequential()
      //     model.add(tf.layers.dense({
      //       units: 1,
      //       inputShape: [2]
      //     }))

      //     const xs = tf.tensor2d([
      //       [1, 2],
      //       [1, 3]
      //     ], [2, 2])
      //     const ys = tf.tensor2d([
      //       [1],
      //       [2]
      //     ], [2, 1])

      //     model.compile({
      //       loss: 'meanSquaredError',
      //       optimizer: 'sgd'
      //     })

      //     await model.fit(xs, ys, {epochs: 100, callbacks: {
      //       onEpochEnd: async (epoch, log) => {
      //         console.log(`Epoch ${epoch}: loss = ${log.loss}`
      //         )}
      //       }
      //     })

      //     model.predict(tf.tensor2d([5], [1, 1])).print();
      //     // Train the model using the data.
          // model.fit(xs, ys, {
          //   epochs: 1
          // }).then(() => {
          //   const output = model.predict(tf.tensor2d([numRooms, squareFootage], [1, 2])).data()
          //   return output
          // })
        // })
      // }
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

.tf_logo {
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
