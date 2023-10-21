<template>
    <div v-if="username" class="allChat">
        <div class="chat">
            <h2>Chat</h2>
            <div class="text" v-for="message in messages" :key="message.id">
            {{ message.username }}: {{ message.text }}
        </div>

        <div v-show="emptyMsg" class="empty">
        No messages :(
        </div>
        </div>

        <input v-model="newMessage" placeholder="Text your message"/>
        <button @click="sendMessage" @keyup.enter="sendMessage" class="send">Send</button>
        <br/>
        <button v-show="deleteBtn" @click="delMessage" class="del">Delete</button>
    </div>

    <div v-else class="alert">
        To use the chat you need to <router-link :to="{name: 'Home'}"><div class="a" title="Click on me">register</div></router-link>
    </div>

</template>


<script>
    export default {
        name: 'ChatPage',
        data() {
            return {
                messages: [],
                newMessage: '',
                emptyMsg: true,
                deleteBtn: false,
                username: localStorage.getItem('username')
            }
        },
        computed(){
            localStorage.setItem('username', this.$route.query.username)
        },
        methods: {
            sendMessage(){
                if(!this.username){
                    this.username = 'Anonim'
                }
                if(this.newMessage!== '') {
                    this.emptyMsg = false
                    console.log('You entered message', this.newMessage)
                    this.messages.push({
                        id:new Date().getTime(),
                        text: this.newMessage,
                        username: this.username
                    })
                    this.saveChatRecords()
                    this.newMessage = ''
                    this.deleteBtn = true
                }else{
                    console.log('Please enter message')
                    alert('Please enter message')
                }
            },
            delMessage(){
                this.messages = []
                localStorage.removeItem(`messages_${this.username}`, JSON.stringify(this.message))
                console.log('Mesaages deleted')
                this.emptyMsg = true
            },
            saveChatRecords(){
                const records = this.messages
                console.log(records)
                localStorage.setItem(`messages_${this.username}`, JSON.stringify(records))
            },
            loadChatRecords() {
                const records = JSON.parse(localStorage.getItem(`messages_${this.username}`))
                if(records) {
                    this.messages = records
                    this.emptyMsg = false
                }
            }
        },
        created(){
            this.loadChatRecords()
        }
        
    }
</script>


<style scoped>
h2 {
    text-transform: uppercase;
    background: linear-gradient(45deg, #FF1493 33%, #9400D3 66%, #8A2BE2);
    background-clip: text;
    -webkit-text-fill-color: transparent;
    color: #8A2BE2;
    margin-left: 39%;
}

.text {
     -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
     border-radius: 20px; 
     color: #FF6347; 
     border: 1px solid #FF1493;
     width: 250px;
     height: 40px;
     padding-left: 11px;
     background-color: #DCDCDC;
     font-size: 20px;
     margin-bottom: 10px; 
     margin-left: 15%;
     display: flex;
     text-align: center;
}

.chat {
     -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
     border-radius: 20px; 
     border: 1px solid #FF1493;
     color: linear-gradient(45deg, #FF1493 33%, #8A2BE2 66%, #8A2BE2);
     width: 355px;
     height: 530px;
     padding-left: 10px;
     background-color: antiquewhite;
     position: relative;
     margin-left: 40%;
}

.empty{
    margin-bottom: 30px;
    font-style: italic;
    text-transform: uppercase;
    background: linear-gradient(45deg, #B3446C, 33%, #9400D3 66%, #230D21);
    background-clip: text;
    -webkit-text-fill-color: transparent;
    color: #8A2BE2;
    margin-left: 30%;
    font-size: 20px;
}

input{
    -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
     border-radius: 20px;
     border: 1px solid #FF1493;
     width: 240px;
     height: 38px;
     padding-left: 10px;
     background-color:  #293133;
      color: #FF1493; 
     margin-left: 36%;
     margin-top: 13px;
     font-size: 20px;
     margin-right: 10px;
}

button{
    -webkit-border-radius: 20px;
    -moz-border-radius: 20px;
     border-radius: 20px;
     border: 1px solid #FF1493;
     color: #FF1493;
     width: 250px;
     height: 40px;
     padding-left: 10px;
     background-color: white;
     margin-top: 10px;
    background-color: #293133;
    font-size: 20px;
}
.alert{
    padding: 30px;
    background-image: url('../assets/AllBack.jpg');
    width: 100%;
    height: 100vh;
    font-size: 29px;
    text-align: center;
}
.allChat{
    background-image: url('../assets/AllBack.jpg');
    width: 100%;
    height: 100vh;
}

.del {
    margin-left: 44%;
}
.a{
    color: #FF6347;
    position: relative;
    cursor: pointer;

}
</style>
