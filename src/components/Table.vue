<template>
<div ref="table" class="table-wrapper">
  <table class="table" :style="bodyStyle">
    <slot name="header">
      <thead>
        <tr>
          <th style="width:100px" v-for="(value, key) in columns" :key="key">
            {{ value }}
            </th>
        </tr>
      </thead>
    </slot>
    <tbody ref="tbody">
      <tr :style="{ top:headerHeight + item._index * 24+'px'}" v-for="item in showData" :key="item.id">
        <td style="width:100px" v-for="(prop, key) in columns" :key="key">{{item[key]}}</td>
      </tr>
    </tbody>
    <slot name="footer">
    </slot>
  </table>
  </div>
</template>
<script>
/* eslint no-console:0 */
export default {
  name: 'Table',
  props: {
    data: Array,
    columns: Object
  },
  data(){
    return {
      scrollTop: 0,
      start: 0,
      length: 50,
      showLength: 20,
      bodyStyle: '',
      tight: 0,
      headerHeight: 30
    }
  },
  methods: {
    scrollChange(){
      this.scrollTop = this.$refs.table.scrollTop
      let { start, length, showLength, scrollTop } = this
      if (scrollTop + showLength * 24 > (start+length) * 24 || scrollTop < (start+showLength / 2) * 24) {
        const height = Math.floor((scrollTop - showLength *24) / 24 ) 
        this.start = height > 0 ? height : 0
      }
    },
  },
  mounted: function () {
    this.$nextTick(function () {
      this.$refs.table.addEventListener('scroll', this.scrollChange, false)
      this.bodyStyle = "height:"+this.data.length * 24 + 'px;';
    })
  },
  computed: {
    showData: function() {
      let {start, length } = this
      return this.data ? this.data.slice(start, start + length).map(function(item, index){
        return {
          _index: start+index, 
          ...item
        }
      }) : [];
    }
  }
}
</script>
<style scoped>
.table-wrapper{
  width:1000px;
  height: 500px;
  overflow: scroll;
  position: relative;
  border: 1px solid #777;
}
.table{
  display: block;
  position: absolute;
}
.table tbody tr{
  position: absolute;
  height: 24px;
}
tbody{
  width:100%;
}
</style>
