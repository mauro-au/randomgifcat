<template>
  <div class="app">
    <h1>{{msg}}</h1>
    <div class="row">
      <form class="form">
        <div class="form-group">
          <label>Tiulo:</label>
          <input type="text" v-model="datagif.title" />
        </div>

        <div class="form-group">
          <label>Filtro:</label>
          <select name='' v-model="datagif.filter" @Change='filterChange($event)'>
            <option value="blur">blur</option>
            <option value="mono">mono</option>
            <option value="sepia">sepia</option>
            <option value="negative">negative</option>
            <option value="paint">paint</option>
            <option value="pixel">pixel</option>
          </select>
        </div>

        <div class="form-group">
          <label for>Color:</label>
          <select name='' v-model="datagif.color" @Change='colorChange($event)'>
            <option value="red">Rojo</option>
            <option value="blue">Azul</option>
            <option value="green">verde</option>
            <option value="white">Blanco</option>
            <option value="yellow">Amarillo</option>
            <option value="black">Negro</option>
          </select>
        </div>
        <div class="form-group">
          <label for>Tamaño</label>
          <input type="number" v-model="datagif.size" />
        </div>
      </form>

      <button @click="gifcat">Obtener mi gato</button>
    </div>
    <div class="result__gif">
        <span v-show="datagif.isLoading">
            <img src="../assets/loading.svg" alt=""></span>
        <img v-show="!datagif.isLoading" :src="this.gif" alt=''/>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gif: "",
      datagif: {
        title: "",
        filter: "",
        color: "",
        size: 0,
        isLoading: false
      }
    };
  },
  props: {
    msg: String
  },
  methods: {
    gifcat() {
        this.datagif.isLoading = true

        fetch(
        `https://cataas.com/cat/gif/says/${this.datagif.title}?filter=${this.datagif.filter}&color=${this.datagif.color}&size=${this.datagif.size}`
        )
            .then(res => this.gif = res.url)
            .then(() => this.datagif.isLoading = false)
    },
    filterChange(event){
        this.datagif.filter = event.target.value
    },
    colorChange(event){
        this.datagif.color = event.target.value
    }
  }
};
</script>

<style>
body {
  background: lightblue;
  margin: 0;
  padding: 0;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
h1{
    text-align: center;
    font-size: 3rem;
}
.row {
  background: pink;
  display: flex;
  flex-direction: column;
}
.form {
  width: 50%;
  margin: 20px auto 0px auto;
  display: flex;
  flex-direction: column;
  align-items: center;
}
button{
    margin: 20px auto;
    cursor: pointer;
    border: none;
    padding: 10px;
    border-radius: 10px;
    width: 10%;
}
input{
    width: 180px;
    padding: 5px;
}
select{
    width: 195px;
    padding: 5px;
}
.form-group{
    margin: 10px;
}
label{
    margin: 10px;
}
.result__gif{
    display: flex;
    justify-content: center;
    margin: 50px 0;
}
</style>