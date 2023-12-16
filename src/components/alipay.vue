<template>
    <div>
        <div class="pic" ref="root">
            <canvas id="canvas" ref="canvas" width="500" height="1120">浏览器不支持canvas</canvas>
            <canvas id="amount" ref="amount" width="500" height="170">浏览器不支持canvas</canvas>
        </div>
    </div>
</template>
<script setup>
import { onMounted, ref, defineProps, watch, defineExpose } from 'vue'
import html2canvas from 'html2canvas'

const props = defineProps({
    info: {
        type: Number,
        default: 0
    },
    user: {
        type: String,
        default: `可爱土豆泥`
    }
})
const canvas = ref()
const amount = ref()
const root = ref()

onMounted(() => {
    initCanvas()
    drawAmount()
})

watch(props, () => {
    drawAmount()
})

function initCanvas() {
    const ctx = canvas.value.getContext('2d')
    const img = new Image()
    img.src = 'alipay.jpg'
    img.onload = function () {
        ctx.drawImage(img, 0, 0, img.width / 2.88, img.height / 2.88)
    }
}

function drawAmount() {
    const ctx = amount.value.getContext('2d')
    // 清空画布
    ctx.clearRect(0, 0, amount.value.width, amount.value.height);
    const price = `￥${props.info.toFixed(2)}`
    ctx.font = 'bold 60px Arial'
    ctx.fillStyle = '#fff'
    let x = (amount.value.width - ctx.measureText(price).width) / 2;
    ctx.fillText(price, x, 60)
    // 交易用户
    const user = `${props.user}`
    ctx.font = '500 17px STHeiti'
    ctx.fillText(user, 30, 120)
    // 交易金额
    x = (amount.value.width - ctx.measureText(price).width) - 30;
    ctx.fillText(price, x, 120)
}

// 保存到图片
function saveToFile() {
    html2canvas(root.value).then(function (canvas) {
        var img = canvas.toDataURL('image/png');
        var a = document.createElement('a');
        a.href = img;
        a.download = 'myDiv.png';
        a.click();
    });
}

defineExpose({
    saveToFile
})
</script>

<style scoped>
.pic {
    width: 500px;
}

#amount {
    position: absolute;
    top: 160px;
    left: 50%;
    z-index: 1;
}
</style>