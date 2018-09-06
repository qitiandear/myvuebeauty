<template>
  <div>
    <v-layout>
      <v-header>
        <v-dropdown class="mymenu" @mouseenter="msenter" @mouseleave="msleave">
          <v-icon type="appstore" v-if="isMenu"></v-icon>
          <v-icon type="appstore-o" v-if="!isMenu"></v-icon>
          菜单
        </v-dropdown>
      </v-header>
      <v-content>
        <router-view/>
      </v-content>
    </v-layout>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      isMenu:true,
    }
  },
  methods:{
    msenter(){
      this.isMenu = false
    },
    msleave(){
      this.isMenu = true
    }
  }
}
</script>

<style scoped>
@import './assets/main.css';
.ant-layout-header{
  padding: 0;
  background: #000;
  color: #fff;
  height: 50px;
  line-height: 50px;
  font-size: 18px;
  cursor: pointer;
}
</style>
