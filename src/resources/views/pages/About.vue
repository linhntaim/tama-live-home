<template lang="pug">
h1 About
</template>

<script>
import {app} from '@/bootstrap/app'

export default {
    // eslint-disable-next-line
    name: 'About',
    data() {
        return {
            world: 'World',
            locale: this.$i18n.locale,
            locales: this.$config.localization.locale.supported,
        }
    },
    watch: {
        locale() {
            this.$setLocale(this.locale)
        },
    },
    beforeRouteEnter() { // cannot access `this`
        app.$log.debug('page', 'about.beforeRouteEnter')
    },
    beforeRouteUpdate() {
        this.$log.debug('page', 'about.beforeRouteUpdate')
    },
    beforeRouteLeave() {
        this.$log.debug('page', 'about.beforeRouteLeave')
    },
    beforeCreate() {
        this.$log.debug('page', 'about.beforeCreate')
    },
    created() {
        this.$log.debug('page', 'about.created')
    },
    beforeUpdate() {
        this.$log.debug('page', 'about.beforeUpdate')
    },
    updated() {
        this.$log.debug('page', 'about.updated')
    },
    beforeMount() {
        this.$log.debug('page', 'about.beforeMount//rendering')
    },
    mounted() {
        this.$log.debug('page', 'about.mounted//rendered')
    },
    beforeUnmount() {
        this.$log.debug('page', 'about.beforeUnmount')
    },
    unmounted() {
        this.$log.debug('page', 'about.unmounted')
    },
}
</script>
