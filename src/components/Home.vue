<template>
      <el-container class="home-container">
        <!-- 头部区域 -->
        <el-header>
          <div>
            <img src="../assets/heima.png" alt="">
            <span>电商后台管理系统</span>
          </div>
          <el-button @click="logout" type="info">退出</el-button>
        </el-header>
        <!-- 页面主题区域 -->
        <el-container>
          <!-- 侧边栏 -->
          <el-aside :width="isCollapse ? '64px' : '200px'">
            <div class="toggle-button" @click="toggleCollapse">|||</div>
            <!-- 侧边栏菜单区域 -->
              <el-menu background-color="#333744" text-color="#fff"
              active-text-color="#ffd04b" unique-opened :collapse='isCollapse'
              :collapse-transition='false' :router="true"
              :default-active="activePath">
                <!-- 一级菜单 -->
                <el-submenu :index="item.id + ''" v-for='item in menulist' :key='item.id'>
                  <!-- 一级菜单的模板区 -->
                  <template slot="title">
                    <!-- 图标 -->
                    <i :class="iconsObj[item.id]"></i>
                    <!-- 文本 -->
                    <span>{{item.authName}}</span>
                  </template>
                  <!-- 二级菜单 -->
                    <el-menu-item :index="'/' + subItem.path" v-for='subItem in item.children'
                    :key='subItem.id' @click="saveNavState('/' + subItem.path)">
                        <template slot="title">
                          <!-- 图标 -->
                          <i class="el-icon-menu"></i>
                          <!-- 文本 -->
                          <span>{{subItem.authName}}</span>
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
          <el-main>
            <router-view/>
          </el-main>
        </el-container>
      </el-container>
</template>

<script>
import { Container, Header, Aside, Main, Menu, Submenu, MenuItem } from 'element-ui'
export default {
  components: {
    'el-container': Container,
    'el-header': Header,
    'el-aside': Aside,
    'el-main': Main,
    'el-menu': Menu,
    'el-submenu': Submenu,
    // 'el-menu-item-group': MenuItemGroup,
    'el-menu-item': MenuItem
  },
  data () {
    return {
      // 左侧菜单数据
      menulist: [],
      // 左侧菜单图标
      iconsObj: {
        125: 'el-icon-user-solid',
        103: 'el-icon-s-help',
        101: 'el-icon-s-goods',
        102: 'el-icon-s-order',
        145: 'el-icon-s-marketing'
      },
      // 是否折叠
      isCollapse: false,
      // 被激活的链接地址
      activePath: ''
    }
  },
  created () {
    this.getMenuList()
    this.activePath = window.sessionStorage.getItem('activePath')
  },
  methods: {
    logout () {
      window.sessionStorage.clear()
      this.$router.push('/login')
    },
    // 获取所有的菜单
    async getMenuList () {
      const { data: res } = await this.$http.get('menus')
      if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
      this.menulist = res.data
      console.log(res)
    },
    // 点击按钮切换菜单的折叠
    toggleCollapse () {
      this.isCollapse = !this.isCollapse
    },
    // 保存链接的激活状态
    saveNavState (activePath) {
      window.sessionStorage.setItem('activePath', activePath)
      this.activePath = activePath
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
  .el-menu {
    border-right: 0;
  }

}

.el-main {
  background-color:#eaedf1;
  // background-color: yellow;
}

.toggle-button {
  background-color: #4A5064;
  font-size: 10px;
  line-height: 24px;
  color: #fff;
  text-align: center;
  letter-spacing: 0.3em;
  cursor: pointer;
}
</style>
