<template>
    <div>
        <div v-for="(item, index) in todos" :key="index">
            <h1>{{item.title}}</h1>

        </div>
    </div>
</template>

<script>
export default {
    name: 'Todos',
    props: ["todos"]
}
</script>

<style scoped>

</style>
