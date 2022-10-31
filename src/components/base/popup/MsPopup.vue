<template>
    <div class="m-popup">
        <div class="m-popup__content">
            <div class="m-popup__header">
                <div class="m-popup__title">
                    <div class="m-popup__title-header">
                        <div class="m-popup__title-text">
                            {{ titlePopup }}
                        </div>
                        <label for="">
                            <input
                                type="checkbox"
                                class="popup-checkbox"
                                tabindex="22"
                            />
                            <span>Là khách hàng</span>
                        </label>
                        <label for="">
                            <input
                                id="lastCheckBox"
                                type="checkbox"
                                class="popup-checkbox"
                                tabindex="23"
                            />
                            <span>Là nhà cung cấp</span>
                        </label>
                    </div>
                </div>
                <div class="m-popup__close">
                    <div class="icon-help mr-8">
                        <div class="tooltip tooltip__help">
                            <label for=""
                                >Trợ giúp (F1)
                                <div></div
                            ></label>
                        </div>
                    </div>
                    <div
                        id="js-close"
                        class="icon-close"
                        @click="closeOpenPopup()"
                    >
                        <div class="tooltip tooltip__close">
                            <label for=""
                                >Đóng (ESC)
                                <div></div
                            ></label>
                        </div>
                    </div>
                </div>
            </div>
            <div class="m-popup__content-main">
                <div class="m-popup__conntent-employee">
                    <div class="content__employee-form">
                        <div class="employee-form__left">
                            <div class="form-popup">
                                <div class="ma-nhan-vien">
                                    <form-control
                                        labelForm="Mã"
                                        required
                                        @dataInput="dataForm"
                                        formControlName="EmployeeCode"
                                        :validateForm="validate.code"
                                        :errorText="errors.code"
                                        @blur="validateForm()"
                                        tabindex="1"
                                    ></form-control>
                                </div>
                                <div class="form-group ten-nhan-vien">
                                    <form-control
                                        labelForm="Tên"
                                        required
                                        @dataInput="dataForm"
                                        :validateForm="validate.name"
                                        :errorText="errors.name"
                                        @blur="validateForm()"
                                        formControlName="EmployeeName"
                                        tabindex="2"
                                    ></form-control>
                                </div>
                            </div>
                            <div class="form-popup">
                                <div class="form-group don-vi">
                                    <label for=""
                                        >Đơn vị
                                        <span class="color-red">*</span></label
                                    >
                                    <ms-dropdown
                                        :listDropdownItem="listDepartment"
                                        defaultValue="Phòng nhân sự"
                                        downData
                                        tabindex="3"
                                        @dropdown-value="dpId"
                                        @default_dpm="defaultDPM"
                                    ></ms-dropdown>
                                </div>
                            </div>
                            <div class="form-popup">
                                <div class="chuc-danh">
                                    <form-control
                                        labelForm="Chức danh"
                                        @dataInput="dataForm"
                                        @blur="validateForm()"
                                        :validateForm="
                                            validate.employeePosition
                                        "
                                        :errorText="errors.employeePosition"
                                        formControlName="EmployeePosition"
                                        tabindex="4"
                                    ></form-control>
                                </div>
                            </div>
                        </div>
                        <div class="employee-form__right">
                            <div class="form-popup">
                                <div class="form-group ngay-sinh">
                                    <label for="">Ngày sinh</label>
                                    <input
                                        id="DateOfBirth"
                                        type="date"
                                        :class="[
                                            'm-input required',
                                            validate.DateOfBirth
                                                ? 'm-input__error'
                                                : '',
                                        ]"
                                        tabindex="5"
                                        v-model="employee.DateOfBirth"
                                        @blur="validateForm()"
                                    />
                                    <label for="" class="error_text">{{
                                        errors.DateOfBirth
                                    }}</label>
                                </div>
                                <div class="form-group gioi-tinh">
                                    <label for="">Giới tính</label>
                                    <div class="m-flex aline-item-center">
                                        <input
                                            class="input-gioi-tinh"
                                            type="radio"
                                            id="Nam"
                                            name="fav_language"
                                            value="1"
                                            tabindex="6"
                                            v-model="employee.Gender"
                                        />
                                         
                                        <label
                                            for="Nam"
                                            class="lable-gioi-tinh pb-0"
                                            >Nam</label
                                        ><br />
                                         
                                        <input
                                            class="input-gioi-tinh"
                                            type="radio"
                                            id="Nam"
                                            name="fav_language"
                                            value="0"
                                            tabindex="7"
                                            v-model="employee.Gender"
                                        />
                                         
                                        <label
                                            for="Nữ"
                                            class="lable-gioi-tinh pb-0"
                                            >Nữ</label
                                        ><br />
                                         
                                        <input
                                            class="input-gioi-tinh"
                                            type="radio"
                                            id="Nam"
                                            name="fav_language"
                                            value="2"
                                            tabindex="8"
                                            v-model="employee.Gender"
                                        />
                                         
                                        <label
                                            for="Khác"
                                            class="lable-gioi-tinh pb-0"
                                            >Khác</label
                                        >
                                    </div>
                                </div>
                            </div>
                            <div class="form-popup">
                                <div class="so-cmnd">
                                    <form-control
                                        labelForm="Số CMND"
                                        @dataInput="dataForm"
                                        :validateForm="validate.IdentityNumber"
                                        :errorText="errors.IdentityNumber"
                                        formControlName="IdentityNumber"
                                    ></form-control>
                                </div>
                                <div class="form-group ngay-cap">
                                    <label for="">Ngày cấp</label>
                                    <input
                                        type="date"
                                        class="m-input required"
                                        v-model="employee.IdentityDate"
                                        tabindex="10"
                                    />
                                    <label for="" class="error_text">{{
                                        errors.IdentityDate
                                    }}</label>
                                </div>
                            </div>
                            <div class="form-popup">
                                <div class="noi-cap">
                                    <form-control
                                        labelForm="Nơi cấp"
                                        @dataInput="dataForm"
                                        :validateForm="validate.IdentityPlace"
                                        :errorText="errors.IdentityPlace"
                                        formControlName="IdentityPlace"
                                    ></form-control>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="content-employee__contact">
                        <div class="form-popup">
                            <div class="dia-chi">
                                <form-control
                                    labelForm="Địa chỉ"
                                    @dataInput="dataForm"
                                    formControlName="Address"
                                    :validateForm="validate.Address"
                                    :errorText="errors.Address"
                                ></form-control>
                            </div>
                        </div>
                        <div class="form-popup">
                            <div class="di-dong">
                                <form-control
                                    labelForm="ĐT di động"
                                    @dataInput="dataForm"
                                    :validateForm="validate.PhoneNumber"
                                    :errorText="errors.PhoneNumber"
                                    formControlName="PhoneNumber"
                                ></form-control>
                            </div>
                            <div class="di-dong">
                                <form-control
                                    labelForm="Đt cố định"
                                    @dataInput="dataForm"
                                    :validateForm="validate.TelephoneNumber"
                                    :errorText="errors.TelephoneNumber"
                                    formControlName="TelephoneNumber"
                                ></form-control>
                            </div>
                            <div class="di-dong">
                                <form-control
                                    labelForm="Email"
                                    @dataInput="dataForm"
                                    :validateForm="validate.Email"
                                    :errorText="errors.Email"
                                    formControlName="Email"
                                ></form-control>
                            </div>
                        </div>
                        <div class="form-popup">
                            <div class="di-dong">
                                <form-control
                                    labelForm="Tài khoản ngân hàng"
                                    @dataInput="dataForm"
                                    :validateForm="validate.BankAccountNumber"
                                    :errorText="errors.BankAccountNumber"
                                    formControlName="BankAccountNumber"
                                ></form-control>
                            </div>
                            <div class="form-group di-dong">
                                <form-control
                                    labelForm="Tên ngân hàng"
                                    @dataInput="dataForm"
                                    :validateForm="validate.BankBranchName"
                                    :errorText="errors.BankBranchName"
                                    formControlName="BankBranchName"
                                ></form-control>
                            </div>
                            <div class="form-group di-dong">
                                <form-control
                                    labelForm="Chi nhánh"
                                    @dataInput="dataForm"
                                    :validateForm="validate.BankProvinceName"
                                    :errorText="errors.BankProvinceName"
                                    formControlName="BankProvinceName"
                                ></form-control>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="m-popup__footer">
                    <ms-button btnText="Hủy" btnExtra></ms-button>
                    <div class="m-popup__footer-left">
                        <ms-button
                            btnText="Cất"
                            btnExtra
                            class="mr-8"
                            @click="validateForm()"
                        ></ms-button>
                        <ms-button
                            btnText="Cất và thêm"
                            @click="addEmployee()"
                        ></ms-button>
                    </div>
                </div>
            </div>
        </div>
        <div class="overlay" @click="closeOpenPopup()"></div>
        <dialog-warning
            v-if="isWarning"
            :isWarningDialog="isWarningDialog"
            :employeeCode="this.employee.EmployeeCode"
            :warning="isWarningStatus"
            :errorCode="errorCode"
        ></dialog-warning>
    </div>
</template>
<script>
import MsButton from "../button/MsButton.vue";
import MsDropdown from "../dropdown/MsDropdown.vue";
import FormControl from "../form-control/FormControl.vue";
import axios from "axios";
import { BASE_URL, DEPARTMENT_URL } from "../../../constans/constans";
import DialogWarning from "../dialog/dialogWarning.vue";

export default {
    components: { FormControl, MsDropdown, MsButton, DialogWarning },
    data() {
        return {
            employee: {
                EmployeeCode: "",
                EmployeeName: "",
                DepartmentId: "",
                Gender: "",
                EmployeePosition: "",
                DateOfBirth: "",
                IdentityNumber: "",
                IdentityDate: "",
                IdentityPlace: "",
                Address: "",
                PhoneNumber: "",
                TelephoneNumber: "",
                Email: "",
                BankAccountNumber: "",
                BankBranchName: "",
                BankProvinceName: "",
            },
            validate: {
                code: false,
                name: false,
                employeePosition: false,
                DateOfBirth: false,
                IdentityNumber: false,
                IdentityDate: false,
                IdentityDate: false,
                IdentityPlace: false,
                PhoneNumber: false,
                TelephoneNumber: false,
                Address: false,
                Email: false,
                BankAccountNumber: false,
                BankBranchName: false,
                BankProvinceName: false,
            },
            errors: {
                code: "",
                name: "",
                employeePosition: "",
                DateOfBirth: "",
                IdentityDate: "",
                IdentityNumber: "",
                IdentityDate: "",
                IdentityPlace: "",
                PhoneNumber: "",
                TelephoneNumber: "",
                Address: "",
                Email: "",
                BankAccountNumber: "",
                BankBranchName: "",
                BankProvinceName: "",
            },
            listDepartment: [],
            testValue: "",
            testInput: "",
            openToast: true,
            isWarning: false,
            isWarningStatus: false,
            errorCode: false,
        };
    },
    props: ["titlePopup", "closeOpenPopup", "employeeEditItem", "reloadList"],
    emits: ["closeOpenPopup"],
    watch: {
        employeeEditItem() {
            console.log(this.employeeEditItem);
        },
        // validateForm() {
        //     this.validate.code = false;
        //     this.errors.code;
        // },
    },
    created() {
        this.getDepartmentList();
    },

    methods: {
        defaultDPM(data) {
            this.employee.DepartmentId = data.id;
        },
        /**
         * Lấy giá trị ô input gán vào employee
         * author: NHAnh (29/10/2022)
         */
        dataForm(data) {
            switch (data.target) {
                case "EmployeeCode":
                    this.employee.EmployeeCode = data.value;
                    break;
                case "EmployeeName":
                    this.employee.EmployeeName = data.value;
                    break;
                case "EmployeePosition":
                    this.employee.EmployeePosition = data.value;
                    break;
                case "IdentityNumber":
                    this.employee.IdentityNumber = data.value;
                    break;
                case "IdentityPlace":
                    this.employee.IdentityPlace = data.value;
                    break;
                case "Address":
                    this.employee.Address = data.value;
                    break;
                case "PhoneNumber":
                    this.employee.PhoneNumber = data.value;
                    break;
                case "TelephoneNumber":
                    this.employee.TelephoneNumber = data.value;
                    break;
                case "Email":
                    this.employee.Email = data.value;
                    break;
                case "BankAccountNumber":
                    this.employee.BankAccountNumber = data.value;
                    break;
                case "BankBranchName":
                    this.employee.BankBranchName = data.value;
                    break;
                case "BankProvinceName":
                    this.employee.BankProvinceName = data.value;
                    break;
                default:
                // code block
            }
        },

        /**
         * Validate Form
         * author: NHAnh (30/10/2022)
         */
        validateForm() {
            (this.validate = {
                code: false,
                name: false,
                employeePosition: false,
                DateOfBirth: false,
                IdentityNumber: false,
                IdentityDate: false,
                IdentityDate: false,
                IdentityPlace: false,
                PhoneNumber: false,
                TelephoneNumber: false,
                Address: false,
                Email: false,
                BankAccountNumber: false,
                BankBranchName: false,
                BankProvinceName: false,
            }),
                (this.errors = {
                    code: "",
                    name: "",
                    employeePosition: "",
                    DateOfBirth: "",
                    IdentityDate: "",
                    IdentityNumber: "",
                    IdentityDate: "",
                    IdentityPlace: "",
                    PhoneNumber: "",
                    TelephoneNumber: "",
                    Address: "",
                    Email: "",
                    BankAccountNumber: "",
                    BankBranchName: "",
                    BankProvinceName: "",
                }),
                (this.errors.code = "");
            if (!this.employee.EmployeeCode) {
                this.validate.code = true;
                this.errors.code = "Mã nhân viên không được để trống";
                return false;
            }
            if (!this.employee.EmployeeName) {
                this.validate.name = true;
                this.errors.name = "Tên nhân viên không được để trống";
                return false;
            }
            if (this.validateTime(this.employee.DateOfBirth)) {
                this.validate.DateOfBirth = true;
                this.errors.DateOfBirth = "Ngày sinh không hợp lệ";
                return false;
            }

            if (this.employee.IdentityNumber) {
                if (!this.isNumber(this.employee.IdentityNumber)) {
                    this.validate.IdentityNumber = true;
                    this.errors.IdentityNumber = "Số CMND phải là số";
                    return false;
                }
            }
            if (this.employee.IdentityDate) {
                if (this.validateTime(this.employee.IdentityDate)) {
                    this.validate.IdentityDate = true;
                    this.errors.IdentityDate = "Ngày cấp không hợp lệ";
                    return false;
                }
            }

            if (this.employee.PhoneNumber) {
                if (!this.isNumber(this.employee.PhoneNumber)) {
                    this.validate.PhoneNumber = true;
                    this.errors.PhoneNumber = "ĐT di động phải là số";
                    return false;
                }
            }

            if (this.employee.TelephoneNumber) {
                if (!this.isNumber(this.employee.TelephoneNumber)) {
                    this.validate.TelephoneNumber = true;
                    this.errors.TelephoneNumber = "ĐT cố định phải là số";
                    return false;
                }
            }
            if (this.employee.Email) {
                if (!this.isEmail(this.employee.Email)) {
                    this.validate.Email = true;
                    this.errors.Email = "Email không đúng định dạng";
                    return false;
                }
            }
            if (this.employee.BankAccountNumber) {
                if (!this.isNumber(this.employee.BankAccountNumber)) {
                    this.validate.BankAccountNumber = true;
                    this.errors.BankAccountNumber =
                        "Tài khoản ngân hàng phải là số";
                    return false;
                }
            }
            return true;
        },

        /**
         * Validate số, emmail, date
         * author: NHAnh (30/10/2022)
         */
        isNumber(value) {
            return /^-?\d+$/.test(value);
        },
        isEmail(email) {
            let regex =
                /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
            return regex.test(email);
        },
        validateTime(dateTime) {
            let today = new Date();
            let dataInputDate = new Date(dateTime);
            if (dataInputDate > today) {
                return true;
            }
            return false;
        },

        /**
         * Get List Department
         * author: NHAnh (29/10/2022)
         */
        async getDepartmentList() {
            await axios
                .get(`${DEPARTMENT_URL}`)
                .then(res => (this.listDepartment = res.data))
                .catch(error => {
                    console.log(error);
                });
        },

        /**
         * Lấy ID Department
         * author: NHAnh (29/10/2022)
         */
        getIdDepartment(dpName) {
            var department = this.listDepartment.find(
                dp => (dp.DepartmentName = dpName)
            );
            return department.DepartmentId;
        },
        dpId(data) {
            // console.log(data);
            this.employee.DepartmentId = data.id;
        },

        /**
         * Thêm mới nhân viên
         */
        async addEmployee() {
            if (this.validateForm()) {
                try {
                    const res = await axios.post(`${BASE_URL}`, this.employee);
                    if (res) {
                        this.employee = {
                            EmployeeCode: "",
                            EmployeeName: "",
                            DepartmentId: "",
                            Gender: "",
                            EmployeePosition: "",
                            DateOfBirth: "",
                            IdentityNumber: "",
                            IdentityDate: "",
                            IdentityPlace: "",
                            Address: "",
                            PhoneNumber: "",
                            TelephoneNumber: "",
                            Email: "",
                            BankAccountNumber: "",
                            BankBranchName: "",
                            BankProvinceName: "",
                        };
                        this.reloadList();
                        this.$emit("openToastAdd", this.openToast);
                        this.closeOpenPopup();
                    }
                } catch (error) {
                    console.log(error.response.data.devMsg);
                    if (
                        error.response.data.devMsg ==
                        "Mã khách hàng đã tồn tại trong hệ thống."
                    ) {
                        this.isWarningStatus = true;
                        this.errorCode = false;
                        this.isWarningDialog();
                    } else if (
                        error.response.data.devMsg ==
                        "Thông tin mã nhân viên không hợp lệ."
                    ) {
                        (this.errorCode = true), (this.isWarningStatus = false);
                        this.isWarningDialog();
                    }
                }
            } else {
                this.errorCode = false;
                this.isWarningStatus = false;
                this.isWarningDialog();
            }
        },

        /**
         * Hiện dialog warning
         * author: NHAnh (31/10/2022)
         */
        isWarningDialog() {
            this.isWarning = !this.isWarning;
        },
    },
};
</script>
<style>
.m-popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10000;
}
.m-popup__content {
    /* min-width: 900px; */
    width: 900px;
    background-color: #fff;
    border: 1px solid #666666;
    border-radius: 4px;
    z-index: 1;
}
/* Header */
.m-popup__header {
    width: 100%;
    display: flex;
    justify-content: space-between;
    position: relative;
}
.m-popup__title {
    width: 100%;
    padding: 20px 32px;
    padding-right: 12px;
    position: relative;
    overflow: hidden;
    border-radius: 5px 5px 0 0;
}
.m-popup__title-header {
    display: flex;
}
.m-popup__title-header label {
    display: flex;
    align-items: center;
    justify-content: start;
    padding: 0 1.5rem;
}
.m-popup__title-header label span {
    padding-left: 10px;
}
.m-popup__title-text {
    font-size: 24px;
    color: #111;
    font-weight: 700;
}
.popup-checkbox {
    width: 18px;
    height: 18px;
    justify-content: start;
    cursor: pointer;
}
.m-popup__close {
    display: flex;
    padding: 12px;
}
/* End Header */

/* Popup content */
.m-popup__content-main {
    overflow: auto;
    padding: 0 32px 12px;
}
.m-popup__content-main label {
    font-size: 13px !important;
    line-height: normal !important;
}
.content__employee-form {
    display: flex;
}
.employee-form__left {
    padding-right: 26px;
    width: calc(50% - 26px);
}
.employee-form__right {
    width: 50%;
}
.color-red {
    color: red;
}
.form-popup {
    display: flex;
    padding-bottom: 24px;
}
.form-group {
    display: flex;
    flex-direction: column;
    position: relative;
}
.form-group label {
    padding-bottom: 8px;
    font-weight: 700;
}
.form-group .error_text {
    position: absolute;
    top: calc(100% + 6px);
    color: red;
    width: 100%;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    font-weight: 400;
}
.ma-nhan-vien,
.ngay-sinh {
    width: 40%;
    padding-right: 10px;
}
.ngay-sinh {
    padding-right: 12px;
}
.ten-nhan-vien,
.gioi-tinh {
    width: 60%;
}
.don-vi,
.chuc-danh,
.noi-cap,
.dia-chi {
    width: 100%;
}
.don-vi .combobox input {
    border-width: 1px;
    border-radius: 4px;
    border-color: #bfbfbf;
    border-style: solid;
}
.don-vi .combobox .combobox__data {
    bottom: unset;
    top: calc(100% + 1px);
    z-index: 1;
}
.input-gioi-tinh {
    padding-right: 16px;
    width: 20px;
    height: 20px;
    accent-color: #50b83c;
}
.lable-gioi-tinh {
    padding-right: 16px;
    padding-left: 8px;
    font-weight: 400 !important;
}
.so-cmnd {
    width: 60%;
    padding-right: 10px;
}
.ngay-cap {
    width: 40%;
}
.content-employee__contact {
    width: 100%;
    border-bottom: 1px solid #bfbfbf;
}
.di-dong {
    width: calc(25% - 10px);
    padding-right: 10px;
}
/* End content */

/* Footer container */
.m-popup__footer {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 12px;
}
.m-popup__footer-left {
    display: flex;
}
/* End Footer */

/* overlay */
.overlay {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    cursor: auto;
}
</style>
