<template>
    <nav class="navigation">
        <ol class="navigation__list">
            <li class="navigation__list__element" v-for="(path, i) in navigation" :key="i">
                <a
                    class="navigation__list__element__link"
                    :class="{'navigation__list__element__link--active': i === activeSection}"
                    @click="$emit('update:activeSection', i)"
                ></a>
            </li>
        </ol>
    </nav>
</template>

<script>
export default {
    name: "Navigation",
    props: {
        navigation: {
            type: Array,
            required: true
        },
        activeSection: {
            type: Number,
            required: true
        }
    }
};
</script>

<style lang="sass" scoped>
.navigation
    z-index: 999999
    position: fixed
    text-align: right
    top: 50%
    transform: translateY(-50%)
    right: 0
    &__list
        margin: 0
        padding: 0
        margin-right: 2em
        @media (max-width: 768px)
            margin-right: 1em
        &__element
            cursor: pointer
            list-style: none
            margin: .5em 0
            &__link
                display: block
                border-radius: 50%
                height: .5em
                width: .5em
                border: 2px solid black
                list-style: none
                transition-duration: .2s

            &__link--active
                background-color: black
</style>