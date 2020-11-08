<template>
    <section>
        <div class="location">{{ location }}</div>
        <div class="description">{{ descriptionText }}</div>
    </section>
</template>

<script>
export default {
    name: 'Weather',

    props: {
        location: {
            type: String,
            required: true
        },
        descriptionText: {
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>
section {
    display: flex;
    flex-direction: column;
}

.description {
    text-transform: lowercase;
    font-weight: bold;
}

.description:first-letter {
    text-transform: uppercase;
}

</style>
