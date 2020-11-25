<template>
  <a-layout id="components-layout-demo-top-side-2">
    <a-layout-header class="header">
      <div class="logo" />
      <a-menu theme="dark" mode="horizontal" v-model:selectedKeys="selectedKeys1" :style="{ lineHeight: '64px' }">
        <a-menu-item key="/">
          <router-link to="/">首页</router-link>
        </a-menu-item>
        <a-menu-item key="/plan">
          <router-link to="/plan">时间计划</router-link>
        </a-menu-item>
      </a-menu>
    </a-layout-header>
    <a-layout>
      <a-layout style="padding: 0 24px 24px">
        <a-layout-content :style="{ background: '#fff', padding: '24px', margin: 0, minHeight: '280px' }">
          <a-row>
            <a-col :span="6">
              <a-card title="计划总用时是：" style="width:100%"><p>总共计划时长是：{{allTime}}</p></a-card>
            </a-col>
            <a-col :span="16" :offset="2">
               <router-view></router-view>
            </a-col>
          </a-row>
         
        </a-layout-content>
      </a-layout>
    </a-layout>
  </a-layout>
</template>
<script>
import { reactive, toRefs, watch, computed, ref } from 'vue'
import { useRoute } from 'vue-router'
import { useStore } from 'vuex'
export default {
  created() {
    console.log('created')
  },
  setup(props, context) {
    console.log('setup', props, context)
    // 默认只执行一次 先执行setup再执行created
    // return ()=>(<h1>hello</h1>)// setup执行完成后返回的就是render函数
    const store = useStore()
    const state = reactive({
      a: 1,
      allTime: ref(store.getters.allTime) //将普通的值包裹成响应式的
      // selectedKeys:computed(()=>{
      //   return [route.path]
      // })//这样写也可以
    })
    const route = useRoute()
    // watch(()=>route.path,(newValue)=>{
    //   state.selectedKeys1 = [newValue]
    // },{immediate:true})//immediate:true立即执行
    const selectedKeys = computed(() => {
      return [route.path]
    })

    setTimeout(() => {
      state.a = 1000
    }, 2000)
    return {
      selectedKeys1: selectedKeys,
      ...toRefs(state) // toRefs保证数据是响应式的
    }
  }
}
</script>

<style>
#components-layout-demo-top-side-2 .logo {
  width: 120px;
  height: 31px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px 28px 16px 0;
  float: left;
}
</style>
