<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      这是我的LeetCode刷题项目集，你可以
      <a href="https://leetcode.com/" target="_blank" rel="noopener">点击这里</a>前往LeetCode首页.
    </p>
    <!-- <p>该项目使用VUE-CLI3搭建</p> -->
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
