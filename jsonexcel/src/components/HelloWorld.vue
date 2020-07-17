
<template>
  <div>
    <Table :data="data" :columns="columns"></Table>
    
    <Button long type="success" style="margin-top:10px;" @click="onexcel2">XLSX</Button>
  
    <Button long type="success" style="margin-top:10px;" @click="onexcel">Export2Excel</Button>
  
  </div>
</template>

<script>
import excel from'../excle/excel'
export default {
  data () {
    return {
      data:[
        {
          list1:'A1',
          list2:'b2',
          list3:'c3',
        },
        {
          list1:'A1',
          list2:'b2',
          list3:'c3',
        },
        {
          list1:'A1',
          list2:'b2',
          list3:'c3',
        },
        {
          list1:'A1',
          list2:'b2',
          list3:'c3',
        },
      ],
      columns:[
        {
          title:'列表1',
          key:'list1'
        },
        {
          title:'列表2',
          key:'list2'
        },
        {
          title:'列表3',
          key:'list3'
        },
      ]
    }
  },
  methods:{
    onexcel2(){
      /**
       * Iview-admin里学来的写法
       *  这个无需引用那两个Js文件
       */
      if (this.data.length) {
          const params = {
          title:['列表1', '列表2', '列表3'],
          key:[ 'list1', 'list2', 'list3'],
          data: this.data,
          autoWidth: true,
          filename: '列表'
          }
          excel.export_array_to_excel(params)
      } else {
          this.$Message.info('表格数据不能为空！')
      }
    },
    onexcel(){
      /**
       * 网上说的最多的一种写法
       */
      const { export_json_to_excel } = require('../excle/Export2Excel');  // 将生成excel的Export2Excel.js引入

      let title = ['列表1', '列表2', '列表3'];  // 这里是excel表格的表头
      let key = [ 'list1', 'list2', 'list3']; // 设置生成列的数据属性
      function formatJson(filterVal, jsonData) {
        return jsonData.map(v => filterVal.map(j => v[j]))
      }

      export_json_to_excel( title, formatJson( key, this.data), '列表数据') //
    }
  }
}
</script>
