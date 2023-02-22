<template>
    <div class="timer font-bold text-yellow-300 "  style="font-size: 14rem;" >{{ time }}</div>
</template>
<script >
export default {
    props:['time'],
    computed:{
        time () {

            let time = this.time / 60
            let minutes = parseInt(time)
            let secondes = Math.round((time - minutes) * 60)
            if (minutes < 10) {
                minutes = "0" + minutes
            }
            if (secondes < 10) {
                secondes = "0" +secondes
            }
            return minutes+":"+secondes
        }
    },
}


</script>

