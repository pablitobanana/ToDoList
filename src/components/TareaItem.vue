<template>
  <div id="TareaItem">
    <div
      class="alert alert-warning mt-3 d-flex justify-content-between align-item-center"
    >
    <p class="m-0" :class="{'tachado':tarea.isComplete}">{{ tarea.texto }}</p>
      <div>
        <i
          class="fas fa-undo-alt mx-2 text-success"
          role="button"
          @click="modificarTarea(tarea.id)"
          v-if="tarea.isComplete"
        ></i>
        <i
          class="fas fa-check-circle mx-2 text-success"
          role="button"
          @click="modificarTarea(tarea.id)"
          v-if="!tarea.isComplete"
        ></i>
        <i
          class="fas fa-minus-circle text-danger"
          role="button"
          @click="eliminarTarea(tarea.id)"
        ></i>
      </div>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
export default {
  name: "TareaItem",
  props: {
    tarea: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const tareas = inject("tareas");


    const modificarTarea = (id) => {
      tareas.value = tareas.value.map((item) => {
        if (item.id === id) {
          item.isComplete = !item.isComplete;
        }
        return item;
      });
    };

    const eliminarTarea = (idTarea) => {
      tareas.value = tareas.value.filter((item) => item.id !== idTarea);
    };
    return { eliminarTarea, modificarTarea };
  },
};
</script>

<style scoped>
.tachado{
  text-decoration: line-through;
}


</style>
