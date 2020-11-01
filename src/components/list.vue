<template>
  <div class="list_out">
    <div>{{list.id}}</div>
    <div>{{list.content}}</div>
    <div class="list_del" @click="delList">删除</div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
  props: {
    list: {
      type: Object
    },
    index: {
      type: Number
    }
  },
  setup(props, context) {},
  mounted() {},
  unmounted() {},
  methods: {
    delList() {
      console.log(this.index);
      this.$emit("delList", this.index, this.list);
    }
  },
  watch: {},
  computed: {}
};
</script>
<style scoped>
.list_out * {
  box-sizing: border-box;
}
.list_out {
  display: flex;
  justify-content: center;
  align-items: center;
}
.list_out div {
  margin-left: 10px;
  padding: 5px;
}
.list_del {
  color: #fff;
  background: rgb(241, 73, 73);
  cursor: pointer;
}
</style>