  <template>
  <div>
    <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>
</div>
</template>
<script>
import axios from "axios"
export default {
    data() {
      return {
        data:[],
        /* data: [{
          label: '一级 1',
          children: [{
            label: '二级 1-1',
            children: [{
              label: '三级 1-1-1'
            }]
          }]
        }, {
          label: '一级 2',
          children: [{
            label: '二级 2-1',
            children: [{
              label: '三级 2-1-1'
            }]
          }, {
            label: '二级 2-2',
            children: [{
              label: '三级 2-2-1'
            }]
          }]
        }, {
          label: '一级 3',
          children: [{
            label: '二级 3-1',
            children: [{
              label: '三级 3-1-1'
            }]
          }, {
            label: '二级 3-2',
            children: [{
              label: '三级 3-2-1'
            }]
          }]
        }], */
        defaultProps: {
          children: 'children',
          label: 'label'
        }
      };
    },
    created(){
        this.fetchData()
    },
    methods: {
      handleNodeClick(data) {
        console.log(data);
      },
      /* 1：查询数据 */
      fetchData(){
        /* this.data = [
          {
          label: '一级 1',
          children: [{
            label: '二级 1-1',
            children: [{
              label: '三级 1-1-1'
            }]
          }]
        }, 
        {
          label: '一级 2',
          children: [{
            label: '二级 2-1',
            children: [{
              label: '三级 2-1-1'
            }]
          }, {
            label: '二级 2-2',
            children: [{
              label: '三级 2-2-1'
            }]
          }]
        }, 
        {
          label: '一级 3',
          children: [{
            label: '二级 3-1',
            children: [{
              label: '三级 3-1-1'
            }]
          }, {
            label: '二级 3-2',
            children: [{
              label: '三级 3-2-1'
            }]
          }]
        }
      ] */
      const config ={
        contentType:'application/json',
      } 
        let formData = new FormData()
        formData.append('instructions', 'mkdir /')
        let path ="http://localhost:5000/mongoDB";

        axios.post(path,formData,config)
          .then((res)=>{
            let organizationList = res.data;
            let tree = organizationList;
            this.data.push(tree);
            console.log(this.data);
          })
          .catch((error)=>{
            console.error(error);
          });
        },
        
      
  }
}
</script>