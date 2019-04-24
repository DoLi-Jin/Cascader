<template>
  <div class="home">
    <el-select
        v-model="selectArrData"
        multiple
        collapse-tags
        @remove-tag="selectTagChange"
        style="margin-left: 20px;"
        filterable
        placeholder="请选择"> 
        <el-option :value="selectArrData" >
            <el-tree
              :data="treeArrData"
              show-checkbox
              :check-strictly=false
              default-expand-all
              highlight-current
              check-on-click-node   
              node-key="id"
              ref="tree"
              highlight-current
              :props="defaultProps"
              @check-change="treeArrChooseData">
            </el-tree>
        </el-option>
    </el-select>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'home',
  	data(){
       return {

       	treeArrData: [{
	         id: 1,
	         label: '一级 1',
	         children: [{
	           id: 4,
	           label: '二级 14',
	           children: [{
	             id: 9,
	             label: '三级 19'
	           }, {
	             id: 10,
	             label: '三级 10'
	           }]
	         }]
	       }, {
	         id: 2,
	         label: '一级 2',
	         children: [{
	           id: 5,
	           label: '二级 25'
	         }, {
	           id: 6,
	           label: '二级 26'
	         }]
	       }, {
	         id: 3,
	         label: '一级 3',
	         children: [{
	           id: 7,
	           label: '二级 37'
	         }, {
	           id: 8,
	           label: '二级 38'
	         }]
	       }],
	       defaultProps: {
	         children: 'children',
	         label: 'label'
	       },
	       //下拉框中的数组
	       selectArrData: [],
	       //树状图中被选中的id:label的对象
	       treeChooseObj:{},
       }
  	},
  	methods:{
  	  //树状图被点击的时候
      treeArrChooseData(){
      	this.treeChooseObj={}
      	this.selectArrData=[];
      	let oldArr=this.$refs.tree.getCheckedNodes()
      	oldArr.map((value,index,arr)=>{

      		// 如果输入框中只需要最后的子节点，那么将此处注释的的代码解开
      		if(!value.children){
      			this.treeChooseObj[value.id]=value.label
      			this.selectArrData.push(value.label)
      		}

      	  })
      },
      //下拉框中的小标签删除事件
      selectTagChange(val){
        let newArr=[]
        for(let i in this.treeChooseObj){
            if(this.treeChooseObj[i]==val){
                delete this.treeChooseObj[i]
            }else{
                newArr.push(i)
            }
	        this.$refs.tree.setCheckedKeys(newArr)
	    };
  	  },
  	}
}
</script>
<style>
/*树状图高度撑起来,树状图鼠标移入背景颜色变成白色*/
.el-select-dropdown__item, .el-select-dropdown__item{height:100%;}
.el-select-dropdown__item.hover, .el-select-dropdown__item:hover{background:#fff;}
</style>
