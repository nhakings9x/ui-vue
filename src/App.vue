<template>
    <div>
        <the-sidebar></the-sidebar>
        <the-header></the-header>
        <the-content></the-content>
    </div>
</template>
<script>
import TheContent from "./components/layout/TheContent.vue";
import TheHeader from "./components/layout/TheHeader.vue";
import TheSidebar from "./components/layout/TheSidebar.vue";
export default {
    components: {
        TheSidebar,
        TheHeader,
        TheContent,
    },
};
</script>
<style>
* {
    font-family: notosans;
    font-size: 13px;
    margin: 0;
    padding: 0;
}
:root {
    --width-sidebar: 200px;
}

body {
    background-color: #f3f4f8;
}

@font-face {
    font-family: notosans;
    src: url(./assets/fonts/notosans-regular.2cb88a13.woff2);
}

.m-flex {
    display: flex;
}

.m-row {
    width: 100%;
}
.m-w-300 {
    width: 300px;
}
.mr-8 {
    margin-right: 8px;
}
.dis-none {
    display: none;
}
.dis-block {
    display: block;
}
.pt-12 {
    padding-top: 12px;
}
.ml-16 {
    margin-left: 16px;
}
.aline-item-center {
    align-items: center;
}
.mr-6 {
    margin-right: 6px;
}
.mr-16 {
    margin-right: 16px;
}
.pb-0 {
    padding-bottom: 0 !important;
}
input[type="checkbox"],
input[type="radio"] {
    accent-color: #409330 !important;
    cursor: pointer !important;
}
input[type="checkbox"] {
    width: 18px;
    height: 18px;
}
.z-index-5 {
    z-index: 99 !important;
}
</style>
