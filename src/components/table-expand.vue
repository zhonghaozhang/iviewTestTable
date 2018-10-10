
<template>
  <Table :columns="col" border :show-header="false" :data="data" :click2="click2"></Table>
</template>
<script>
  import expand from './table-expand.vue'
  export default {
    components: { expand },
    props: {
      data:Array,
      click2:Function,
    },
    data(){
      return {
        col:[
          {
            align:'center',
            title:'序号',
            type:'index',
            width:60,
          },

          {
            align:'center',
            type: 'expand',
            width: 30,
            render: (h, params) => {
              console.log(params)
              return h(expand, {
                props: {
                  data:params.row.data,
                  click2:this.click2,
                }
              })
            }
          },
          {
            align:'center',
            title: 'Name',
            key: 'name'
          },
          {
            align:'center',
            title: 'Age',
            key: 'age'
          },
          {
            align:'center',
            title: 'Address',
            key: 'address'
          },
          {
            title: '操作',
            key: 'action',
            width: 150,
            align: 'center',
            render: (h, params) => {
              return h('div', [
                h('Button', {
                  props: {
                    type: 'primary',
                    size: 'small'
                  },
                  style: {
                    marginRight: '5px'
                  },
                  on: {
                    click: () => {
                      console.log(this)
                      this.click2()
                    }
                  }
                }, 'View'),
                h('Button', {
                  props: {
                    type: 'error',
                    size: 'small'
                  },
                  on: {
                    click: () => {
                      this.data.splice(params.index,1)
                    }
                  }
                }, 'Delete')
              ]);
            }
          }
        ]
      }
    },
    created(){

    }
  };
</script>


<style scoped>
  .expand-row{
    margin-bottom: 16px;
  }
</style>
