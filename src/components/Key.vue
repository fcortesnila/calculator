<template>
    <div >
        <h3 class="calc-key"> {{ valor }} </h3>
    </div>
</template>

<script>
export default {
    props: ['valor', 'numb', 'funct']
}
</script>

<style>
.calc-key{
    text-align: center;
    cursor: pointer;
    border-radius: 50px;
    background-color: #aaa;
}

</style>