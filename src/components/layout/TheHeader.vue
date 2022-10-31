<template>
    <div class="m-header">
        <div class="m-header__left">
            <div
                id="thu-gon-sidebar"
                class="icon-3-gach sidebar-hiden"
                @click="closeSidebar()"
                v-show="!colHeader"
            >
                <div class="tooltip tooltip__3-gach">
                    <label for=""
                        >Thu gọn Sidebar
                        <div></div
                    ></label>
                </div>
            </div>
            <b class="header-text"
                >CÔNG TY TNHH SẢN XUẤT - THƯƠNG MẠI - DỊCH VỤ QUI PHÚC</b
            >
            <div class="icon-down"></div>
        </div>
        <div class="m-header__right">
            <div class="icon-bell">
                <div class="tooltip tooltip__bell">
                    <label for=""
                        >Thông báo
                        <div></div
                    ></label>
                </div>
            </div>
            <div class="icon-user"></div>
            <b class="user-name">Nguyễn Văn Mạnh</b>
            <div class="icon-down-small"></div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            colHeader: false,
        };
    },
    props: ["openCloseSidebar"],
    created() {
        this.eventBus.on("openSidebar", e => (this.colHeader = e));
    },
    methods: {
        closeSidebar() {
            this.colHeader = !this.colHeader;
            this.eventBus.emit("closeSidebar", this.colHeader);
        },
    },
};
</script>
<style>
.m-header {
    width: calc(100% - 200px);
    height: 56px;
    background-color: #fff;
    float: left;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.m-header__left {
    display: flex;
    align-items: center;
    padding-left: 16px;
}
.header-text {
    padding-right: 8px;
}
.m-header__right {
    display: flex;
    align-items: center;
    padding-right: 16px;
}
.user-name {
    padding-left: 4px;
    padding-right: 8px;
}
</style>
