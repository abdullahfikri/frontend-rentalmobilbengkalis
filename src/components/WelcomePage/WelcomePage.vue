<template>
    <NavbarPage />
    <HeroPage />
    <SectionAbout />
    <SectionArmada /> <FooterPage />
</template>

<script>
import NavbarPage from "./NavbarPage.vue";
import HeroPage from "./HeroPage.vue";
import SectionAbout from "./SectionAbout.vue";
import SectionArmada from "./SectionArmada.vue";
import FooterPage from "./FooterPage.vue";
export default {
    name: "WelcomePage",
    components: {
        NavbarPage,
        HeroPage,
        SectionAbout,
        SectionArmada,
        FooterPage,
    },
};
</script>
