<template>
    <div class="m-main__pagging">
        <label for="" class="m-pagging__left"
            >Tổng: <b>{{ totalRecord }}</b></label
        >

        <div class="m-pagging__right">
            <label for="">Số bản ghi/trang : </label>
            <div id="combobox__pagging" class="combobox mr-16">
                <div class="pagging-list">
                    <ms-dropdown
                        :listDropdownItem="listPagging"
                        :defaultValue="10"
                        @pagging_value="paggingNumber"
                    ></ms-dropdown>
                </div>
            </div>

            <label for="" class="pagging__label mr-16"
                ><b
                    >{{ numberItem * (pageNumberData - 1) + 1 }} -
                    {{ numberItem * pageNumberData }}</b
                >
                bản ghi</label
            >

            <button class="icon-left mr-16" @click="downPage()"></button>
            <button class="icon-right" @click="nextPage()"></button>
        </div>
    </div>
</template>
<script>
import MsDropdown from "../base/dropdown/MsDropdown.vue";
export default {
    components: { MsDropdown },
    props: {
        // Tổng bản ghi
        totalRecord: {
            type: Number,
        },
        // Tổng số trang
        totalPage: {
            type: Number,
        },
        // trang hiện tại
        pageNumberData: {
            type: Number,
        },
    },
    data() {
        return {
            listPagging: [
                {
                    title: 10,
                },
                {
                    title: 20,
                },
                {
                    title: 50,
                },
                {
                    title: 100,
                },
            ],
            pageNumber: 1,
            numberItem: 10,
            fisrtData: 0,
            lastData: 0,
        };
    },
    emits: ["pageNumber:pageNumber", "numberItem:numberItem"],
    watch: {
        fisrtData() {
            this.fisrtData = this.numberItem * (this.pageNumberData - 1) + 1;
        },
        lastData() {
            this.lastData = this.pageNumberData = this.totalPage
                ? this.numberItem * this.pageNumberData
                : this.numberItem * this.pageNumberData -
                  (this.numberItem * this.pageNumberData - this.totalRecord);
        },
    },
    methods: {
        /**
         * Tiến 1 trang
         * author: NHAnh (26/10/2022)
         */
        nextPage() {
            this.pageNumber = this.pageNumberData;
            if (this.pageNumber < this.totalPage) {
                this.pageNumber++;
            }
            this.$emit("nextPage", this.pageNumber);
        },
        /**
         * lùi 1 trang
         * author: NHAnh (26/10/2022)
         */
        downPage() {
            this.pageNumber = this.pageNumberData;

            if (this.pageNumber > 1) {
                this.pageNumber--;
            }
            this.$emit("downPage", this.pageNumber);
        },

        /**
         * lấy dữ liệu dropdown
         * author: NHA (29/10/2022)
         */
        paggingNumber(data) {
            this.numberItem = data;
            this.$emit("number-item", this.numberItem);
        },
    },
};
</script>
<style>
.m-main__pagging {
    position: absolute;
    height: 48px;
    width: calc(100% - 32px);
    bottom: 0;
    margin-left: 16px;
    margin-right: 16px;
    border-top: 1px solid #bbbbbb;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.m-pagging__left {
    padding-left: 16px;
}

.m-pagging__right {
    display: flex;
    align-items: center;
    padding-right: 16px;
}
.pagging-number {
    display: flex;
    align-items: center;
}
.number-page-none {
    border: none;
    background-color: #fff;
    min-width: 24px;

    cursor: pointer;
}

.pagging__label {
    width: auto;
}
.pagging-list {
    width: 80px;
}
</style>
