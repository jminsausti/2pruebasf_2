<template>
    <div class="home">
        <img alt="Turismo logo" src="../assets/turismo_200x200.png"> 
    </div>
    <h1>Creación de ruta turística</h1>
    <hr>
    <h3>Eventos</h3>
    <hr>
    <table class="content-table">
      <thead>
        <tr>
        <th scope="col">Evento</th>
        <th scope="col">Descripción</th>
        <th scope="col">Precio</th>
        <th scope="col">Stock</th>
      </tr>
      </thead>
      <tbody>
          <tr scope="row" v-for="evento in eventos">
          <td>{{ evento.documentName }}</td>
          <td>{{ evento.friendlyUrl }}</td>
          <td>{{ evento.eventStartDate }}</td>
          <td>{{ evento.territory }}</td>
          <!-- <td><button @click="factura(producto)">Comprar</button></td> -->
        </tr>
      </tbody>
    </table>
      
    <p><hr></p>
</template>

<script>
 import axios from 'axios';
 export default {
    data(){
      return{
        usuario:'',
        eventos:[],
        
      }
    },
      mounted() {
        
        this.cargarEventos()
      },
  methods:{
    cargarEventos(){
      axios.get('../json/agenda.json')
            .then((respuesta) => {
                console.log(respuesta);
                this.eventos = respuesta.data;
            });
    },
   
    }
  }
</script>
<style>
  table {
    width: 80%; 
    border-collapse: collapse;
    margin: 0 auto;
  }
th, td {
    padding: 8px;
    text-align: left;
    border: 1px solid #dee2e6;
  }
th {
  height: 40px;
  text-align: center;
  font-weight: bold;
  }
</style>