<template>

    <div class="HomeP">
        <div v-if="isAunthenticated">
            <div class="HomeText">Welcome, <b>{{ username }}</b>, to our website here you will find the functionality of the website and useful information</div>
            <button @click="logout" id="out">Logout</button>
        </div>

        <div v-else>
            <label class="gradient-text">Enter your name</label>
            <input v-model="username" @keyup.enter="login"/>
            <br/>
            <button @click="login">Sign up</button>
        </div>
    </div>

</template>


<script>
    export default {
        name: 'HomePage',
        data(){
        return{
            isAunthenticated: false,
            username: ''
        }
    },
        methods: {
            login() {
                if(this.username !== ''){
                    console.log('You entered as', this.username)
                    this.isAunthenticated = true
                    localStorage.setItem('isAunthenticated', true)
                    localStorage.setItem('username', this.username)
                    this.$router.push({
                        name: 'Chat',
                        query: {username: this.username}
                    })
                }else{
                        console.log('Please, enter your name')
                    }
                },
                logout(){
                    this.isAunthenticated = false
                    this.username = ''
                    localStorage.removeItem('isAunthenticated')
                    localStorage.removeItem('username')
            }
        },
        created() {
            if(localStorage.getItem('isAunthenticated')) {
                this.isAunthenticated = true
                this.username =localStorage.getItem('username')
            }
        }
    }
</script>



<style scoped>
input {
    -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
     border-radius: 20px;
     border: 1px solid #FF1493;
     background: linear-gradient(45deg, #FF1493 33%, #9400D3 66%, #8A2BE2);
     background-clip: text;
     -webkit-text-fill-color: transparent;
     color: #8A2BE2;
     width: 250px;
     height: 30px;
     padding-left: 10px;
     background-color:  #293133;
     font-size: 20px;
}

button{
    -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
     border-radius: 20px;
     border: 1px solid #FF1493;
     color: black;
     width: 250px;
     height: 40px;
     padding-left: 10px;
     background-color: white;
     margin-top: 10px;
     color: black;
     font-size: 23px;
}
.gradient-text {
  font-family: 'Rubik One', sans-serif;
  font-size: 40px;
  text-transform: uppercase;
  background: linear-gradient(45deg, #FF1493 33%, #9400D3 66%, #8A2BE2);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  color: #8A2BE2;
  display: table;
  margin: 0 auto;
  padding-top: 70px;
  text-align: center;
}

.HomeP {
    background-image: url('../assets/AllBack.jpg');
    text-align: center;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    height: 100vh;
    width: 100%;
    margin: 0;
    padding: 0;
}

.HomeText {
  font-size: 40px;
  color: black;
  text-align: center;
  display: table;
  padding-top: 15px;
  margin: 0 auto;
  padding: 12px;
}
#out {
    background-color: #293133;
    color: #FF1493;
}
</style>