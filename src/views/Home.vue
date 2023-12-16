<template>
    <div class="home">
        <div class="left">
            金额：<input type="number" v-model="Amount" />
            收款人：<input type="text" v-model="user" />
            <button @click="saveToFile">保存</button>
        </div>
        <div class="right">
            <Alipay :info="Amount" :user="user" ref="pic" />
        </div>
    </div>
</template>

<script setup>
import Alipay from '@/components/alipay.vue'
import { ref } from 'vue'
const Amount = ref(100)
const user = ref('可爱土豆泥')
const pic = ref()

function saveToFile() {
    pic.value.saveToFile()
}
</script>

<style scoped>
.home {
    display: flex;
    justify-content: space-between;
    width: 100%;
}

.left {
    width: 50%;
}

.right {
    width: 50%;
}
</style>