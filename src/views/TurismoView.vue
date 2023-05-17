<template>
    <div class="home">
        <img alt="Turismo logo" src="../assets/turismo_200x200.png"> 
        <img alt="Turismo logo" src="../assets/like_2.png"> 
    </div>
    <h1>Creación de ruta turística</h1>
  
    <h3>FILTROS</h3>
    <p>Los filtros NO son excluyentes, es decir se puede filtrar por territorio, por mes del evento y por territorio y mes</p>
    <label for="territorios">Selecciona provincia:</label>
    <select v-model="territorio">
      <option disabled value="">Elige una opción</option>
      <option>Todos</option>
      <option>Araba</option>
      <option>Bizkaia</option>
      <option>Gipuzkoa</option>
    </select>
    
    <label for="Fechas">Selecciona mes del evento:</label>
    <select v-model="mes">
      <option  value="">Elige una opción (Todos)</option>
      <option value="01">Enero</option>
      <option value="02">Febrero</option>
      <option value="03">Marzo</option>
      <option value="04">Abril</option>
      <option value="05">Mayo</option>
      <option value="06">Junio</option>
      <option value="07">Julio</option>
      <option value="08">Agosto</option>
      <option value="09">Setiembre</option>
      <option value="10">Octubre</option>
      <option value="11">Noviembre</option>
      <option value="12">Diciembre</option>
    </select>
    <hr><hr>
    <table class="content-table">
      <thead>
        <tr>
        <th scope="col">Evento</th>
        <th scope="col">Fecha</th>
        <th scope="col">Territorio</th>
        <th scope="col">Descripción</th>
        <th scope="col">Más Info</th>
      </tr>
      </thead>
      <tbody>
          <tr :style="backClass(evento.territory)" scope="row" v-for="evento in eventosSelect">
          <td>{{ evento.documentName }}</td>
          <td>{{ evento.eventStartDate }}</td>
          <td>{{ evento.territory }}</td>
          <td>{{ evento.documentDescription }}</td>
          <td><a  target="_BLANK" :href="evento.friendlyUrl">{{ evento.friendlyUrl }}</a></td>
          <td><img class="imagen" src="../assets/like_2.png" alt="like" @click="like(evento)"></td>

          <!-- <td><button @click="masInfo(evento)">Más información</button></td> -->
         
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
        territorio:'',
        mes:'',
        rowColor:'',
        imagenLike:''
        
      }
    },
      mounted() {
        this.cargarEventos()
      },
      computed:{
        eventosSelect(){
          if (this.territorio != "Todos"){
            if (this.mes !="")
              return this.eventos.filter((evento) => (evento.territory == this.territorio) && (evento.eventStartDate.substring(3,5)==this.mes) );
            if (this.mes =='')
              return this.eventos.filter((evento) => (evento.territory == this.territorio))
          }
          else {
            if (this.mes !="")
              return this.eventos.filter((evento) => (evento.eventStartDate.substring(3,5)==this.mes))
            if (this.mes =='')
              return this.eventos;

            /* if(this.territorio=="Bizkaia") this.rowColor='chartreuse';
            if(this.territorio=="Gipuzkoa") this.rowColor='darkkhaki'; */
            
          } 
            
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
    backClass(valor){
      //alert(valor)
      if (valor=="Araba"){
        return {'background-color':'coral'}
      }
      else if (valor=="Bizkaia"){
        return {'background-color':'bisque'}
      }
      else if (valor == "Gipuzkoa"){
        return {'background-color':'darkkhaki'}
      }
    },
    like(e){
      if (e.target.src="../assets/like_2.png")
        e.target.src="../assets/like.png"
      else
        e.target.src="../assets/like_2.png"
    }
    
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
  .arabaClass{
  background-color: coral;
}
.bizkaiaClass {
    background-color: bisque;
  }
.gipuzkoaClass{
  background-color: darkkhaki;
}
.imagen{
  height: 60px;
  width: 60px;
}

</style>