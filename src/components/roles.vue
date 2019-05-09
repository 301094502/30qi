<template>
  <div class="user-container">
    <!-- 面包屑 -->
    <el-breadcrumb class="my-breadcrumb" separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>权限管理</el-breadcrumb-item>
      <el-breadcrumb-item>角色列表</el-breadcrumb-item>
    </el-breadcrumb>
    <!-- 栅格 输入框 和按钮 -->
    <el-row>
      <el-col :span="24">
        <!-- 按钮 -->
        <el-button type="danger" @click="addVisible=true" plain>添加角色</el-button>
      </el-col>
    </el-row>
    <!-- table -->
    <el-table :data="tableData" style="width: 100%" border>
      <el-table-column type="index" width="50"></el-table-column>
      <el-table-column prop="roleName" label="角色名称" width="180"></el-table-column>
      <el-table-column prop="roleDesc" label="角色描述" width="180"></el-table-column>
      <el-table-column label="操作">
        <template slot-scope="niubi">
          <!-- 
              template中必须设置 slot-scope="scope"
          scope.$index 索引  scope.row 这一行的数据-->
          <el-button
            type="primary"
            icon="el-icon-edit"
            @click="handleEdit(niubi.$index, niubi.row)"
            plain
            size="mini"
          ></el-button>
          <el-button
            type="danger"
            icon="el-icon-delete"
            @click="handleDelete(niubi.$index, niubi.row)"
            plain
            size="mini"
          ></el-button>
          <!-- 角色 -->
          <el-button
            type="success"
            icon="el-icon-check"
            plain
            size="mini"
            @click="handleRole(niubi.row)"
          ></el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-dialog title="添加角色" :visible.sync="addVisible">
      <el-form :model="addForm" :rules="addRules" ref="addForm">
        <el-form-item label="用户名称" label-width="120px" prop="roleName">
          <el-input v-model="addForm.userName" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="角色描述" label-width="120px" >
       
          <el-input v-model="addForm.roleDesc" autocomplete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="addVisible = false">取 消</el-button>
        <el-button type="primary" @click="submitForm('addForm')">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "roles",
  // 数据
  data() {
    return {
      // 表格依赖于数据没有数据  会一行都没有
      tableData: [
        {
          date: "2016-05-02",
          name: "王小黑",
          address: "上海市普陀区金沙江路 1518 弄"
        },
        {
          date: "2016-05-04",
          name: "王小白",
          address: "上海市普陀区金沙江路 1517 弄"
        },
        {
          date: "2016-05-01",
          name: "王小绿",
          address: "上海市普陀区金沙江路 1519 弄"
        },
        {
          date: "2016-05-03",
          name: "王小花",
          address: "上海市普陀区金沙江路 1516 弄"
        }
      ]
    };
  },
  //生命周期钩子
  created() {
    this.$request.getRoles().then(res => {
      let data = res.data.data;
      data.forEach(v => {
        v._children = v._children;
        delete v._children;
      });
      this.tableData = data;
    });
  },
  methods: {
    hangleEdit(index, row) {},
    hangleDelete(index, row) {},
    hangleRole(row) {},
    //获取角色的方法
    
  }
};
</script>

<style  lang='scss'>
.my-breadcrumb {
  height: 45px;
  line-height: 45px;
  background-color: #d3dce6;
  padding-left: 10px;
}
</style>
