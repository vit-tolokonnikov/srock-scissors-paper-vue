<template>
    <header class="container">
        <h1>{{ title }}</h1>
    </header>
</template>

<script>
export default {
    name: 'TheHeader',
    props: {
        title: String,
        required: Boolean(true)
    }
}
</script>

<style scoped>

</style>