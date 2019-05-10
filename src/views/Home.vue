<template>
  <div class="home">
<!--    下拉框，必须是多选和标签化-->
    <el-select v-model="selectValue" placeholder="请选择"
               collapse-tags  multiple @remove-tag="selTagChange">
      <el-option :value="selectValue">
<!--        树状图，必须有ref属性和node-key属性-->
        <el-tree
                :data="treeData"
                show-checkbox
                default-expand-all
                node-key="id"
                ref="tree"
                @check-change="treeOnChange"
                highlight-current
                :props="defaultProps">
        </el-tree>

      </el-option>
    </el-select>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  data(){
    return{
      // 树状图list
      treeData: [
        {
          id: 1,
          label: '一级 1',
          children: [
            {
              id: 4,
              label: '二级 1-1',
              children: [
                {
                  id: 9,
                  label: '三级 1-1-1'
                },
                {
                  id: 10,
                  label: '三级 1-1-2'
                }
              ]
            }
          ]
        },
        {
          id: 2,
          label: '一级 2',
          children: [
            {
              id: 5,
              label: '二级 2-1'
            },
            {
              id: 6,
              label: '二级 2-2'
            }
          ]
        },
        {
          id: 3,
          label: '一级 3',
          children: [
            {
              id: 7,
              label: '二级 3-1'
            },
            {
              id: 8,
              label: '二级 3-2'
            }
          ]
        }
      ],
      // 树状图的配置
      defaultProps: {
        children: 'children',
        label: 'label',
        value:"id"
      },
      // 下拉框中的list绑定值（Array)
      selectValue:[]
    }
  },
  methods:{
    //树状图被选择时候调用函数（data:当前的被点击元素的对象，checked：是否被选中）
    treeOnChange(data, checked){
      // 过滤了非最下级子元素
      if(!data.children){
        // 此条被选中触发事件
        if(checked){
          this.selectValue.push(data.label)
        }
        // 被取消触发事件
        else{
          this.selectValue.map((value,index)=>{
            if(value==data.label){
              this.selectValue.splice(index,1)
            }
          })
        }
      }
    },
    // 下拉框中的tag标签被取消时候触发事件（val：被×标签label）
    selTagChange(val){
      // 设置树状图被选中的数组
      this.$refs.tree.setCheckedKeys(
        // 树状图去掉下拉框中被×掉的标签节点
        (this.$refs.tree.getCheckedNodes()).map((value,index)=>{
          if(!value.children){
            if(value.label!=val){
              return value.id
            }
          }
        })
      );
    }
  },
}
</script>
<style>
  /*很重要的两条css样式属性，请重视，最好列为行内样式*/
  .el-select-dropdown__item{
    height:100%;
    background:#fff;
    padding:0;
  }
  .el-select-dropdown__item.hover,.el-select-dropdown__item:hover{
    height:100%;
    background:#fff;
    padding:0;
  }
</style>