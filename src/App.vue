<template>
  <div>
    <TodoList />
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";

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
    TodoList
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
