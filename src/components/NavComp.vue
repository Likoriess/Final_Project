<template>
<div class="container">
    <nav>
        <RouterLink to="/"><b>Home page</b></RouterLink>
        <RouterLink to="/chat"><b>Chat</b></RouterLink>
        <RouterLink to="/test"><b>NBA</b></RouterLink>
    </nav>
</div>
<div style="border-bottom: solid 3px #a70de4;"></div>
</template>

<script>
    export default {
        name: 'NavComp'
    }
</script>

<style scoped>
.container{
        background-color: #1C1C1C;
        display: flex;
        justify-content: center;
    }

nav {
    width: 400px;
    height: 41px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 30px;
    font-size: 21px;
    text-transform: uppercase;
    background: linear-gradient(45deg, #FF1493 33%, #9400D3 66%, #8A2BE2);
    background-clip: text;
    -webkit-text-fill-color: transparent;
    color: #8A2BE2;
}
</style>