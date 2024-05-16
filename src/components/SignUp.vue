<template>
    <img class="logo" src="../assets/restoimage.jpg" alt="">
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name">
        <input v-model="email" type="email" placeholder="Enter Email">
        <input v-model="password" type="password" placeholder="Enter Password">
        <button v-on:click="signUp">Sign Up</button>
        <p>
            <router-link to="/login">Login</router-link>
        </p>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    name : 'SignUp',
    data()
    {
        return {
            name:'',
            email:'',
            password:'',
        }
    },
    methods:{
        async signUp()
        {
            let result = await axios.post("http://localhost:3000/users",{
                email:this.email,
                password:this.password,
                name:this.name
            });

            console.warn(result);
            if(result.status==201)
            {
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:"HomePage"});
                //json-server --watch db.json
            }
        }
    },
    mounted()
    {
        let user= localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name:'HomePage'})
        }
    }
}
</script>

<style>

</style>