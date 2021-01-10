<template>
  <div class="container text-center">
    <!-- ####### ALERT ####### -->
    <CAlert color="success" :show.sync="currentAlertCounter" closeButton>
      {{ messageAlert }}, esta alerta se cerrara en:
      {{ currentAlertCounter }} segundos.
      <CProgress
        :max="10"
        :value="currentAlertCounter"
        height="3px"
        color="success"
        animate
      />
    </CAlert>

    <div class="about row p-3 justify-content-center">
      <!-- ####### FORMULARIO ####### -->
      <div class="col-sm-10 col-md-5 mb-5">
        <h3 class="mb-5">Formulario</h3>
        <CCard bodyWrapper class="mt-3 form-tareas">
          <div class="mt-5" style="text-align: left">
            <CInput
              label="Titulo de la Tarea"
              placeholder="Introduzca un titulo para la tarea"
              v-model="titleTask"
            />
          </div>
          <div class="mt-5" style="text-align: left">
            <CInput
              label="Description de la tarea"
              placeholder="Introduzca una description para la tarea"
              v-model="descriptionTask"
            />
          </div>
          <p class="text-danger" v-if="fieldRequired">
            Todos los campos son reuqeridos
          </p>
          <CCardFooter>
            <div class="row justify-content-end">
              <div class="col">
                <CButton
                  color="primary"
                  v-bind="propsButton"
                  @click="saveTask"
                  v-if="!editTaskStatus"
                >
                  Guardar
                </CButton>
                <CButton
                  color="primary"
                  v-bind="propsButton"
                  @click="updateTask"
                  v-if="editTaskStatus"
                >
                  Actualizar
                </CButton>
              </div>
              <div class="col-auto">
                <CButton color="danger" v-bind="propsButton">
                  Cancelar
                </CButton>
              </div>
            </div>
          </CCardFooter>
        </CCard>
      </div>

      <!-- ####### LISTA DE TAREAS ###### -->
      <div class="col-sm-12 col-md-7">
        <h2 class="text-left mb-5">Lista de tareas</h2>
        <CCard bodyWrapper v-for="(task, index) in tasks" :key="index">
          <div class="row justify-content-center">
            <div class="col-2">
              {{ task.title }}
            </div>
            <div class="col">
              {{ task.description }}
            </div>
            <div class="col-auto">
              <CButton
                color="primary"
                v-bind="propsButton"
                size="sm"
                @click="editTask(index)"
              >
                Editar <CIcon size="sm" name="cil-pencil" />
              </CButton>
            </div>
            <div class="col-auto">
              <CButton
                color="danger"
                size="sm"
                v-bind="propsButton"
                @click="deleteTask(task)"
              >
                Eliminar <CIcon size="sm" name="cil-delete" />
              </CButton>
            </div>
          </div>
        </CCard>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      propsButton: { shape: "pill" },
      tasks: [
        {
          title: "tarea 1",
          description: "Descripcion tarea 1",
          id: 1,
        },
        {
          title: "tarea 2",
          description: "Descripcion tarea 2",
          id: 2,
        },
        {
          title: "tarea 3",
          description: "Descripcion tarea 3",
          id: 3,
        },
        {
          title: "tarea 4",
          description: "Descripcion tarea 4",
          id: 4,
        },
      ],
      titleTask: "",
      descriptionTask: "",
      fieldRequired: false,
      editTaskStatus: false,
      indexIdUpdateTask: 0,
      currentAlertCounter: 0,
      messageAlert: "",
    };
  },
  components: {},
  methods: {
    async saveTask() {
      this.fieldRequired = false;
      if (this.titleTask !== "" && this.descriptionTask !== "") {
        let id = this.tasks.lebgth + 1;
        const newTask = {
          title: this.titleTask,
          description: this.descriptionTask,
          id: id,
        };
        this.tasks = await [newTask, ...this.tasks];
        this.fieldRequired = false;
        this.titleTask = "";
        this.descriptionTask = "";
        this.messageAlert = "Tarea agregada con exito";
        this.currentAlertCounter = 5;
      } else {
        this.fieldRequired = true;
      }
    },
    editTask(index) {
      this.editTaskStatus = true;
      this.indexIdUpdateTask = index;
      this.titleTask = this.tasks[index].title;
      this.descriptionTask = this.tasks[index].description;
    },
    updateTask() {
      if (this.titleTask !== "" && this.descriptionTask !== "") {
        let index = this.indexIdUpdateTask;
        this.editTaskStatus = false;
        this.tasks[index].title = this.titleTask;
        this.tasks[index].description = this.descriptionTask;
        this.fieldRequired = false;
        this.titleTask = "";
        this.descriptionTask = "";
        this.messageAlert = "Tarea actualizada con exito";
        this.currentAlertCounter = 5;
      } else {
        this.fieldRequired = true;
      }
    },
    deleteTask(task) {
      let item = this.tasks.indexOf(task);
      if (item !== -1) {
        this.tasks.splice(item, 1);
      }
      this.messageAlert = "Tarea eliminada con exito";
      this.currentAlertCounter = 5;
    },
  },
  computed: {},
};
</script>
<style lang="scss">
.form-tareas {
}
</style>
