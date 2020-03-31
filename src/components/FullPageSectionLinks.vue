<template>
    <v-full-page-section :id="id">
        <header>
            <slot name="header" />
        </header>
        <div class="fullpage__section__links">
            <a class="fullpage__section__links__link" href="https://github.com/maksymilian-lakomy">
                <img src="@/assets/github-icon.gif" />
                GitHub
            </a>
            <a
                class="fullpage__section__links__link"
                href="https://www.instagram.com/maksymilianlakomy/"
            >
                <img src="@/assets/instagram-icon.gif" />
                Instagram
            </a>
            <a class="fullpage__section__links__link" href="https://www.facebook.com/makslakomy">
                <img src="@/assets/facebook-icon.gif" />
                Facebook
            </a>
            <a class="fullpage__section__links__link" href="https://twitter.com/makslakomy">
                <img src="@/assets/twitter-icon.gif" />
                Twitter
            </a>
            <a
                class="fullpage__section__links__link"
                href="https://open.spotify.com/playlist/4Uw3qlyPuGd4xrXCPhSxL6"
            >
                <img src="@/assets/spotify-icon.gif" />
                Spotify
            </a>
        </div>
    </v-full-page-section>
</template>

<script>
import FullPageSection from "./FullPageSection";
export default {
    name: "FullPageSectionLinks",
    props: {
        id: {
            type: String,
            required: true
        }
    },
    components: {
        "v-full-page-section": FullPageSection
    }
};
</script>

<style lang="sass" scoped>

.fullpage__section__links
    position: relative
    width: fit-content
    display: flex
    justify-content: space-between
    margin: 0 auto

    @media (max-width: 1280px)
        flex-direction: column

    &__link
        margin: .5em
        display: flex
        align-items: center
        opacity: .5
        transition-duration: .2s
        &:hover
            opacity: 1
        img
            height: 4em
            width: 4em
            margin-right: 1em
</style>