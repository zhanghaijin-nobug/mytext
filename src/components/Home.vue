<template>
      <el-container class="home-container">
        <!-- 头部区域 -->
        <el-header>
          <div>
            <img src="../assets/header.png" alt="">
            <span>电商后台管理系统</span>
          </div>
          <el-button @click="logout" type="info">退出</el-button>
        </el-header>
        <!-- 页面主题区域 -->
        <el-container>
          <!-- 侧边栏 -->
          <el-aside width="200px">
            <!-- 侧边栏菜单区域 -->
              <el-menu background-color="#333744" text-color="#fff" active-text-color="#ffd04b">
                <!-- 一级菜单 -->
                <el-submenu index="1">
                  <!-- 一级菜单的模板区 -->
                  <template slot="title">
                    <!-- 图标 -->
                    <i class="el-icon-location"></i>
                    <!-- 文本 -->
                    <span>导航一</span>
                  </template>
                  <!-- 二级菜单 -->
                    <el-menu-item index="1-1">
                        <template slot="title">
                          <!-- 图标 -->
                          <i class="el-icon-location"></i>
                          <!-- 文本 -->
                          <span>导航一</span>
                        </template>
                    </el-menu-item>
                  <!-- <el-submenu index="1-4">
                    <template slot="title">选项4</template>
                    <el-menu-item index="1-4-1">选项1</el-menu-item>
                  </el-submenu> -->
                </el-submenu>
              </el-menu>
          </el-aside>
          <!-- 右侧内容主体 -->
          <el-main></el-main>
        </el-container>
      </el-container>
</template>

<script>
import { Container, Header, Aside, Menu, Submenu, MenuItem } from 'element-ui'
export default {
  components: {
    'el-container': Container,
    'el-header': Header,
    'el-aside': Aside,
    'el-menu': Menu,
    'el-submenu': Submenu,
    // 'el-menu-item-group': MenuItemGroup,
    'el-menu-item': MenuItem
  },
  methods: {
    logout () {
    //   window.sessionStorage.clear()
      this.$router.push('/login')
    }
  }
}
</script>

<style lang="less" scoped>
.home-container {
  height: 100%;
  // background-color: yellow;
}

.el-header {
  background-color: #373d41;
  // background-color: #019aff;
  display: flex;
  justify-content: space-between;
  padding-left: 0;
  align-items: center;
  color: #fff;
  > div {
    display: flex;
    align-items: center;
    span {
      margin-left: 15px;
    }
  }
}

.el-aside {
  background-color: #333744;
  // background-color: rgb(242, 0, 0);
}

.el-main {
  background-color:#eaedf1;
  // background-color: yellow;
}
</style>
