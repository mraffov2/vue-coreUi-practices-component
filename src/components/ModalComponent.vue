<template>
  <div>
    <CButton @click="showModal = true" color="primary">
      Open modal
    </CButton>
    <CModal
      :title="title"
      :color="color"
      :show.sync="showModal"
      @update:show="showModal = false"
    >
      {{ content }}
    </CModal>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "ModalComponent",
  data() {
    return {
      showModal: false,
    };
  },
  props: {
    title: String,
    color: String,
    content: String,
  },
  methods: {},
  computed: {},
  components: {
    //HelloWorld,
  },
};
</script>
