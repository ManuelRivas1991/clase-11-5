<template>
    <h1 v-if="estado">Soy el sistema de tareas</h1>
    <button v-on:click="estado=!estado">{{ estado ? 'Desaparece' : 'Aparece'}}</button>
    {{ hola }}

<button v-on:click="hecho = true">
    Para hacer
</button>
<button v-on:click="hecho = false">
    Realizadas
</button>

<div v-for="(tar,index) in tareas" :key="index" >
    <div class="cuadrado" v-if="hecho ? !tar.estado && !tar.dadoDeBaja : tar.estado&&!tar.dadoDeBaja">
        {{tar.tarea}}
    <button v-on:click="tar.estado = !tar.estado">
        {{ hecho ? 'Realizada' : 'Reanudar' }}
    </button>
    <button v-on:click="tar.dadoDeBaja = true">
        Dar de baja
    </button>
    <button v-on:click="eliminar(index)">ELiminar tarea</button>
    </div>
</div>

<input type="text" v-model="nuevaTarea">
<button v-on:click="cargar">Crear Tarea</button>

</template>

<script>
export default {
  name: 'TasksComponent',
  data() {
    return {
        hola: "Hola como andas?",
        estado: true,
        hecho: true,
        nuevaTarea: '',
        dadoDeBaja: false,
        tareas: [
            {
                id:0,
                tarea: "Algo para hacer 1",
                realizado: false
            },
            {
                id:1,
                tarea: "Algo para hacer 2",
                realizado: false
            },
            {
                id:2,
                tarea: "Algo para hacer 3",
                realizado: false
            },
            {
                id:3,
                tarea: "Algo para hacer 4",
                realizado: false
            }
        ]

    }
 },
  methods: {
   cargar : function () {
    this.tareas.push({
        id: this.tareas.lenght ? this.tareas.lenght : 0,
        tarea: this.nuevaTarea,
        estado: false
    })
   },
   eliminar:function(index){
            if (confirm("Eliminar Tarea?")){
                this.tareas.splice(index, 1)
            }
             
        }
  }
}
</script>

<style scoped>

.cuadrado {
    border: solid 2px black;
    padding: 10px;
    margin: 5px;
}

</style>
