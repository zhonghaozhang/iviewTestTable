<template>
  <Table :columns="columns10" border :data="data9" ></Table>

</template>

<script>
  import expandRow from './table-expand.vue';

export default {
  components: { expandRow },
  name: 'HelloWorld',
  data () {
    return {
      isShow:false,
      loading:false,
      delIndex:0,
      columns10: [
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
            return h(expandRow, {
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
          key: 'address',
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
                    this.click2()
                  }
                }
              }, '新增'),
              h('Button', {
                props: {
                  type: 'error',
                  size: 'small'
                },
                on: {
                  click: () => {
//                    this.isShow=true
                    this.$Modal.confirm({
                      title:'确认删除吗？',
                      content:'删除子集也会被一并删除，请小心操作!',
                      closable:true,
                      onOk:()=>{
                        this.data9.splice(params.index,1)
                        this.$Message.success('确认删除成功！');
                      },
                      onCancel:()=>{
                        this.$Modal.remove()
                      }
                    })

                  }
                }
              }, '删除')
            ]);
          }
        }
      ],
      data9: [
        {
          name: 'John Brown',
          age: 18,
          address: 'New York No. 1 Lake Park',
          job: 'Data engineer',
          interest: 'badminton',
          birthday: '1991-05-14',
          book: 'Steve Jobs',
          movie: 'The Prestige',
          music: 'I Cry',
          data:[{
            name:'aaa',
            age:'33',
            address:'aaaaaaaa',
            data:[{
              name:'vv',
              age:'22',
              address:'bbbb',
              data:[{
                name:'vv',
                age:'22',
                address:'bbbb',
              }]
            }]
          }]
        },
        {
          name: 'Jim Green',
          age: 25,
          address: 'London No. 1 Lake Park',
          job: 'Data Scientist',
          interest: 'volleyball',
          birthday: '1989-03-18',
          book: 'My Struggle',
          movie: 'Roman Holiday',
          music: 'My Heart Will Go On',
          data:[{
            name:'aaa',
            age:'33',
            address:'aaaaaaaa',
          }]
        },
        {
          name: 'Joe Black',
          age: 30,
          address: 'Sydney No. 1 Lake Park',
          job: 'Data Product Manager',
          interest: 'tennis',
          birthday: '1992-01-31',
          book: 'Win',
          movie: 'Jobs',
          music: 'Don’t Cry',
          data:[{
            name:'aaa',
            age:'33',
            address:'aaaaaaaa',
          }]
        },
        {
          name: 'Jon Snow',
          age: 26,
          address: 'Ottawa No. 2 Lake Park',
          job: 'Data Analyst',
          interest: 'snooker',
          birthday: '1988-7-25',
          book: 'A Dream in Red Mansions',
          movie: 'A Chinese Ghost Story',
          music: 'actor',
          data:[{
            name:'aaa',
            age:'33',
            address:'aaaaaaaa',
          }]
        }
      ]
    }


  },
  methods:{
    click2(){
      console.log(333);
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
