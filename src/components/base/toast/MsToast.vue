<template>
    <div class="m-toast">
        <div class="m-toast-main">
            <div class="left-toast">
                <div class="icon-succses ml-16 mr-16"></div>
                <div class="toast-content">
                    <b for="" class="title-toast">Thành công!</b>
                    <label for=""
                        >Bạn đã {{ toastAct }} thành công nhân viên</label
                    >
                </div>
            </div>
            <div class="icon-close mr-8" @click="closeOpenToast()"></div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            toastStatus: true,
        };
    },
    props: ["toastAct"],
    methods: {
        closeOpenToast() {
            this.toastStatus = !this.toastStatus;
        },
    },
};
</script>
<style>
.m-toast {
    position: fixed;
    right: 32px;
    bottom: 32px;
    z-index: 9999;
}
.m-toast-main {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 400px;
    height: 80px;
    background-color: #eef8ec;
    border-left: 5px solid #50b83c;
    border-radius: 4px;
    animation: toastLeft ease 0.3s, toastOut linear 1s 3s forwards;
}
.left-toast {
    display: flex;
}
.toast-content {
    align-items: center;
    flex-direction: column;
    justify-content: start;
}
.title-toast {
    display: block;
    font-size: 20px;
}
@keyframes toastLeft {
    from {
        opacity: 0;
        transform: translateX(calc(100% + 32px));
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}
@keyframes toastOut {
    to {
        opacity: 0;
    }
}
</style>
