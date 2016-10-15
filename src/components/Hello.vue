<template>
  <div class="hello">
    <tabbar>
      <tabbar-item>
        <img slot="icon" src="../assets/demo/icon_nav_button.png">
        <span slot="label">俯卧撑</span>
      </tabbar-item>
      <tabbar-item show-dot>
        <img slot="icon" src="../assets/demo/icon_nav_msg.png">
        <span slot="label">仰卧起坐</span>
      </tabbar-item>
      <tabbar-item selected>
        <img slot="icon" src="../assets/demo/icon_nav_article.png">
        <span slot="label">平板支撑</span>
      </tabbar-item>
    </tabbar>
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Hello Vue!'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: #42b983;
}
</style>
