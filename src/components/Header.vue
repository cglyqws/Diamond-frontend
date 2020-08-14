<template>
  <div>
    <el-menu
        :default-active="activeIndex2"
        class="el-menu-demo"
        mode="horizontal"
        @select="handleSelect"
        background-color="#545c64"
        text-color="#fff"
        active-text-color="#ffd04b">

      <el-menu-item class = "logo">Diamond文档</el-menu-item>

      <el-dropdown :hide-on-click="false">
                      <span class="el-dropdown-link">
                        <el-avatar :size="50" :src="user.avatar" size="mini" ></el-avatar>
                      </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item>{{user.username}}</el-dropdown-item>
          <el-dropdown-item><a href="../changeinfo"> 修改信息</a></el-dropdown-item>
          <el-dropdown-item divided>注销</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>

    </el-menu>

  </div>
</template>

<script>
export default {
  name: "head"
}
</script>

<style scoped>
.logo{
  font-size: 20px;
  text-align: left;
}

.avat{
  margin-top: 10px;
}

</style>