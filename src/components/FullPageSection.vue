<template>
    <section class="fullpage__section" :class="{'fullpage__section--full' : full}" :id="id">
        <slot />
    </section>
</template>

<script>
export default {
    name: "FullPageSection",
    props: {
        full: {
            type: Boolean,
            default: false
        },
        id: {
            type: String,
            required: true
        }
    }
};
</script>

<style lang="sass" scoped>
.fullpage
    &__section--full
        padding: unset !important
        height: 100vh !important

    &__section
        height: calc(100vh - 2 * 5em)
        padding: 5em 20em
        position: relative
        display: flex
        flex-direction: column
        justify-content: center
        @media (max-width: 1440px)
            padding: 5em 15em
            @media (max-width: 1280px)
                padding: 5em 10em
            @media (max-width: 960px)
                padding: 5em 5em
            @media (max-width: 768px)
                padding: 5em 2.5em

        &::before, &::after
            z-index: -1
            display: block
            position: absolute
            width: 80px
            height: 80px
            content: " "
            background-image: url('../assets/corner.gif')

        &::before
            top: 1em
            left: 1em

        &::after
            bottom: 1em
            right: 1em
            transform: rotate(180deg)
</style>