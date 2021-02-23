<template>
  <div>
    <el-input v-on:keyup.enter.native="keydown($event)" class="123"> </el-input>
    <el-input v-on:keyup.enter.native="keydown($event)" class="123"> </el-input>
    <el-input v-on:keyup.enter.native="keydown($event)" class="123"> </el-input>
    <el-input v-on:keyup.enter.native="keydown($event)" class="123"> </el-input>
    <input type="text" class="123" v-on:keyup.enter="keydown($event)" /><br />
    <input type="text" class="123" v-on:keyup.enter="keydown" /><br />
    <input type="text" class="123" /><br />
    <input type="text" class="123" /><br />
    <input type="text" class="123" /><br />
    <input type="text" class="123" /><br />
    <input type="text" class="123" /><br />
  </div>
</template>

<script>
export default {
  name: "inputEnter",
  components: {},
  // extends: null,
  // minxins: [],
  props: [],
  data() {
    return {};
  },
  computed: {},
  watch: {},
  beforeCreate() {},
  created() {},
  beforeMount() {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  beforeDestroy() {},
  destroyed() {},
  methods: {
    keydown(e) {
      console.log(e);

      let nodes = document.getElementsByClassName("123");
      for (let index = 0; index < nodes.length; index++) {
        const element = nodes[index].children[0];
        console.log(element);
        if (element === e.target) {
          console.log(index);
          if (index !== nodes.length - 1) {
            nodes[index + 1].children[0].focus();
          }
        }
      }
    },
  },
};
</script>

<style lang="less" scoped></style>
