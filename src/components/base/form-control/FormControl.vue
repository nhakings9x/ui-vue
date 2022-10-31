<template>
    <div class="form-group">
        <label for=""
            >{{ labelForm }}
            <span class="color-red" v-if="required">*</span></label
        >
        <ms-input
            inputInfo
            :inputError="validateForm"
            @dataInput="inputValue"
            :name="formControlName"
        ></ms-input>
        <label for="" class="error_text" v-if="validateForm">{{
            errorText
        }}</label>
    </div>
</template>
<script>
import MsInput from "../input/MsInput.vue";
export default {
    components: { MsInput },
    props: {
        labelForm: {
            type: String,
            default: "Lable",
        },
        required: {
            type: Boolean,
            default: false,
        },
        validateForm: {
            type: Boolean,
        },
        errorText: {
            type: String,
            default: "Ô này không được để trống",
        },
        formControlName: {
            type: String,
        },
    },
    methods: {
        inputValue(data) {
            this.$emit("dataInput", data);
        },
    },
};
</script>
<style>
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
    top: calc(100% + 4px) !important;
    color: red;
    width: 100%;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
    font-weight: 400;
}
</style>
