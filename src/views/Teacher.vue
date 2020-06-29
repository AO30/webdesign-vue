<template>
  <el-container>
    <el-header>
      <div style="margin:10px">
        <span>{{ name }}老师,欢迎</span>
      </div>

      <el-button type="info" plain @click="logout" class="logoutBtn">
        退出
      </el-button>
    </el-header>
    <el-container>
      <el-aside width="200px">
        <el-menu
          default-active="2"
          class="el-menu-vertical-demo"
          @open="handleOpen"
          @close="handleClose"
          background-color="#ffff99"
          text-color="#ffd04b"
          active-text-color="#ff8c00"
        >
          <router-link to="/course">
            <el-menu-item index="1">
              <i class="el-icon-s-order"></i>
              课程
            </el-menu-item>
          </router-link>

          <router-link to="/direction">
            <el-menu-item index="2">
              <i class="el-icon-s-promotion"></i>
              <span slot="title">方向</span>
            </el-menu-item>
          </router-link>
          <router-link to="/selectStudent">
            <el-menu-item index="3">
              <i class="el-icon-success"></i>
              选择学生
            </el-menu-item>
          </router-link>
          <router-link to="/addStudent">
            <el-menu-item index="4">
              <i class="el-icon-circle-plus"></i>
              添加学生
            </el-menu-item>
          </router-link>
          <router-link to="/setting">
            <el-menu-item index="5">
              <i class="el-icon-s-tools" width="20"></i>
              <span slot="title" width="20">设置</span>
            </el-menu-item>
          </router-link>
        </el-menu>
      </el-aside>
      <el-main><router-view></router-view></el-main>
    </el-container>
  </el-container>
</template>
<script>
import { mapState } from "vuex";
export default {
  data() {
    return {
      name: ""
    };
  },
  methods: {
    logout() {
      window.sessionStorage.clear();
      this.$router.push("/login");
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    },
    select() {
      let res = this.$http.get("/teacher/selectRoot");
      if (res != null) {
        this.$message.success("开启成功");
        this.$router.push("/addStudent");
      }
    }
  },
  computed: {},
  created: function() {
    this.name = window.sessionStorage.getItem("name");
  }
};
</script>
<style scope>
.el-header {
  color: #333;
  text-align: center;
  line-height: 60px;
  display: flex;
  justify-content: space-between;
  background-color: #99cc00;
  border-radius: 3px;
}
.logoutBtn {
  margin: 13px;
}
.el-aside {
  background-color: #ffff99;
  color: #333;
  text-align: center;
  line-height: 200px;
}

.el-main {
  background-color: #f0e6bc;
  color: #333;
  text-align: center;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container {
  height: 100%;
}
a {
  text-decoration: none;
}
</style>
