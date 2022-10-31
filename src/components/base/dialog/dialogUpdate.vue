<template>
    <div class="m-notification">
        <div class="m-noti-box">
            <div class="box-content">
                <div class="content">
                    <div class="icon-message"></div>
                    <div class="message-content pt-12">
                        Dữ liệu đã bị thay đổi. Bạn có muốn cất không?
                    </div>
                </div>
                <div class="content-footer">
                    <button class="m-btn m-btn-extra">Hủy</button>
                    <div class="content-footer-left">
                        <button class="m-btn m-btn-extra mr-8">Không</button>
                        <button class="m-btn">Có</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {};
</script>
<style scoped>
.m-notification {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.2);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 2;
}
.m-noti-box {
    width: 444px;
    min-width: 444px;
    height: 183px;
    background-color: #fff;
    border-radius: 4px;
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
