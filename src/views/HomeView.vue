<template>
  <el-container style="min-height: 100vh">
      <el-aside :width="sideWidth+'px'" style="background-color: rgb(238, 241, 246);">
        <el-menu :default-openeds="['1', '3']" style="min-height: 100%;overflow-x:hidden;"
                 background-color="rgb(48,65,86)"
                 text-color="#fff"
                 active-text-color="#ffe528"
                 :collapse-transition="false"
                 :collapse="isCollapse"
                 class="el-menu-vertical-demo"
        >
          <div style="height: 60px;line-height: 60px;text-align: center;color: aliceblue;">
            <img src="../assets/logo.png" style="width: 20px;position: relative;top: 5px" >
            <b v-show="logoTextShow">后台管理系统</b>
          </div>
          <el-submenu index="1">
            <template slot="title"><i class="el-icon-message"></i>
            <span slot="title"> 导航一</span></template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="1-1">选项1</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <template slot="title">选项2</template>
              <el-menu-item index="1-4-1">选项2-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title"><i class="el-icon-menu"></i>
              <span slot="title"> 导航二</span>
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="2-1">选项1</el-menu-item>
              <el-menu-item index="2-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="2-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="2-4">
              <template slot="title">选项4</template>
              <el-menu-item index="2-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title"><i class="el-icon-setting"></i>
              <span slot="title"> 导航三</span>
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="3-1">选项1</el-menu-item>
              <el-menu-item index="3-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="3-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="3-4">
              <template slot="title">选项4</template>
              <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>

      <el-container>

        <el-header style=" font-size: 12px;border-bottom: 1px solid #ccc;line-height: 60px;display: flex">
          <div style="flex:1;font-size: 18px">
            <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
          </div>
          <el-dropdown style="width: 70px;cursor: pointer">
            <span>张译文</span><i class="el-icon-arrow-down" style="margin-left: 5px"></i>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人信息</el-dropdown-item>
              <el-dropdown-item>退出</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>

        </el-header>

        <el-main>
          <el-breadcrumb separator="/">
            <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item><a href="/">用户管理</a></el-breadcrumb-item>
          </el-breadcrumb>
          <div style="margin: 10px 0">
            <el-input style="width: 200px"  placeholder="请输入名称" suffix-icon="el-icon-search"></el-input>
            <el-input style="width: 200px;margin-left: 5px"  placeholder="请输入邮箱" suffix-icon="el-icon-message"></el-input>
            <el-input style="width: 200px;margin-left: 5px"  placeholder="请输入地址" suffix-icon="el-icon-position"></el-input>
            <el-button style="margin-left: 5px" type="primary">搜索</el-button>
          </div>
          <div style="margin: 10px 0">
            <el-button type="primary">新增<i style="margin-left: 3px" class="el-icon-circle-plus-outline"></i> </el-button>
            <el-button type="danger">批量删除<i style="margin-left: 3px" class="el-icon-remove-outline"></i> </el-button>
            <el-button type="primary">导入<i style="margin-left: 3px" class="el-icon-download"></i> </el-button>
            <el-button type="primary">导出<i style="margin-left: 3px" class="el-icon-upload2"></i> </el-button>
          </div>
          <el-table :data="tableData" border stripe >
            <el-table-column prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
            <el-table-column label="操作">
              <el-button type="success">编辑<i style="margin-left: 3px" class="el-icon-edit"></i></el-button>
              <el-button type="danger">删除<i style="margin-left: 3px" class="el-icon-remove-outline"></i></el-button>
            </el-table-column>
          </el-table>
          <div style="padding: 10px 0">
            <el-pagination
                @size-change="handleSizeChange"
                @current-change="handleCurrentChange"
                :current-page="currentPage4"
                :page-sizes="[5,10,15,20]"
                :page-size="10"
                layout="total, sizes, prev, pager, next, jumper"
                :total="400">
            </el-pagination>
          </div>
        </el-main>
      </el-container>
    </el-container>
</template>

<script>


export default {
  name: 'HomeView',
  data() {
    const item = {
      date: '2020-05-02',
      name: '张译文',
      address: '浙江省嘉兴市海盐县'
    };
    return {
      tableData: Array(10).fill(item),
      collapseBtnClass: 'el-icon-s-fold',
      isCollapse:false,
      sideWidth:200,
      logoTextShow:true
    }
  },
  methods:{
    collapse(){//点击收缩按钮触
        this.isCollapse=!this.isCollapse
        if(this.isCollapse){
          this.sideWidth=64
          this.collapseBtnClass='el-icon-s-unfold'
          this.logoTextShow=false
        }else{
          this.sideWidth=200
          this.collapseBtnClass='el-icon-s-fold'
          this.logoTextShow=true
        }


    }
  }
}
</script>

