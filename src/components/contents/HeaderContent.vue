<template>
    <div>
        <div class="m-main__header">
            <label for="">Nhân viên</label>
            <div class="m-main__header-right">
                <ms-button
                    btnText="Thêm mới nhân viên"
                    @click="closeOpenPopup()"
                ></ms-button>
            </div>
        </div>
        <ms-popup
            v-if="popupStatus"
            titlePopup="Thêm mới nhân viên"
            :closeOpenPopup="closeOpenPopup"
            :reloadList="reloadList"
            @openToastAdd="openToastAdd"
        ></ms-popup>
        <ms-toast v-show="toastStatusAdd" toastAct="thêm mới"></ms-toast>
    </div>
</template>
<script>
import MsButton from "../base/button/MsButton.vue";
import MsPopup from "../base/popup/MsPopup.vue";
import MsToast from "../base/toast/MsToast.vue";

export default {
    components: { MsButton, MsPopup, MsToast },
    props: ["reloadList"],
    data() {
        return {
            popupStatus: false,
            toastStatusAdd: false,
        };
    },
    methods: {
        closeOpenPopup() {
            this.popupStatus = !this.popupStatus;
        },
        openToastAdd(data) {
            // this.toastStatusAdd = data;
            this.toastStatusAdd = data;
            setTimeout(() => {
                this.toastStatusAdd = false;
            }, 4000);
        },
    },
};
</script>
<style>
.m-main__header {
    width: 100%;
    height: 56px;
    background-color: #f3f4f8;
    display: flex;
    align-items: start;
    justify-content: space-between;
}
</style>
