<template>
  <tr>
    <td style="width:100px" v-for="(prop, key) in columns" :key="key">{{item[key]}}</td>
  </tr>
</template>
<script>
/* eslint no-console:0*/
export default {
  name: 'TableRow',
  props: {
    item : Object,
    columns : Object
  },
  methods: {

  },
  destroyed(){
    console.log(this.item.title)
  }
}
</script>
