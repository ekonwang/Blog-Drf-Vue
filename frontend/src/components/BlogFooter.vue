<template>
    <!--  br 标签给页脚留出位置  -->
    <br><br><br>
    <div id="footer">
        <p>yifou.club</p>
    </div>
</template>

<script>
    export default {
        name: 'BlogFooter'
    }
</script>

<style scoped>
    #footer {
        position: fixed;
        left: 0;
        bottom: 0;
        height: 50px;
        width: 100%;
        background: whitesmoke;
        text-align: center;
        font-weight: bold;
    }
</style>