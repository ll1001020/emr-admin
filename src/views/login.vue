<template>
		<el-card class="box-card" style="margin: auto;margin-top: 10%;">
			<el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
				<el-form-item label="电话" prop="name">
					<el-input v-model="ruleForm.name"></el-input>
				</el-form-item>

				<el-form-item label="密码" prop="desc">
						<el-input  v-model="ruleForm.desc"></el-input>
				</el-form-item>
			
				<el-form-item>
					<el-button type="primary" @click="submitForm('ruleForm')" :loading="load123">立即创建</el-button>
					<el-button @click="resetForm('ruleForm')">重置</el-button>
				</el-form-item>
			</el-form>
		</el-card>
</template>

<script>
  export default {
    data() {
      return {
        ruleForm: {
          name: '',
          region: '',
          date1: '',
          date2: '',
          delivery: false,
          type: [],
          resource: '',
          desc: '',
        },
		load123:false,
        rules: {
          name: [
            { required: true, message: '请输入电话', trigger: 'blur' },
            { min: 11, max:11, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          desc: [
            { required: true, message: '请填写密码', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
		  this.load123 = true;
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
		this.load123 = false;
			
          } else {
            console.log('error submit!!');
			this.load123 = false;
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>

<style>
	.text {
	    font-size: 14px;
	  }
	
	  .item {
	    padding: 18px 0;
	  }
	
	  .box-card {
		  padding-top: 20px;
	    width: 480px;
		height: 480px;
	  }
</style>