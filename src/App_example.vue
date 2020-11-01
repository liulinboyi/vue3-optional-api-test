<template>
  <div>
    <button @click="showHandler">点击</button>
    <button @click="inverseShowHander">反转</button>
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld v-if="show" msg="Hello Vue 3.0 + Vite" />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  data() {
    return {
      show: true
    };
  },
  beforeCreate() {
    console.log("beforeCreate");
  },
  created() {
    console.log("created");
    this.$watch(
      "show",
      function(newVal, oldVal) {
        console.log(newVal, oldVal, "watch show");
      },
      {
        immediate: true,
        deep: true
      }
    );
  },
  setup(props, context) {},
  components: {
    HelloWorld
  },
  methods: {
    showHandler() {
      this.show = !this.show;
      console.log(this.inverseShow, "反转show");
    },
    inverseShowHander() {
      this.inverseShow = false;
      console.log(this.inverseShow, "反转show");
    }
  },
  computed: {
    inverseShow: {
      get() {
        return !this.show;
      },
      set(val) {
        this.show = val;
      }
    }
  }
  // watch: {
  //   show: function(newVal, oldVal) {
  //     console.log(newVal, oldVal, 'watch show')
  //   }
  // }
};
</script>
