<template>
	<div>
		<!-- <label for="name">账号</label><br>
		<input type="text" id="name" v-model="username"><br>
		<label for="passwd">密码</label><br>
		<input type="password" id="passwd" v-model="userpasswd"><br>
		<button @click="login">提交</button><br> -->
		<label for="tid">id</label><br>
		<input type="text" id="tid" v-model="tid"><br>
		<label for="ZDMC">ZDMC</label><br>
		<input type="text" id="ZDMC" v-model="ZDMC"><br>
		<label for="ZDBM">ZDBM</label><br>
		<input type="text" id="ZDBM" v-model="ZDBM"><br>
		<label for="ZDFBM">ZDFBM</label><br>
		<input type="text" id="ZDFBM" v-model="ZDFBM"><br>
		<label for="JB">JB</label><br>
		<input type="text" id="JB" v-model="JB"><br>
		<button @click="sub">提交</button>
		<br>
		<button @click="getinfo">ddddd</button>
		<v-form>
			<v-form-item label="账户">
				<v-input placeholder="请输入账户名" v-model="username"></v-input>
			</v-form-item>
			<v-form-item label="密码">
				<v-input placeholder="请输入密码" v-model="userpasswd"></v-input>
			</v-form-item>
			<v-form-item>
		        <v-button type="primary" html-type="submit" @click="login">登录</v-button>
		    </v-form-item>
		</v-form>
	</div>
</template>
<script>
import axios from 'axios'
import qs from 'qs'
import store from '../store'
export default {
	name:'Main',
    data(){
    	return{
    		username:'',
    		userpasswd:'',
    		token: store.fetch(),
    		tid:'',
    		ZDMC:'',
    		ZDBM:'',
    		ZDFBM:'',
    		JB:''
    	}
    },
    methods:{
    	login(){
    		this.axios.post("http://172.66.66.201:2015/api/Login",
    			this.$qs.stringify({'user_name': this.username, 'password': this.userpasswd})
    		).then((res)=>{
	  			var token = JSON.parse(res.data).token
	  			this.token = token
	  			console.log(token)
	  		})
    	},
    	sub(){
    		var k = this.token
    		console.log(k)
    		this.axios.post('http://172.66.66.201:2015/SJZDSava',
    			this.$qs.stringify({
					ZDMC: this.ZDMC,
					ZDBM: this.ZDBM,
					ZDFBM: this.ZDFBM,
			    }),
			    {
			        headers: {
			            "access-key":k,
			            "Content-Type": "application/x-www-form-urlencoded"
			        }
			    }
    		).then((res)=>{
    			console.log(res)
    		})
    	},
    	getinfo(){
    		var k = this.token
    		console.log(k)
    		this.axios.get('http://172.66.66.201:2015/SJZDList',{
    			headers:{"access-key":k},
    			params:{
    				pageSize:12,
    				pageNum:1
    			}
    		}).then((res)=>{
    			console.log(res)
    		})
    	}
    },
	watch: {
		token: {
			handler: function(val, oldVal) {
			store.save(val);
		},
			deep: true
		}
	}
}

</script>
<style>
input{
	border:1px solid #ccc;
}
</style>