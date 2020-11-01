<template>
  <div>
    <div class="input">
      <input v-model="inputContent" />
      <div class="list_add" @click="addList">添加</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      inputContent: ""
    };
  },
  props: {
    content: {
      type: String
    },
    lists: {
      type: Array
    }
  },
  methods: {
    async addList() {
      //   this.$emit("addList");
      let index =
        this.lists.length > 0 ? this.lists[this.lists.length - 1].id + 1 : 0;
      let url = `https://oqqgsl-wgafte-8080.preview.myide.io/posts`;
      let body = JSON.stringify({
        id: index,
        content: this.inputContent
      });
      let result = await fetch(url, {
        method: "post",
        body,
        headers: {
          "Content-Type": "application/json"
        }
      });
      console.log(result, "添加返回结果");
      let res = await result.json();
      console.log(res);
      if (result.status === 201) {
        this.$emit("update:lists", [...this.lists, res]);
        this.inputContent = "";
        console.log(this.inputContent, "this.inputContent");
      } else {
        alert("添加错误");
      }
    }
  },
  watch: {
    inputContent(newVal, oldVal) {
      console.log(newVal, oldVal, "inputContent");
      this.$emit("update:content", newVal);
    },
    content(newVal, oldVal) {
      console.log(newVal, oldVal, "child content");
    }
  }
};
</script>
<style scoped>
.input {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 42px;
}
.input input {
  padding: 5px;
}
.list_add {
  color: #fff;
  background: rgb(65, 184, 132);
  padding: 5px;
  margin-left: 10px;
}
</style>