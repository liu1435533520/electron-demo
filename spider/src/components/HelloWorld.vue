<!--
 * @Author: your name
 * @Date: 2021-01-06 14:56:55
 * @LastEditTime: 2021-01-06 17:32:31
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \electron-demo\spider\src\components\HelloWorld.vue
-->
<template>
    <input type="text" v-model="dirPath">
    <button @click="selectDirPath">选择文件</button>
</template>

<script>
const { dialog } = require('electron').remote
import { defineComponent, ref } from 'vue'
export default defineComponent({
  name: 'HelloWorld',
  setup(){
    let dirPath = ref('');
    const selectDirPath =()=>{
      dialog.showOpenDialog(null, {
        title:"选择文件夹",
        properties: ['openDirectory']
      }).then(result => {
        dirPath.value = result.canceled?'':result.filePaths[0]
      }).catch(err => {
        console.log(err)
      })
    }
    return {
      dirPath,
      selectDirPath
    }
  }
})
</script>
