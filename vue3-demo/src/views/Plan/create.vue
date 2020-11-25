<template>
  <a-form :model="form" :label-col="{ span: 4 }" :wrapper-col="{ span: 4 }">
    <a-form-item label="Activity time">
      <a-date-picker
        v-model:value="form.date"
        show-time
        type="date"
        placeholder="Pick a date"
        style="width: 100%;"
      />
    </a-form-item>
    <a-form-item label="请输入耗时">
      <a-input-number v-model:value="form.time" :min="1" :max="10"></a-input-number>
    </a-form-item>
    <a-form-item label="请输入代办事项">
      <a-textarea v-model:value="form.content" placeholder="Basic usage" :rows="4" />
    </a-form-item>
    <a-form-item>
      <a-button type="primary" @click="onSubmit">创建任务</a-button>
    </a-form-item>
  </a-form>
</template>
<script>
import { reactive, toRefs } from 'vue'
import moment from 'moment'
export default {
 setup(){
   const state = reactive({
     form:{
       date:moment(Date.now()).format('YYYY-MM-DD'),
       time:0,
       content:''
     }
   })
   const onSubmit = ()=>{
     console.log(state.form)
   }
   return {
     ...toRefs(state)
   }
 }
};
</script>
