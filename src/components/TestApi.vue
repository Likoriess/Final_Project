<template>
    <div class="container">
        <div class="title">
            Commands:
        </div>

        <div v-if="isLoad" class="loading">
        <b>Loading data..</b>
        </div>

        <div v-else class="data">
            <div v-for="(el, i) in teamData" :key="el.id">
                {{ i + 1 }}.{{ el.abbrevation }}{{ el.city }}
                <img src="../assets/dele.png" alt="del" title="Delete"
                style="width: 18px;
                height: 18px;"
                @click="removeTeam(el.id)"/>
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        name: 'TestApi',
        data() {
            return{
                teamData:[],
                isLoad: true
            }
        },
        methods:{
            removeTeam(id) {
                this.teamData = this.teamData.filter((el) => el.id !==id )
            }
        },
        mounted() {
            const url = "https://free-nba.p.rapidapi.com/teams?page=0";
            const options = {
                method: "GET",
                headers: {
                    "X-RapidAPI-Key": "488f437511msh2d3854838388c55p13692cjsn135921cfebdf",
                    "X-RapidAPI-Host": "free-nba.p.rapidapi.com",
                },
            };
            fetch(url, options)
                .then((res) => res.json())
                .then((res) =>{
                    this.teamData = res.data
                    this.isLoad = false
                })
    }}
</script>


<style scoped>
.container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background-image: url('../assets/AllBack.jpg');
}

.title {
    font-size: 34px;
    color: #8a2be2;
    margin-top: 1%;
    margin-bottom: 0%;
    font-weight: bold;
    border: 3px solid black;
    background-color: #FF6347;
    width: 200px;
    height: 40px;
    text-align: center;
}

.data{
    padding: 20px;
    font-size: 22px;
    background: linear-gradient(45deg, #FFB300 33%, #FFB300  66%, #EDFF21);
    background-clip: text;
    -webkit-text-fill-color: transparent;
}

.loading{
    padding-bottom: 37%;
    padding-top: 10px;
    font-size: 30px;
    background: linear-gradient(45deg, #FFB300 33%, #FFB300 66%, #EDFF21);
    background-clip: text;
    -webkit-text-fill-color: transparent;
}

img{
    cursor: pointer;
    margin-left: 15px;
}
</style>