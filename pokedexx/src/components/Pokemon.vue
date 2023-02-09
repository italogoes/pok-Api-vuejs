<script>
    export default {
        props: {
            num: Number,
            name: String,
            url: String
        }
    }
</script>

<template>
    <div>
        <h1>{{ num }} {{ name }}</h1>
        <small>{{ url }}</small>
    </div>
</template>
