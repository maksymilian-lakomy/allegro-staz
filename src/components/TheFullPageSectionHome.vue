<template>
    <v-full-page-section :id="id" :full="true">
        <div class="fullpage__section__home">
            <img src="@/assets/home-waving.gif" />
        </div>
    </v-full-page-section>
</template>

<script>
import FullPageSection from "./FullPageSection";
export default {
    name: "TheFullPageSectionHome",
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
.fullpage__section__home
    position: relative
    text-align: center
    z-index: -1
    margin: auto
    overflow: hidden
    img
        max-width: 100%
        max-height: 100%
        z-index: -2
        text-align: center
</style>