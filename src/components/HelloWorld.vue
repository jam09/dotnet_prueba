<template>
<Navbar></Navbar>
<div class="card">
  <div class="card-body">
    <form v-on:submit.prevent="multiplicar">
                    <div class="mb-3">
                        <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="dato1" v-model="dato1" required>
                    </div>
                    <div class="mb-3" style="margin-bottom:1rem">
                        <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="dato2" v-model="dato2" required>
                    </div>
                    <div class="mb-3">
                        <button class="btn btn-success" style="width:100%">Multiplicar</button>
                    </div>
                </form>

                <p>Dato1: {{dato1}}</p>
                <p>Dato2: {{dato2}}</p>
                <p>Resultado: {{resultado}}</p>
                <p>Fecha: {{fecha}}</p>
               <p> Error:<span style="color:red" >{{error}}</span></p> 
  </div>
</div>


</template>

<script>
import Navbar from '../components/navbar.vue'
import axios from "axios";
export default {
  name: 'HelloWorld',
  components: {
    Navbar
    },

    data() {
        return {
          dato1: '',
          dato2: '',
          resultado: '',
          fecha: '',
          error:''
        }
    },
    mounted() {   
},
methods:{
  multiplicar(){

    // https://testapimath.azurewebsites.net/api/Multiplica?dato1=2.5&dato2=0.5
    axios.get(`http://localhost:8080/api/Multiplica?dato1=${this.dato1}&dato2=${this.dato2}`, {headers:{
      "Access-Control-Allow-Origin": "*",
      "accept-ranges": "bytes",
      "content-type": "text/html; charset=UTF-8"
    }}).then(resp => {
      console.log(resp.data);
      this.resultado = resp.data.respuesta;
      this.fecha = resp.data.fecha;
      this.error = resp.data.error;
    }).catch((err) => {
      console.log(err);
    })

  }

}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border: 0;
    width: 25rem;
    border-radius: 0.35rem;
}
.card h3 {
    text-align: center;
    text-transform: uppercase;
    color: #043e00c2;
    font-weight: bold;
}
.card-header {
    background: #0a6e0b;
    border-bottom: 0;
}
.card-footer {
    color: #6c757d;
    font-size: 12px;
}
.form-check-input:checked {
    background-color: #198754;
    border-color: #198754;
}
.form-check-label{
    color: #6c757d;
}
</style>
