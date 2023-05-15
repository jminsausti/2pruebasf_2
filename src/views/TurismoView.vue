<template>
    <div class="home">
        <img alt="Turismo logo" src="../assets/turismo_200x200.png"> 
    </div>
    <h1>Creación de ruta turística</h1>
  
    <h3>Eventos</h3>
    <label for="territorios">Selecciona provincia:</label>
    <select v-model="territorio">
      <option disabled value="">Elige una opción</option>
      <option>Todos</option>
      <option>Araba</option>
      <option>Bizkaia</option>
      <option>Gipuzkoa</option>
    </select>
    <hr>
    <table class="content-table">
      <thead>
        <tr>
        <th scope="col">Evento</th>
        <th scope="col">URL</th>
        <th scope="col">Fecha</th>
        <th scope="col">Territorio</th>
      </tr>
      </thead>
      <tbody>
          <tr class="bizkaiaClass" scope="row" v-for="evento in eventosSelect">
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
        territorio:[]
        
      }
    },
      mounted() {
        
        this.cargarEventos()
      },
      computed:{
        eventosSelect(){
          if (this.territorio != "Todos")
            return this.eventos.filter((evento) => evento.territory == this.territorio);
          else  
            return this.eventos
        }
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
  background-color: darkgrey;
  height: 40px;
  text-align: center;
  font-weight: bold;
  }
.bizkaiaClass {
    background-color: chartreuse;
  }
</style>