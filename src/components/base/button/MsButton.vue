<template>
    <button :class="['m-btn', btnExtra ? 'm-btn-extra' : '']">
        {{ btnText }}
    </button>
</template>
<script>
export default {
    props: {
        btnText: {
            type: String,
            default: "Button",
        },
        btnExtra: {
            type: Boolean,
            default: false,
        },
    },
};
</script>
<style>
.m-btn {
    height: 36px;
    border-radius: 4px;
    padding: 0 16px;
    border: none;
    background-color: #50b83c;
    font-weight: 500;
    font-size: 14px;
    text-align: center;
    line-height: 36px;
    color: #fff;
    display: flex;
    align-items: center;
}
.m-btn:hover {
    background-color: #73c663;
    cursor: pointer;
}
.m-btn:focus {
    background-color: #409330;
    cursor: pointer;
}

.m-btn-extra {
    background-color: #fff;
    color: #000;
    border: 1px solid #8d9096;
    font-weight: 500;
    font-size: 14;
}

.m-btn-extra:hover {
    background-color: #ccc;
}
.m-btn-extra:focus {
    background-color: #ccc;
}

/* .m-btn-icon {
    width: 20px;
    height: 20px;
    background-image: url(../../assets/img/Sprites.64af8f61.svg);
    background-repeat: no-repeat;
    background-position: -832px -462px;
} */
</style>
