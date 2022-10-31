<template>
    <div class="m-main">
        <header-content :reloadList="getListPageOne"></header-content>
        <main-content
            :listEmployee="listEmployee"
            :reloadList="getListPageOne"
            @searchValue="searchValue"
        ></main-content>
        <pagging-content
            :totalRecord="totalRecord"
            :totalPage="totalPage"
            :pageNumberData="pageNumberData"
            @number-item="funNumberItem"
            @nextPage="funNextPage"
            @downPage="funDownPage"
        ></pagging-content>
        <ms-loading v-show="isLoading"></ms-loading>
    </div>
</template>
<script>
import axios from "axios";
import HeaderContent from "../contents/HeaderContent.vue";
import MainContent from "../contents/MainContent.vue";
import PaggingContent from "../contents/PaggingContent.vue";
import { BASE_URL } from "../../constans/constans";
import MsLoading from "../base/loading/MsLoading.vue";

export default {
    components: { HeaderContent, PaggingContent, MainContent, MsLoading },
    data() {
        return {
            listEmployee: [],
            totalRecord: 0,
            totalPage: 0,
            isLoading: false,
            pageNumberData: 1,
            numberItemData: 10,
            search: "",
        };
    },
    watch: {
        pageNumberData() {
            this.getList();
        },
        numberItemData() {
            this.getListPageOne();
        },
        search() {
            this.getListPageOne();
        },
    },
    created() {
        this.getList();
        // Emit bus
        this.eventBus.emit("getList", this.getList());
    },
    methods: {
        /**
         * Lấy list data
         * author: NHAnh(26/10/2022)
         */
        async getList() {
            // Bật loading
            this.isLoading = true;
            const res = await axios
                .get(
                    `${BASE_URL}/filter?pageSize=${this.numberItemData}&pageNumber=${this.pageNumberData}${this.search}`
                )
                .then(res => {
                    this.listEmployee = res.data.Data;
                    // Thêm trường checked cho từng ô dữ liệu
                    this.listEmployee.map(e => (e.isChecked = false));
                    // Thêm giá trị đóng mở thanh chức năng
                    this.listEmployee.map(e => (e.closeOpenDelete = false));

                    // Lấy số bản ghi
                    this.totalRecord = res.data.TotalRecord;
                    // Lấy số trang
                    this.totalPage = res.data.TotalPage;
                    // Tắt Loading
                    this.isLoading = false;
                })
                .catch(e => console.log(e));
            if (!res) {
                setTimeout(() => {
                    // Tắt Loading
                    this.isLoading = false;
                }, 2000);
            }
        },

        /**
         * lấy listdata trang đầu tiên
         * author: NHAnh (31/10/2022)
         */
        getListPageOne() {
            this.pageNumberData = 1;
            this.getList();
        },

        /**
         * Lấy số trang và số dữ liệu trên 1 trang từ cpn Pagging
         * author: NHAnh(26/10/2022)
         */
        funNumberItem(data) {
            this.pageNumberData = 1;
            this.numberItemData = data;
        },

        /**
         * search value
         * author: NHAnh(30/10/2022)
         */
        searchValue(data) {
            if (data) {
                this.search = `&employeeFilter=${data}`;
            } else {
                this.search = "";
            }
        },
        /**
         * Tiến lùi số trang
         * author: NHAnh(26/10/2022)
         */
        funNextPage(data) {
            this.pageNumberData = data;
        },
        funDownPage(data) {
            this.pageNumberData = data;
        },
    },
};
</script>

<style>
.m-main {
    width: calc(100% - var(--width-sidebar) - 36px);
    height: calc(100vh - 56px - 36px);
    background-color: #fff;
    float: left;
    overflow: hidden;
    margin: 24px 12px 12px 24px;
    position: relative;
}

.tooltip-relative {
    position: relative;
}
.tooltip-relative:hover .tooltip {
    display: block;
}
.m-main__header label {
    font-size: 24px;
    font-weight: 700;
    line-height: 36px;
}
.m-main__table {
    width: calc(100% -32px);
    height: calc(100% - 105px);
    background-color: #fff;
    padding-left: 16px;
    padding-right: 16px;
}
.m-input-icon {
    background-repeat: no-repeat;
    background-position: right 6px center;
    padding-right: 32px;
    padding-left: 16px;
}
.m-main__table-header {
    width: 100%;
    height: 56px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-right: -16px;
}
.m-main__table-header input {
    margin-right: 16px;
}
.m-main__table-body {
    /* padding-right: 8px; */
    max-height: calc(100% - 60px);
    overflow: auto;
}
.m-main__table-body::-webkit-scrollbar {
    width: 10px;
    background: #000;
    height: 10px;
}
.m-main__table-body::-webkit-scrollbar {
    width: 10px;
    border-radius: 4px;
}

/* Track */
.m-main__table-body::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 4px;
}

/* Handle */
.m-main__table-body::-webkit-scrollbar-thumb {
    background: #888;
    border-radius: 4px;
}

/* Handle on hover */
.m-main__table-body::-webkit-scrollbar-thumb:hover {
    background: #555;
    border-radius: 4px;
}

/* End update table */

/* End Main */
</style>
