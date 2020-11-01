<template>
  <div>
    <h1>{{ msg }}</h1>
    <button @click="count++">count is: {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test hot module replacement.
    </p>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  setup(props, context) {
    const msg = props.msg
    console.log(props, context)
    // return {msg}
    return {}
  },
  beforeMount() {
    console.log('beforemount', this.msg)
  },
  mounted() {
    console.log('mounted', this.msg)
  },
  beforeUnmount() {
    console.log("beforedestory => beforeUnmount", this.msg)
  },
  unmounted() {
    console.log("destoryed => unmounted", this.msg)
  },
  props: {
    msg: String
  },
  data() {
    return {
      count: 0
    };
  }
};
</script>
