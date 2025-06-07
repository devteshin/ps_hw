<script setup>
import FailIcon from './icons/FailIcon.vue';
import SuccessIcon from './icons/SuccessIcon.vue';
import StatusSuccessIcon from './icons/StatusSuccessIcon.vue';
import StatusFailIcon from './icons/StatusFailIcon.vue';

const emit = defineEmits({
    turnCard: null,
    changeStatusCard: null
});

function turn() {
    emit('turnCard')
}

function changeStatus() {
    emit('changeStatusCard')
}

const cardData = defineProps({
    word: String,
    translation: String,
    state: String,
    status: String,
})


</script>

<template>
    <div class="card">
        <div class="card-border" @click.self="turn">
            <div class="inner-border" @click.self="turn">
                <div class="card-number">06</div>
                <div class="card-status-success-icon" v-if="status==='success'"><StatusSuccessIcon /></div>
                <div class="card-status-fail-icon" v-else-if="status==='fail'"><StatusFailIcon /></div>
                <div class="card-word"  v-if="state==='closed'" @click="turn">{{cardData.word}}</div>
                <div class="card-word"  v-else @click="turn">{{cardData.translation}}</div>
                <div class="card-status" @click="changeStatus" v-show="state==='closed'">ПЕРЕВЕРНУТЬ</div>
                <div class="card-status" @click="changeStatus" v-show="state==='opened' & status==='pending'">
                    <FailIcon />
                    <SuccessIcon />
                </div>
                <div class="card-status" @click="changeStatus" v-show="state==='opened' & status!=='pending'">ЗАВЕРШЕНО</div>
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
        display: flex;
        justify-content: center;
        gap: 32px;
    }

    .card-status-success-icon {
        position: absolute;
        top: -13px; left: 90px;
    }
    .card-status-fail-icon {
        position: absolute;
        top: -24px; left: 82px;
    }

</style>