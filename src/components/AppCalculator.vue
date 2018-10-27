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
          <p>Discover your monthly car payment.</p>
          <label for="price"># of Rooms</label>
          <input type="number" name="price" class="currency" v-model.number="price" />
          <br />
          <label for="down-payment">Square Footage</label>
          <input type="number" name="down-payment" class="currency" v-model.number="downPayment" />
          <br />
        </form>
        <div class="payment">Predicted House Price: {{ totalPayment }}</div>
        <div>{{sampleCal()}}</div>

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
        downPayment: '',
        tradeIn: '',
        length: '60',
        rate: '',
        calcPayment: ''
      }
    },
    computed: {
      totalPayment() {
        var p = this.price - this.downPayment - this.tradeIn;
        var r = this.rate / 1200;
        var n = this.length;
        var i = Math.pow((1 + r), n);
        return (p * r * i) / (i - 1) || 0;
      },
    },
    methods: {
      sampleCal() {
        // Define a model for linear regression.
        const model = tf.sequential();
        model.add(tf.layers.dense({
          units: 1,
          inputShape: [1]
        }));

        // Prepare the model for training: Specify the loss and the optimizer.
        model.compile({
          loss: 'meanSquaredError',
          optimizer: 'sgd'
        });

        // Generate some synthetic data for training.
        const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
        const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

        // Train the model using the data.
        model.fit(xs, ys, {
          epochs: 10
        }).then(() => {
          // Use the model to do inference on a data point the model hasn't seen before:
          model.predict(tf.tensor2d([5], [1, 1])).print();
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
