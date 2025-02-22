<template>
			<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
				
				<el-form-item label="电话" prop="phone">
					<el-input v-model="ruleForm.phone"></el-input>
				</el-form-item>

				<el-form-item label="密码" prop="password">
						<el-input  v-model="ruleForm.password"></el-input>
				</el-form-item>
				
				<el-form-item >
				    <el-radio-group v-model="ruleForm.resource">
				      <el-radio type="docotor" label="doctor"></el-radio>
				      <el-radio type="patient" label="patient"></el-radio>
				    </el-radio-group>
				</el-form-item>
			
				<el-form-item>
					<el-button type="primary" @click="submitForm('ruleForm')" :loading="load123">立即登录</el-button>
					<el-button @click="resetForm('ruleForm')">重置</el-button>
				</el-form-item>
			</el-form>
</template>

<script>
  export default {
    data() {
      return {
        ruleForm: {
          phone: '',
          password: '',
		  resource: ''
        },
		load123:false,
        rules: {
          phone: [
            { required: true, message: '填写电话号码', trigger: 'blur' },
            { min: 11, max:11, message: '长度为 11 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请填写密码', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(ruleForm) {
        this.$refs.ruleForm.validate((valid) => {
			console.log('表单验证结果:', valid);
			console.log(this.ruleForm);
          if (valid) {
			let _this = this;
			if(_this.ruleForm.resource == 'doctor'){
				axios.get('http://localhost:8081/doctor/login',{params:_this.ruleForm}).then(function(resp){
					console.log(resp)
				})
				if(resp.data.code == 0){
					alert('登录成功')
				}else{
					alert('登录失败')
				}

			}else if(_this.ruleForm.resource == 'patient'){
				axios.get('http://localhost:8081/patient/login',{params:_this.ruleForm}).then(function(resp){
					console.log(resp)
				})
			}
			
          } else {
			
			console.log('error submit!!');
            return false;
			
          }
        });
      },
      resetForm(ruleForm) {
        this.$refs[ruleForm].resetFields();
      }
    }
  }
</script>

<style>
	.text {
	    font-size: 14px;
	  }
	  .demo-ruleForm{
		padding: 0px;
	  }
	  
</style>