<template>
  <body id = "poster">
  <el-container>
    <el-header>
      <el-menu
          :default-active="activeIndex2"
          class="el-menu-demo"
          mode="horizontal"
          @select="handleSelect"
          background-color="#545c64"
          text-color="#fff"
          active-text-color="#ffd04b">

        <el-menu-item class = "logo">xx文档</el-menu-item>

        <el-dropdown class = "avat">
          <el-avatar src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png" class = "el-dropdown-link">
          </el-avatar><i class="el-icon-arrow-down el-icon--right"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item @click="tochange()">修改个人信息</el-dropdown-item>
            <el-dropdown-item>注销</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </el-menu>
    </el-header>
    <el-container>
      <el-aside width="200px">
        <el-row class="tac">
          <el-col :span="24">
            <el-menu
                default-active="2"
                class="el-menu-vertical-demo"
                @open="handleOpen"
                @close="handleClose"
                background-color="#545c64"
                text-color="#fff"
                active-text-color="#ffd04b">

              <el-menu-item align="left" @click="towork()">
                <i class="el-icon-suitcase-1"></i>
                <span slot="title" >工作台</span>
              </el-menu-item>
              <el-submenu index="1" align="left">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>我的团队</span>
                </template>
                <el-menu-item>
                  <i class="el-icon-circle-plus-outline"></i>
                  <span>新建团队</span>
                </el-menu-item>
                <el-submenu index="1-1">
                  <template slot="title">

                    <span>HLZZ</span>
                  </template>
                  <el-menu-item>何宇峰</el-menu-item>
                  <el-menu-item>罗志贤</el-menu-item>
                  <el-menu-item>赵致远</el-menu-item>
                  <el-menu-item>张洋</el-menu-item>
                </el-submenu>
                <el-submenu index="1-4">
                  <template slot="title">HHH</template>
                  <el-menu-item index="1-4-1">何宇峰</el-menu-item>
                </el-submenu>
              </el-submenu>
              <el-submenu index="2" align="left">
                <template slot="title">
                  <i class="el-icon-document"></i>
                  <span>我的文档</span>
                </template>
                <el-submenu index="1-1">
                  <template slot="title">
                    <span>HLZZ</span>
                  </template>
                  <el-menu-item>小学期注意事项</el-menu-item>
                  <el-menu-item>123</el-menu-item>
                  <el-menu-item>aa</el-menu-item>
                </el-submenu>
                <el-submenu index="1-4">
                  <template slot="title">HHH</template>
                  <el-menu-item index="1-4-1">hh</el-menu-item>
                </el-submenu>
              </el-submenu>
              <el-menu-item index="3" align="left" @click="tobin()">
                <i class="el-icon-delete"></i>
                <span slot="title">回收站</span>
              </el-menu-item>
            </el-menu>
          </el-col>
        </el-row>
      </el-aside>
      <el-main>

        <div>

          <el-input style="width: 80%;  margin-right:20%"
                    placeholder="请输入文档名"
                    v-model="docname"
                    clearable>
          </el-input>

          <br> <br> <br>

          <el-card style="height: 610px;width: 80%">
            <quill-editor v-model="content" ref="myQuillEditor" style="height: 500px;" :options="editorOption">
            </quill-editor>
          </el-card>
          <br><br>
          <el-button type="success" round style="margin-left:50%" @click="save()">保存</el-button>
        </div>

      </el-main>

    </el-container>



  </el-container>
  </body>
</template>

<script>
import {
  quillEditor
} from 'vue-quill-editor'
import 'quill/dist/quill.core.css'
import 'quill/dist/quill.snow.css'
import 'quill/dist/quill.bubble.css'

export default {

  name: 'FuncFormsEdit',
  components: {
    quillEditor
  },
  data() {

    return {
      docname: this.$route.query.filename,
      content: this.$route.query.content,
      editorOption: {},
      data: [{
        label: '我的团队',
        children: [{
          label: 'HLZZ',
          children: [{
            label: '何宇峰'},
            {label: '罗志贤'},
            {label: '赵致远'},
            {label: '张洋'}
          ]
        }]
      }, {
        label: '我的文档',
        children: [{
          label: '共产党宣言',
        }, {
          label: '小学期评分细则',
        }]
      }, {
        label: '最近浏览',
        children: [{
          label: '二级 3-1',
          children: [{
            label: '三级 3-1-1'
          }]
        }, {
          label: '二级 3-2',
          children: [{
            label: '三级 3-2-1'
          }]
        }]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    };
  },
  methods: {
    save:function (){
      this.$router.push("/work")
    },
    handleNodeClick(data) {
      console.log(data);
    },
    towork:function ()
    {
      this.$router.push("/work")
    },
    tochange:function ()
    {
      this.$router.push("/changeinfo")
    }
  },
}
</script>

<style scoped>


#poster {
  background:url("../assets/blue-snow.png") repeat;
  background-position: center;
  position: fixed;
}
body{
  margin: 0px;
  padding: 0;
}

.tac{
  width: 200px;
  margin-top: 100px;
}

.logo{
  font-size: 20px;
  text-align: left;
}

.avat{
  margin-top: 10px;
}


</style>