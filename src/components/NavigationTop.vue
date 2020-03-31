<template>
    <div class="navigation-top">
        <a href="https://github.com/maksymilian-lakomy">GitHub</a>
        <a href="https://www.facebook.com/makslakomy">Facebook</a>
    </div>
</template>

<style lang="sass" scoped>
.navigation-top
    z-index: 999999
    position: fixed
    right: 0
    padding: 1em
    a
        margin: 0 .5em
        font-size: .75em
        font-weight: bolder
        opacity: .5
        transition: opacity .2s
        &:hover
            opacity: 1
</style>