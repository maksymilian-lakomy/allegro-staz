<template>
    <v-full-page-section :id="id">
        <header>
            <slot name="header" />
        </header>
        <div class="fullpage__section__about__columns">
            <div>
                <slot name="column1" />
            </div>
            <div v-if="secondColumn === true">
                <slot name="column2" />
            </div>
        </div>
    </v-full-page-section>
</template>

<script>
import FullPageSection from "./FullPageSection";
export default {
    name: "FullPageSectionTexts",
    props: {
        id: {
            type: String,
            required: true
        },
        secondColumn: {
            type: Boolean,
            required: false
        }
    },
    components: {
        "v-full-page-section": FullPageSection
    }
};
</script>

<style lang="sass" scoped>

.fullpage__section__about
    position: relative
    &__columns
        overflow: auto
        display: grid
        grid-template-columns: repeat(2, 1fr)
        column-gap: 2em
        line-height: 1.75em
        @media (max-width: 768px)
            grid-template-columns: repeat(1, 1fr)
    
</style>