<template>
    <div class="message">
        <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    props: {
        message:{
            type: String,
            required: true,
        }
    }
}
</script>
<style lang="scss" scoped>
p{
    color: red;
}

.message{
    text-align: center;
    padding-top: 20px;
    padding-bottom: 20px;
}
</style>