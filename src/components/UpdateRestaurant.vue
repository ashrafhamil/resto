<template>
    <MainHeader></MainHeader>
    <h1>Hello User, Welcome on Update Restaurant Page</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter name" v-model="restaurant.name">
        <input type="text" name="address" placeholder="Enter address" v-model="restaurant.address">
        <input type="text" name="contact" placeholder="Enter contact" v-model="restaurant.contact">
        <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    </form>
</template>
<script>
import MainHeader from './MainHeader.vue'
import axios from 'axios';
export default {
    name:'UpdateRestaurant',
    components:{
        MainHeader
    },
    data()
    {
        return{
            restaurant : {
                name:'',
                address:'',
                contact:'',
            }
        }
    },
    methods:{
        async updateRestaurant()
        {
            
            const result = await axios.put("http://localhost:3000/restaurants/"+this.$route.params.id,{
                name:this.restaurant.name,
                address:this.restaurant.address,
                contact:this.restaurant.contact,
            });
            console.log(result)
            if(result.status==200)
            {
                this.$router.push({name:"HomePage"})
            }
        }
    },
    async mounted()
    {
        let user= localStorage.getItem('user-info');
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }

        const result = await axios.get('http://localhost:3000/restaurants/'+this.$route.params.id)
        // console.warn(this.$route.params.id)
        console.warn(result)
        this.restaurant=result.data
    }
    
}
</script>