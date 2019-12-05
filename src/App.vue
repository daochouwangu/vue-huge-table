<template>
  <div id="app">
    <Table v-bind:data="data" v-bind:columns="columns" >
      <!-- <template #header>
        <thead>
          <tr>
            <td>a</td>
            <td>qwd</td>
            <td>qsdac</td>
            <td>qdasd</td>
            <td>zxc</td>
            </tr>
        </thead>
      </template> -->
    </Table>
  </div>
</template>

<script>
import Table from './components/Table.vue'
const data = [];
for (var i = 0; i < 50000; i++) {
  data[i] = {
    title: "Task " + i,
    duration: "5 days",
    percentComplete: Math.round(Math.random() * 100),
    start: "01/01/2009",
    finish: "01/05/2009"
  };
}
const columns = {
  title: '标题',
  duration: '周期',
  percentComplete: '完成进度',
  start: '开始时间',
  finish: '结束时间'
}
export default {
  name: 'app',
  data() {
    return {
      data: data,
      columns: columns
    }
  },
  components: {
    Table
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
