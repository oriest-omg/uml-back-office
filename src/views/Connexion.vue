<template>
<body>
    <div>
        <div id="login">
            <h3 class="text-center text-white pt-5">Login form</h3>
            <div class="container">
                <div id="login-row" class="row justify-content-center align-items-center">
                    <div id="login-column" class="col-md-6">
                        <div id="login-box" class="col-md-12">
                                <h3 class="text-center text-info">Login</h3>
                                <div class="form-group">
                                    <label for="username" class="text-info">Username:</label><br>
                                    <input type="text" name="username" id="username" class="form-control" v-model="username">
                                </div>
                                <div class="form-group">
                                    <label for="password" class="text-info">Password:</label><br>
                                    <input type="text" name="password" id="password" class="form-control" v-model="password">
                                </div>
                                <div class="form-group">
                                    <label for="remember-me" class="text-info"><span>Remember me</span> <span><input id="remember-me" name="remember-me" type="checkbox"></span></label><br>
                                    <button @click="goToDash()" type="button"> Submit</button>
                                </div>
                                <div id="register-link" class="text-right">
                                    <a href="#"  class="text-info">Register here</a>
                                </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>        
    </div>
</body>
</template>
<script>

import axios from 'axios';
export default {
  name: 'Connexion',
    data() {
        return {
                username :'',
                password :'',
                admins : []
        }
    },
    methods : {
            async getDatas (){
                console.log(axios.get("http://localhost:8000/api/admins"));
                await axios
                .get("http://localhost:8000/api/admins")
                .then(response=> {
                    console.log(response);
                    for (const admin of response.data){
                        this.admins.push(admin)
                    }
                console.log(this.admins);
            });
            },
            goToDash() {
                console.log('appuyer');
                this.admins.forEach(admin => {
                    if(admin.email == this.username && admin.password == this.password)
                    {
                        console.log('succ');
                        this.$router.push('/DashBoard');
                    }else
                    {
                        console.log("error");
                    }
                });
            }
        },
    async mounted() {
        await this.getDatas();
        console.log('ok')
    },
}
</script>
<style scoped>
body {
  margin: 0;
  padding: 0;
  background-color: #17a2b8;
  height: 100vh;
}
#login .container #login-row #login-column #login-box {
  margin-top: 120px;
  max-width: 600px;
  height: 320px;
  border: 1px solid #9C9C9C;
  background-color: #EAEAEA;
}
#login .container #login-row #login-column #login-box #login-form {
  padding: 20px;
}
#login .container #login-row #login-column #login-box #login-form #register-link {
  margin-top: -85px;
}
    
</style>