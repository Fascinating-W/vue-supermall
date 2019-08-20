<template>
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive"><slot name="item-icon"></slot></div>
    <div v-else><slot name="item-icon-active"></slot></div>
    <div :style="activeStyle"><slot name="item-text"></slot></div>
  </div>
</template>
<script>
export default {
  props: {
    path: String,
    activeColor: {
      type: String,
      default: 'red'
    }
  },
  data() {
    return {

    }
  },
  computed: {
    isActive() {
      //判断当前活动路由是否包含 props传进来的path,不等于-1代表找到了
      return this.$route.path.indexOf(this.path) != -1
    },
    activeStyle() {
      // 是否处于活跃，活跃绑定样式
      return this.isActive ? {color: this.activeColor} : {}
    }
  },
  methods: {
    itemClick() {
      this.$router.push({
        path: this.path
      })
    }
  },

}
</script>
<style>
#tab-bar{
  display: flex;
  background-color: #f6f6f6;

  position: fixed;
  bottom: 0;
  right: 0;
  left: 0;

  box-shadow: 0 -5px 1px rgba(100,100,100,.2)
}
.tab-bar-item{
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
} 
.tab-bar-item img{
  height: 24px;
  width: 24px;
  margin-top: 3px;
  vertical-align: middle;
  margin-bottom: 2px;
}
.active{
  color: cyan;
}
</style>