<template lang="pug">
nav
    router-link(:to="{name: 'root'}") Home
    | &nbsp;|&nbsp;
    router-link(:to="{name: 'about'}") About
router-view
</template>

<script>
export default {
    // eslint-disable-next-line
    name: 'Base',
}
</script>
