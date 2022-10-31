<template>
    <div id="dropdown__don-vi" class="dropdown" @click="dataShow = !dataShow">
        <input
            type="text"
            class="m-input dropdown__input"
            readonly
            :value="inputValue || defaultValue"
        />
        <div
            :class="[
                'dropdown__btn icon-down-dd',
                dataShow ? 'trasform-icon' : '',
            ]"
        ></div>
        <div
            :class="['dropdown__data', downData ? 'down-data' : '']"
            v-show="dataShow"
        >
            <ul>
                <li
                    v-for="dropdownItem in listDropdownItem"
                    :key="dropdownItem.title"
                    :class="[
                        'data-item',
                        inputValue == dropdownItem.title ||
                        inputValue == dropdownItem.DepartmentName
                            ? 'item-active'
                            : '',
                    ]"
                    :data-idDpm="dropdownItem.DepartmentId"
                    @click="
                        handleClickDD(
                            $event,
                            dropdownItem.title || dropdownItem.DepartmentName
                        )
                    "
                >
                    <!-- @click="handleClickDD(dropdownItem.value)" -->
                    {{ dropdownItem.title || dropdownItem.DepartmentName }}
                </li>
            </ul>
        </div>
        <br />
    </div>
</template>
<script>
export default {
    data() {
        return {
            inputValue: null,
            modelInput: "",
            dataShow: false,
            isActive: false,
        };
    },
    props: {
        listDropdownItem: {
            type: Array,
            default: [],
        },
        downData: {
            type: Boolean,
            default: false,
        },
        defaultValue: {
            type: [Number, String],
        },
    },
    // watch: {
    //     // Cần xem lại
    //     inputValueSetup() {
    //         if (this.inputValue == null) {
    //             this.inputValue = this.defaultValue;
    //         }
    //     },
    // },
    created() {
        this.inputValueSetup();
        this.$emit("default_dpm", {
            id: this.$props.listDropdownItem[0].DepartmentId,
            inputValue: this.listDropdownItem[0].DepartmentName,
        });
    },
    methods: {
        handleClickDD(event, value) {
            this.inputValue = value;
            this.$emit("dropdown-value", {
                id: event.target.dataset.iddpm,
                inputValue: this.inputValue,
            });
            this.$emit("pagging_value", this.inputValue);
        },
        inputValueSetup() {
            if (this.inputValue == null) {
                this.inputValue = this.defaultValue;
            }
        },
    },
};
</script>
<style>
.dropdown {
    height: 36px;
    border-radius: 4px;
    outline: none;
    display: flex;
    position: relative;
    align-items: center;
}
.dropdown__input {
    flex: 1;
    height: 36px;
    border: unset;
    width: 72px;
}
.dropdown__input::placeholder {
    color: black;
}
.dropdown__input:focus {
    border: 1px solid #50b83c;
}
ul {
    padding-left: 0;
}

.dropdown__btn {
    width: 36px;
    height: 36px;
    font-size: 20px;
    border-radius: 4px;
    outline: unset;
    border: none;
    position: absolute;
    right: 16px;
    background-color: unset;
    cursor: pointer;
    background-image: url(../../../assets/img/Sprites.64af8f61.svg);
    background-position: -1129px -365px;
    width: 14px;
    height: 8px;
}

.dropdown__data {
    position: absolute;
    background-color: #fff;
    bottom: calc(100% + 1px);
    border-radius: 4px;
    max-height: 200px;
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
}
.data-item {
    height: 36px;
    display: flex;
    align-items: center;
    border-radius: 4px;
    padding: 0 12px;
}
.data-item:hover {
    background-color: rgb(185, 226, 177);
    cursor: pointer;
}
.item-active {
    background-color: rgb(185, 226, 177);
}
.trasform-icon {
    transform: rotate(180deg);
}
.border {
    border: #50b83c 1px solid !important;
    border-radius: 4px !important;
}
.down-data {
    bottom: unset;
    top: calc(100% + 1px);
    z-index: 10;
}
</style>
