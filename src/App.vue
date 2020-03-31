<template>
    <div class="app">
        <transition name="fade">
            <v-navigation-top v-show="navigation[activeSection] !== 'links'" />
        </transition>
        <v-navigation
            :activeSection.sync="activeSection"
            :navigation="navigation"
            @scroll="activeSection = $event"
        />
        <v-full-page
            :activeSection.sync="activeSection"
            @smallWindow="smallWindow = $event"
            @navigation="navigation = $event"
        ></v-full-page>
    </div>
</template>

<script>
import FullPage from "@/components/FullPage";
import Navigation from "@/components/Navigation";
import NavigationTop from "@/components/NavigationTop";

export default {
    name: "App",
    data() {
        return {
            activeSection: 0,
            smallWindow: false,
            navigation: []
        };
    },
    components: {
        "v-full-page": FullPage,
        "v-navigation": Navigation,
        "v-navigation-top": NavigationTop
    }
};
</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css?family=Roboto+Mono&display=swap')

a
    color: inherit
    text-decoration: unset

body
    margin: 0
    overflow: hidden
    font-family: 'Roboto Mono', monospace

.fade-enter-active, .fade-leave-active
    transition-duration: .25s
    transform: translateY(0%)

.fade-enter, .fade-leave-to
    transform: translateY(-100%)

.app
    width: 100%
    height: 100vh
    overflow: hidden
    position: relative
    @media (max-height: 640px)
        font-size: .8em
</style>
