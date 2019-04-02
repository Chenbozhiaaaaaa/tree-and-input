

<template>
  <el-container>
    <el-header>Header</el-header>
    <el-container>
      <el-aside width="200px">
        <el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick" default-expand-all></el-tree>
      </el-aside>
      <el-main>
        <input type="text" v-focus="data[0].children[0].focus"><br>
        <input type="text" v-focus="data[0].children[1].focus"><br>
        <input type="text" v-focus="data[0].children[2].focus"><br>
        <input type="text" v-focus="data[0].children[3].focus"><br>
        <input type="text" v-focus="data[0].children[4].focus"><br>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      data: [
        {
          label: "root [结构类型]",
          children: [
            {
              id: "0",
              label: "单行文字",
              focus:true
            },
            {
              id: "1",
              label: "单行数字",
              focus:false
            },
            {
              id: "2",
              label: "多行文字",
              focus:false
            },
            {
              id: "3",
              label: "表格类型",
              focus:false
            },
            {
              id: "4",
              label: "图片文件",
              focus:false
            },
          ]
        }
      ],
      defaultProps: {
        children: "children",
        label: "label"
      },
      labelPosition: "top",
      formLabelAlign: {
        name: "",
        region: "",
        type: ""
      }
    };
  }, 
  directives: {
    focus: {
      // 绑定判断
      inserted: function (el, {value}) {
        if (value) {
          el.focus()
        }
      },
      //更新判断	
      update: function (el, {value}) {
        if (value) {
          el.focus()
        }
      },
      //更新完成s
      componentUpdated:function(el, {value}){

      }
    }
  },
  methods: {
    updateFocusStatus(id){
      let _this = this;
      let children = _this.data[0].children;

      if(children[id].focus){
        children[id].focus=!children[id].focus;
        return;
      }

      children.map(n =>{
        n.id != id ? n.focus = false : n.focus = true;
      })
    },
    handleNodeClick(data) {
      let _this = this;
      console.log(data.id+":"+data.focus);
      _this.updateFocusStatus(data.id);
    }
  }
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
}
html,
body,
#app {
  height: 100%;
}
.el-container {
  height: 100%;
}
.el-header {
  background-color: #b3c0d1;
  color: #333;
  padding: 0;

  line-height: 60px;
}

.el-aside {
  background-color: #d3dce6;
  color: #333;
  height: 100%;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
  height: 100%;
}
</style>