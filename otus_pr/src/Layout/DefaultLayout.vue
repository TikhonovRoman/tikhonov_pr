<template>
    <header>
        <slot name="header"></slot>
    </header>
    <nav>
        <slot name="navigation"></slot>
    </nav>
    <main>
        <slot name="default"></slot>
    </main>
    <footer>
        <slot name="footer"></slot>
    </footer>

</template>
<style scoped>
nav {
    margin-bottom: 10vh;
}
</style>