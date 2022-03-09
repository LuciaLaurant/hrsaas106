<template>
  <div class="dashboard-container">
    <div class="app-container">
      <el-card class="tree-card">
        <!-- 用了一个行列布局 -->
        <tree-tools :tree-node="company" :is-root="true" @addDepts="addDepts" />
        <el-tree :data="departs" :props="defaultProps" :default-expand-all="true">
          <!-- 传入内容 插槽内容 会循环多次 有多少节点 就循环多少次 -->
          <!-- 作用域插槽 slot-scope="obj" 接收传递给插槽的数据   data 每个节点的数据对象-->
          <tree-tools
            slot-scope="{ data }"
            :tree-node="data"
            @delDepts="getDepartments"
            @addDepts="addDepts"
          />
        </el-tree>
      </el-card>
    </div>
    <!-- 放置新增弹层组件  -->
    <add-dept :show-dialog="showDialog" :tree-node="node" />
  </div>
</template>

<script>
/* eslint-disable */ 
import TreeTools from './components/tree-tools.vue'
import AddDept from './components/add-dept' // 引入新增部门组件
import { getDepartments } from '@/api/departments'
import { tranListToTreeData } from '@/utils/index.js'
export default {
  components: {
    // eslint-disable-next-line vue/no-unused-components
    TreeTools,
    AddDept
  },
  created() {
    this.getDepartments() // 调用自身的方法
  },
  data() {
    return {
      company: {},
      departs: [],
      defaultProps: {
        label: 'name' // 表示 从这个属性显示内容
      },
      showDialog: false, // 显示窗体
      node:null //记录当前节点
    }
  },
  methods:{
    async getDepartments() {
      const result = await getDepartments()
      this.company = { name: result.companyName, manager: '负责人' ,id: ''}
      this.departs = tranListToTreeData(result.depts, '') // 需要将其转化成树形结构
      console.log(result)
    },
    // 监听显示弹层
    addDepts(node){
      this.showDialog = true // 显示弹层
      // 因为node是当前的点击的部门， 此时这个部门应该记录下来,
      this.node = node
    }
  }
}
</script>

<style scoped>
.tree-card {
  padding: 30px  140px;
  font-size:14px;
}
</style>
