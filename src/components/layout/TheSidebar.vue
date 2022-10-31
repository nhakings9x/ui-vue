<template>
    <div :class="['m-sidebar', updateSidebar ? 'sidebar-toggle' : '']">
        <div class="m-sidebar__header">
            <div class="icon-9-cham sidebar-hiden"></div>
            <div class="m-sidebar__logo sidebar-hiden"></div>
            <b class="sidebar-hiden">KẾ TOÁN</b>
            <div
                id="mo-rong-side-bar"
                class="icon-3-gach-white"
                @click="openSidebar()"
            >
                <div class="tooltip tooltip__3-gach-white">
                    <label for=""
                        >Mở rộng Sidebar
                        <div></div
                    ></label>
                </div>
            </div>
        </div>
        <div class="m-sidebar__main">
            <div class="m-sidebar__menu">
                <a class="m-sidebar__menu-item item-1">
                    <div class="item-icon icon-tong-quan"></div>
                    <div class="item-text sidebar-hiden">Tổng quan</div>
                </a>
                <a class="m-sidebar__menu-item item-2">
                    <div class="item-icon icon-tien-mat"></div>
                    <div class="item-text sidebar-hiden">Tiền mặt</div>
                </a>
                <a class="m-sidebar__menu-item item-3">
                    <div class="item-icon icon-hop-dong"></div>
                    <div class="item-text sidebar-hiden">Tiền gửi</div>
                </a>
                <a class="m-sidebar__menu-item item-4">
                    <div class="item-icon icon-mua-hang"></div>
                    <div class="item-text sidebar-hiden">Mua hàng</div>
                </a>
                <a class="m-sidebar__menu-item item-5">
                    <div class="item-icon icon-ban-hang"></div>
                    <div class="item-text sidebar-hiden">Bán hàng</div>
                </a>
                <a class="m-sidebar__menu-item item-6">
                    <div class="item-icon icon-qlhd"></div>
                    <div class="item-text sidebar-hiden">Quản lý hóa đơn</div>
                </a>
                <a class="m-sidebar__menu-item item-7">
                    <div class="item-icon icon-kho"></div>
                    <div class="item-text sidebar-hiden">Kho</div>
                </a>
                <a class="m-sidebar__menu-item item-8">
                    <div class="item-icon icon-cong-dung-cu"></div>
                    <div class="item-text sidebar-hiden">Công cụ dụng cụ</div>
                </a>
                <a class="m-sidebar__menu-item item-9">
                    <div class="item-icon icon-thue"></div>
                    <div class="item-text sidebar-hiden">Thuế</div>
                </a>
                <a class="m-sidebar__menu-item item-10">
                    <div class="item-icon icon-gia-thanh"></div>
                    <div class="item-text sidebar-hiden">Giá thành</div>
                </a>
                <a class="m-sidebar__menu-item item-11">
                    <div class="item-icon icon-tong-hop"></div>
                    <div class="item-text sidebar-hiden">Tổng hợp</div>
                </a>
                <a class="m-sidebar__menu-item item-12">
                    <div class="item-icon icon-ngan-sach"></div>
                    <div class="item-text sidebar-hiden">Ngân sách</div>
                </a>
                <a class="m-sidebar__menu-item item-13">
                    <div class="item-icon icon-bao-cao"></div>
                    <div class="item-text sidebar-hiden">Báo cáo</div>
                </a>
                <a class="m-sidebar__menu-item item-14">
                    <div class="item-icon icon-pttc"></div>
                    <div class="item-text sidebar-hiden">
                        Phân tích tài chính
                    </div>
                </a>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            updateSidebar: null,
        };
    },
    props: {},
    created() {
        this.eventBus.on("closeSidebar", e => (this.updateSidebar = e));
    },
    methods: {
        openSidebar() {
            this.updateSidebar = !this.updateSidebar;
            this.eventBus.emit("openSidebar", this.updateSidebar);
        },
    },
};
</script>
<style>
.m-sidebar {
    width: var(--width-sidebar);
    height: 100vh;
    background-color: #38393d;
    float: left;
    color: #fff;
    overflow: auto;
}

.m-sidebar__header {
    height: 56px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
}
.m-sidebar__header b {
    padding-left: 4px;
    cursor: pointer;
}

.m-sidebar__logo {
    background-image: url("../../assets/favicon.ico");
    width: 36px;
    height: 36px;
    background-size: cover;
    cursor: pointer;
}

.m-sidebar__main {
    height: calc(100vh - 100px);
    width: 100%;
}
.m-sidebar__menu {
    padding: 20px 12px;
    height: calc(100% - 84px);
}
.m-sidebar__menu-item {
    display: flex;
    /* width: 100%; */
    align-items: center;
    height: 24px;
    margin-bottom: 4px;
    padding: 10px 12px;
    position: relative;
}
.item-icon {
    padding-right: 12px;
}
.item-text {
    color: #a8a8a8;
}
.m-sidebar__menu-item:hover {
    background-color: #777983;
    border-radius: 4px;
    cursor: pointer;
}
.m-sidebar__menu-item:hover .item-text {
    color: #fff;
}
.m-sidebar__menu-item:hover .item-icon {
    opacity: 1;
}

.m-sidebar-bottom {
    height: 44px;
    width: 100%;
    bottom: 0;
}

/* CSS thu Gọn (25/10/2022) */
.sidebar-toggle {
    --width-sidebar: 73px !important;
    width: var(--width-sidebar);
    height: 100vh;
    overflow: unset;
}
.sidebar-toggle + div {
    width: calc(100% - 73px);
}
.sidebar-toggle + div + div {
    width: calc(100% - 73px - 36px);
}
.sidebar-toggle .m-sidebar__header .sidebar-hiden {
    display: none;
}
.sidebar-toggle .m-sidebar__header .icon-3-gach-white {
    display: block;
}
.sidebar-toggle
    .m-sidebar__main
    .m-sidebar__menu
    .m-sidebar__menu-item
    .item-text {
    position: absolute;
    display: none;
    align-items: center;
    white-space: nowrap;
    padding: 0 16px;
    left: 150%;
    height: 40px;
    border-radius: 4px;
    background-color: #38393d;
    z-index: 10;
}
.sidebar-toggle
    .m-sidebar__main
    .m-sidebar__menu
    .m-sidebar__menu-item
    .item-text::before {
    content: "";
    position: absolute;
    left: -20px;
    top: 10px;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 10px solid transparent;
    border-right: 10px solid #38393d;
}
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-1:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-2:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-3:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-4:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-5:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-6:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-7:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-8:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-9:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-10:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-11:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-12:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-13:hover .item-text,
.sidebar-toggle .m-sidebar__main .m-sidebar__menu .item-14:hover .item-text {
    display: flex;
}
</style>
