<template>
    <div class="m-notification">
        <div class="m-noti-box">
            <div class="box-content">
                <div class="content">
                    <div class="icon-warning"></div>
                    <div class="message-content">
                        Bạn có thực sự muốn xóa nhân viên "{{ employeeName }}"
                        không?
                    </div>
                </div>
                <div class="content-footer">
                    <div>
                        <ms-button
                            btnText="Hủy"
                            btnExtra
                            @click="oClDialogDelete"
                        ></ms-button>
                    </div>
                    <div class="content-footer-left">
                        <ms-button
                            btnText="Đồng ý"
                            @click="handleDelete(employeeID)"
                        ></ms-button>
                    </div>
                </div>
            </div>
        </div>
        <ms-loading v-show="isLoading"></ms-loading>
        <div class="overlay" @click="oClDialogDelete"></div>
        <!-- <ms-toast v-show="openToast" toastAct="xóa"></ms-toast> -->
    </div>
</template>
<script>
import axios from "axios";
import MsButton from "../button/MsButton.vue";
import { BASE_URL } from "../../../constans/constans";
import MsLoading from "../loading/MsLoading.vue";

export default {
    components: { MsButton, MsLoading },
    data() {
        return {
            openToast: true,
            isLoading: false,
        };
    },
    props: ["oClDialogDelete", "employeeID", "employeeName", "reloadList"],
    methods: {
        async handleDelete(employee) {
            try {
                this.isLoading = true;
                const res = await axios.delete(`${BASE_URL}/${employee}`);
                if (res) {
                    this.openToast = true;
                    this.isLoading = false;
                    this.reloadList();
                    this.oClDialogDelete();
                    this.$emit("openToast", this.openToast);
                }
            } catch (error) {
                console.log(error);
            }
        },
    },
};
</script>
<style>
.m-notification {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 999;
}
.m-noti-box {
    width: 444px;
    min-width: 444px;
    height: 183px;
    background-color: #fff;
    border-radius: 4px;
    z-index: 1;
}
.box-content {
    padding: 32px;
}
.content {
    display: flex;
    align-items: flex-start;

    border-bottom: 1px solid #b8bcc3;
}
.content-footer {
    margin-top: 20px;
    display: flex;
    justify-content: space-between;
}
.content-footer-left {
    display: flex;
}
.message-content {
    overflow: auto;
    max-height: 400px;
    margin-bottom: 32px;
    padding-left: 16px;
}
</style>
