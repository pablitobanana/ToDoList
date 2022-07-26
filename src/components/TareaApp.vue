<template>
  <div id="TareaApp">
    <h1>App Tareas</h1>
    <tarea-form />
    <tarea-item v-for="tarea in tareas" :key="tarea.id" :tarea="tarea" />
    <div class="alert alert-dark mt-3" v-if="tareas.length === 0">
      Sin tareas pendientes
    </div>
  </div>
</template>

<script>
import TareaForm from "@/components/TareaForm.vue";
import TareaItem from "@/components/TareaItem.vue";
import { provide, ref, watchEffect } from "vue";
export default {
  name: "TareaApp",
  components: { TareaForm, TareaItem },
  setup() {
    const tareas = ref([]);
    provide("tareas", tareas);

    if (localStorage.getItem('tareas')) {
      tareas.value = JSON.parse(localStorage.getItem('tareas'));
    }

    watchEffect(() => {
      localStorage.setItem("tareas", JSON.stringify(tareas.value));
    });

    return { tareas };
  },
};
</script>

<style scoped></style>
