<template>
    <div
        class="fullpage"
        :style="{'transform': `translateY(${offsetY})`, 'transition-duration': '.75s'}"
        ref="sections"
    >
        <v-full-page-section-home id="home" />
        <v-full-page-section-texts id="about" :secondColumn="!smallWindow">
            <template v-slot:header>Header 1</template>
            <template v-slot:column1>{{aboutTexts[0]}}</template>
            <template v-slot:column2>{{aboutTexts[1]}}</template>
        </v-full-page-section-texts>
        <v-full-page-section-texts id="about2" v-show="smallWindow === true">
            <template v-slot:header>Header 2 ...</template>
            <template v-slot:column1>{{aboutTexts[1]}}</template>
        </v-full-page-section-texts>
        <v-full-page-section-links id="links" />
    </div>
</template>

<script>
import TheFullPageSectionHome from "./TheFullPageSectionHome";
import FullPageSectionTexts from "./FullPageSectionTexts";
import FullPageSectionLinks from "./FullPageSectionLinks";

export default {
    name: "FullPage",
    data() {
        return {
            inMove: false,
            sections: 0,
            touchStartY: 0,
            windowWidth: undefined,
            smallWindow: false,
            navigation: []
        };
    },
    props: {
        activeSection: {
            type: Number,
            required: true,
            default: 0
        }
    },
    components: {
        "v-full-page-section-home": TheFullPageSectionHome,
        "v-full-page-section-texts": FullPageSectionTexts,
        "v-full-page-section-links": FullPageSectionLinks
    },
    computed: {
        offsetY() {
            return (this.activeSection / this.sections) * -100 + "%";
        },
        aboutTexts() {
            const leftColumn = `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec vehicula, erat ac mattis dignissim, tellus justo fringilla quam, et ultrices felis sapien cursus dolor. Phasellus mattis eros non pellentesque ornare. Vestibulum volutpat nec lacus quis dignissim. Pellentesque mollis eget turpis in dapibus.`;
            const rightColumn = `Morbi mi felis, fringilla ut risus eu, pellentesque scelerisque augue. Aliquam sit amet pretium sem. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Pellentesque magna neque, scelerisque quis nisl non, fringilla pellentesque mauris.`;
            return [leftColumn, rightColumn];
        }
    },
    watch: {
        smallWindow() {
            this.$emit("smallWindow", this.smallWindow);
        },
        navigation() {
            console.log('test');
            this.$emit("navigation", this.navigation);
        }
    },
    created() {
        this.resize();
        window.addEventListener("resize", this.resize);
        window.addEventListener("resize", this.countSections);
        window.addEventListener("mousewheel", this.handleMouseWheel, {
            passive: false
        });
        window.addEventListener("touchstart", this.touchStart, {
            passive: false
        });
        window.addEventListener("touchmove", this.touchMove, {
            passive: false
        });
        window.addEventListener("touchend", this.touchEnd, {
            passive: false
        });
        window.addEventListener("keydown", this.keyDown);
    },
    mounted() {
        this.countSections();
    },
    destroyed() {
        window.removeEventListener("resize", this.resize);
        window.removeEventListener("resize", this.countSections);
        window.removeEventListener("mousewheel", this.handleMouseWheel, {
            passive: false
        });
        window.removeEventListener("touchstart", this.touchStart, {
            passive: false
        });
        window.removeEventListener("touchmove", this.touchMove, {
            passive: false
        });
        window.removeEventListener("touchend", this.touchEnd, {
            passive: false
        });
        window.removeEventListener("keydown", this.keyDown);
    },
    methods: {
        resize() {
            this.windowWidth = window.innerWidth;
            this.smallWindow = this.windowWidth <= 768;
        },
        countSections() {
            let sections = this.$refs.sections.getElementsByTagName("section");
            const navigation = [];
            sections.forEach(section => {
                if (section.style.display !== "none")
                    navigation.push(section.id);
            });
            this.navigation = navigation;
            if (this.activeSection >= navigation.length)
                this.scrollToSection(navigation.length - 1, true);
            this.sections = navigation.length;
        },
        handleMouseWheel(event) {
            if (event.wheelDelta < 30 && !this.inMove) this.move(1);
            else if (event.wheelDelta > 30 && !this.inMove) this.move(-1);
            event.preventDefault();
            return;
        },
        touchStart(event) {
            this.touchStartY = event.touches[0].clientY;
            return;
        },
        touchMove(event) {
            if (this.inMove) return;
            event.preventDefault();
            const currentY = event.touches[0].clientY;
            if (this.touchStartY < currentY) this.move(-1);
            if (this.touchStartY > currentY) this.move(1);
            return;
        },
        touchEnd() {
            this.touchStartY = 0;
        },
        keyDown(event) {
            if (event.keyCode === 38) this.move(-1);
            else if (event.keyCode === 40) this.move(1);
        },
        move(direction) {
            const newIndex = this.activeSection + direction;
            this.scrollToSection(newIndex, true);
        },
        scrollToSection(index, force = false) {
            if ((this.inMove && !force) || index < 0 || index >= this.sections)
                return;
            this.$emit("update:activeSection", index);
            this.inMove = true;
            setTimeout(() => {
                this.inMove = false;
            }, 750);
        }
    }
};
</script>

<style lang="sass" scoped>
.fullpage
</style>