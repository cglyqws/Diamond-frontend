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

        <el-menu-item class = "logo">Diamond文档</el-menu-item>

        <el-dropdown class = "avat">
          <el-avatar src="https://cube.elemecdn.com/0/88/03b0d39583f48206768a7534e55bcpng.png" class = "el-dropdown-link">
          </el-avatar><i class="el-icon-arrow-down el-icon--right"></i>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>修改个人信息</el-dropdown-item>
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

              <el-menu-item align="left">
                <i class="el-icon-suitcase-1"></i>
                <span slot="title">工作台</span>
              </el-menu-item>
              <el-submenu index="1" align="left">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>我的团队</span>
                </template>
                <el-menu-item>
                  <i class="el-icon-circle-plus-outline"></i>
<!--                  <el-button size="mini" @click="dialogFormVisible=true">新建团队</el-button>-->
                  <span @click="dialogFormVisible=true">新建团队</span>
                  <el-dialog title="新建团队" :visible.sync="dialogFormVisible" style="width: 1200px" center="true">
                    <el-form :model="dynamicValidateForm" ref="dynamicValidateForm" label-width="100px" class="demo-dynamic" size="small" style="width: 500px">
                      <el-form-item
                              prop=""
                              label="团队名称"
                              :rules="[{ required: true, message: '请输入团队名称', trigger: 'blur' },]">
<!--       { type: 'email', message: '请输入正确的邮箱地址', trigger: ['blur', 'change'] }-->


                        <el-input v-model="dynamicValidateForm.email"></el-input>
                      </el-form-item>
                      <el-form-item
                              v-for="(domain, index) in dynamicValidateForm.domains"
                              :label="'成员' + index "
                              :key="domain.key"
                              :prop="'domains.' + index + '.value'"
                              :rules="{
      required: true, message: '成员不能为空', trigger: 'blur'
    }"
                      >
                        <el-input v-model="domain.value"></el-input>
                          <el-button plain icon="el-icon-delete" circle style="width: 45px;height: 45px" @click.prevent="removeDomain(domain)"></el-button>
<!--                          <el-button @click.prevent="removeDomain(domain)" style="height: 30px;width: 100px">删除</el-button>-->
                      </el-form-item>
                      <el-form-item>
                        <el-button type="primary" @click="submitForm('dynamicValidateForm')" style="height: 40px;width: 130px">提交</el-button>
                        <el-button @click="addDomain" style="height: 40px;width: 130px">添加成员</el-button>
                        <el-button @click="resetForm('dynamicValidateForm')" style="height: 40px;width: 130px">重置</el-button>
                      </el-form-item>
                    </el-form>
                  </el-dialog>
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
                <span slot="title" >回收站</span>
              </el-menu-item>
            </el-menu>
          </el-col>
        </el-row>
      </el-aside>

      <el-main>
<!--        <el-button round class="but1">新建文档</el-button><br><br>-->
<!--        <el-button round>模板库</el-button><br><br>-->
<!--        <el-button round>导入</el-button>-->

        <el-button round class="but1" @click="showrecent()">最近使用</el-button>
        <el-divider direction="vertical"></el-divider>
        <el-button round class="but1" @click="showmycreate()">我创建的</el-button>
        <el-divider direction="vertical"></el-divider>
        <el-button round class="but1">我的收藏</el-button>

          <div class = dtemp>
                    <el-button  class="but1" @click="tocreatedoc()">新建文档</el-button><br><br>
                    <el-button >模板库</el-button><br><br>
                    <el-button >导入</el-button>
          </div>


      </el-main>
    </el-container>



  </el-container>
</body>
</template>

<script>
import Head from "@/components/Header";
export default {
  components: {Head},
  data() {
    return {
      dynamicValidateForm: {
        domains: [{
          value: ''
        }],
        email: ''
      },
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
      },
      dialogFormVisible: false,
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      formLabelWidth: '120px'
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('submit!');
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    removeDomain(item) {
      var index = this.dynamicValidateForm.domains.indexOf(item)
      if (index !== -1) {
        this.dynamicValidateForm.domains.splice(index, 1)
      }
    },
    addDomain() {
      this.dynamicValidateForm.domains.push({
        value: '',
        key: Date.now()
      });
    },
    handleNodeClick(data) {
      console.log(data);
    },
    showrecent:function () {
      this.$router.push("/work/recent")
    },
    showmycreate:function () {
      this.$router.push("/work/mycreate")
    },
    showmyfav:function ()
    {
      this.$router.push("/work/favorites")
    },
    tocreatedoc:function ()
    {
      this.$router.push("/work/createdoc")
    },
    towork:function ()
    {
      this.$router.push("/work")
    },
    tochange:function ()
    {
      this.$router.push("/changeinfo")
    },
    tobin:function ()
    {
      this.$router.push("/work/bin")
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

.el-button{
  font-size: x-large;
  width: 170px;
  font-weight: bold;
}

.but1{
  font-size: x-large;
  background-color: #333333;
  font-weight: bold;
  color: #dcdfe6;
}

.el-main{
  margin-top: 20px;
  margin-left: 0;
  text-align: left;
}

.eld{
  height: 0;
}

.dtemp{
  margin-left: 80%;
}
</style>