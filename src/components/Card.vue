<script setup>

const emit = defineEmits({
    turnCard(payload) {
        return payload;
    },
    changeStatusCard(payload) {
        return payload;
    },
});

function turn() {
    emit('turnCard')
}

function changeStatus() {
    emit('changeStatusCard')
}

</script>

<template>
    <div class="card">
        <div class="card-border">
            <div class="inner-border">
                <div class="card-number">06</div>
                <div class="card-word">Unadmited</div>
                <div class="card-status">ПЕРЕВЕРНУТЬ</div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .card {
        width: 250px;
        height: 376px;
        box-shadow: 10px 10px 10px 0px #0000000D;
        font-family: Roboto;
        position: relative;
    }

    .card-border {
        background: #FFFFFF;
        width: 250px;
        height: 376px;
        border-radius: 16px;
        box-shadow: 0px 0px 16px 0px #0000001A;
    }

    .inner-border {
        position: absolute;
        top: 28px; left: 19px;
        width: 212px;
        height: 320px;
        border-radius: 12px;
        border-width: 1px;
        background: #FFFFFF;
        border: 1px solid #CCE8FF
    }

    .card-word {
        position: absolute;
        top: 149px; left: 16px;
        width: 180px;
        height: 21px;
        font-weight: 400;
        font-size: 18px;
        line-height: 100%;
        letter-spacing: 0%;
        text-align: center;
        color: #000000;
    }

    .card-number {
        position: absolute;
        top: -8px; left: 16px;
        width: 16px;
        height: 16px;
        gap: 10px;
        font-family: Roboto;
        font-weight: 400;
        font-size: 14px;
        line-height: 100%;
        letter-spacing: 0%;
        text-align: center;
        color: #000000;
        background: #FFFFFF;
    }

    .card-status {
        position: absolute;
        top: 311px; left: 61px;
        padding-right: 4px;
        padding-left: 4px;
        width: 97px;
        height: 18px;
        font-weight: 700;
        font-size: 12px;
        line-height: 18px;
        text-align: center;
        color: #222222;
        background: #FFFFFF;
        
    }

</style>