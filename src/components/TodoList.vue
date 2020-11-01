<template>
  <div>
    <inputList
      class="list_input"
      :lists="lists"
      @update:lists="lists = $event"
      :content="content"
      @update:content="content = $event"
      @addList="addList"
    />
    <!-- 这种写法失效 -->
    <!-- <inputList class="list_input" :content.sync="content" @addList="addList" /> -->
    <template v-if="lists.length > 0">
      <list
        v-for="(list, index) in lists"
        :key="list.id"
        :list="list"
        :index="index"
        @delList="delList"
      />
    </template>
    <div v-if="lists.length <= 0">额...没有数据了</div>
  </div>
</template>
<script>
import list from "./list.vue";
import inputList from "./listInput.vue";
export default {
  data() {
    return {
      lists: [],
      content: ""
    };
  },
  components: {
    list,
    inputList
  },
  props: {},
  setup(props, context) {},
  async mounted() {
    let url = "https://oqqgsl-wgafte-8080.preview.myide.io/posts";
    let result = await fetch(url, {
      method: "get"
    }).then(res => res.json());
    this.lists = result;
    console.log(result, "结果");
  },
  unmounted() {},
  methods: {
    async addList() {},
    async delList(index, list) {
      console.log("删除", index, list);
      let url = `https://oqqgsl-wgafte-8080.preview.myide.io/posts/${list.id}`;
      try {
        let result = await fetch(url, {
          method: "delete"
        });
        console.log(result, "删除返回结果");
        let res = await result.json();
        console.log(res);
        if (result.status === 200) {
          this.lists.splice(index, 1);
        } else {
          alert("删除错误");
        }
      } catch (error) {
        console.log(error);
      }
    }
  },
  watch: {
    content(newVal, oldVal) {
      console.log(newVal, oldVal, "content");
    }
  },
  computed: {}
};
</script>
<style scoped>
.list_input {
  padding: 10px;
}
</style>