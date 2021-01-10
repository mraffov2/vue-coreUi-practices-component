<template>
  <div class="container">
    <CJumbotron class="mb-6">
      <h1 class="display-4">CORE UI Bootstrap 4 - Vue js</h1>
      <p class="lead">Bootstrap 4 Components for Vue.js</p>
    </CJumbotron>
    <hr />

    <ModalComponent
      :title="titleModal"
      :color="modalColor"
      :content="content"
      class="mb-5"
    />

    <div class="text-center mt-6">
      <div class="mt-3">
        <hr />
      </div>
      <div class="row justify-content-center">
        <div class="col">
          <CButton color="primary" @click="sumarCount">
            Sumar +
          </CButton>
        </div>
        <div class="col">
          <h3>{{ count }}</h3>
        </div>
        <div class="col">
          <CButton color="danger" @click="restarCount">
            Restar -
          </CButton>
        </div>
      </div>
      <ProgressBar :counter="count" :color="colorBar" />
    </div>

    <div class="mt-4">
      <CSelect
        label="Background Text"
        :options="optionsSelescts"
        @update:value="colorText = $event"
      />
      <div :class="colorText" class="p-3 text-white">
        ¿Qué es Lorem Ipsum? Lorem Ipsum es simplemente el texto de relleno de
        las imprentas y archivos de texto. Lorem Ipsum ha sido el texto de
        relleno estándar de las industrias desde el año 1500, cuando un impresor
        (N. del T. persona que se dedica a la imprenta) desconocido usó una
        galería de textos y los mezcló de tal manera que logró hacer un libro de
        textos especimen. No sólo sobrevivió 500 años, sino que tambien ingresó
        como texto de relleno en documentos electrónicos, quedando esencialmente
        igual al original. Fue popularizado en los 60s con la creación de las
        hojas "Letraset", las cuales contenian pasajes de Lorem Ipsum, y más
        recientemente con software de autoedición, como por ejemplo Aldus
        PageMaker, el cual incluye versiones de Lorem Ipsum.
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";
import ModalComponent from "../components/ModalComponent.vue";
import ProgressBar from "..//components/ProgressBarComponent.vue";

export default {
  name: "Home",
  data() {
    return {
      warningModal: false,
      titleModal: "Modal title",
      modalColor: "primary",
      count: 0,
      content:
        "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod",
      optionsSelescts: [
        { value: "bg-primary", label: "PRIMARY" },
        { value: "bg-danger", label: "DANGER" },
        { value: "bg-info", label: "INFO" },
        { value: "bg-success", label: "SUCCESS" },
      ],
      colorText: "bg-primary",
    };
  },
  methods: {
    sumarCount() {
      if (this.count < 100) {
        this.count++;
      }
    },
    restarCount() {
      if (this.count !== 0) {
        this.count--;
      }
    },
  },
  computed: {
    colorBar() {
      if (this.count <= 20) return "danger";
      if (this.count > 20 && this.count <= 45) {
        return "warning";
      }
      if (this.count > 45 && this.count < 75) {
        return "info";
      } else return "success";
    },
    colorTextinput() {
      return this.colorText;
    },
  },
  updated() {
    console.log(this.inputSelect);
  },
  components: {
    //HelloWorld,
    ModalComponent,
    ProgressBar,
  },
};
</script>
