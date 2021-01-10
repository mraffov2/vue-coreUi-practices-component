<template>
  <div class="mt-3">
    <CProgress
      :value="counter"
      :color="color"
      animated
      show-value
      style="height:20px;"
      showPercentage
      class="mt-1"
    />
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "ProgressBar",
  data() {
    return {};
  },
  props: {
    counter: Number,
    color: String,
  },
  methods: {},
  computed: {},
  components: {
    //HelloWorld,
  },
};
</script>
