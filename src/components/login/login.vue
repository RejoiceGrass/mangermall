<template>
  <div class="login-wrap">
    <el-form
     class="login-form"
     :label-position="labelPosition"
     label-width="80px"
     :model="formData">
     <h2>用户登录</h2>
      <el-form-item label="用户名">
        <el-input v-model="formData.userName"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input
        v-model="formData.passWord"></el-input>
      </el-form-item>
      <el-button @click.prevent = "handleLogin()"  class="login-btn" type="primary">登录</el-button>
    </el-form>
  </div>
</template>
<script>
export default{
  data() {
      return {
        labelPosition: 'top',
        formData: {
          userName: '',
          passWord: ''
        }
      };
    },
    methods: {
      handleLogin(){
        this.$http.post('login',this.formData) .then((res)=>{
          const {
            data,
            meta:{msg,stats}
           } = res.data

            if(status === 200){
              //登录成功
              //1.跳转home
              this.$router.push({name:'home'})
                //2.  提示成功
                this.$message.success(msg)
            }
            else{
              this.$message.waring(msg)
            }


           /* //=>
            const {meta:{msg,status}} =
            {meta:{msg:"11",status:200}}
            //=>
            obj = {msg:"11",status:200}
            //=>
            {msg,status} = {msg:"11",status:200}
            */

        })
      }
    }
}
</script>
<style>
  .login-wrap{
  height: 100%;
  background-color: #324152;
  display: flex;
  justify-content: center;
  align-items: center;
  }
  .login-wrap .login-form{
    width: 400px;
    background-color: aliceblue;
    border-radius: 5px;
    padding:30px;
  }
  .login-wrap .login-btn{
    width: 100%;
  }
</style>
