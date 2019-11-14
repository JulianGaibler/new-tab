<template>
    <div id="app" class="dark">
        <div class="time">
            <span>{{time[0]}}</span>
            <span>{{time[1]}}</span>
            <span>{{time[2]}}</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'app',
    data() {
        return {
            time: [0,0,0]
        }
    },
    created() {
        this.updateCurrentTime()
        setInterval(this.updateCurrentTime, 500)
        window.addEventListener("keypress", e => {
            if (e.keyCode === 44) {
                document.body.classList.toggle('dark')
            }
        });
    },
    methods: {
        updateCurrentTime() {
            let date = new Date()
            let arr = new Array(3)
            arr[0] = date.getHours().toString().padStart(2, '0')
            arr[1] = date.getMinutes().toString().padStart(2, '0')
            arr[2] = date.getSeconds().toString().padStart(2, '0')
            this.time = arr
        }
    },
}
</script>

<style lang="stylus">

// @font-face
//     font-family 'CustomFont'
//     font-style normal
//     src local('CustomFont') url('~@/assets/CustomFont.ttf') format('truetype')

html, body
    height 100%
    margin 0
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
body
    font-size 16px
    font-family 'Arial-Black', sans-serif
    user-drag none
    background #000000
    -webkit-user-drag none
    -webkit-tap-highlight-color transparent
    -webkit-touch-callout none
    -webkit-user-select none
    outline none
    user-select none
    overflow hidden
    transition-duration .5s
    transition-property background-color
#app
    height 100%
    display flex
    flex-direction column
    background #0f0f10
    justify-content center
    align-items center
    animation well-animation 1s cubic-bezier(.1, .82, .25, 1)
    .time
        display inline-block
        font-size 6rem
        color transparent
        -webkit-text-stroke-width 1.5px
        -webkit-text-stroke-color #ff617b
        text-shadow 0 0 2.5rem rgba(233, 32, 66, 0.4)
        > span
            font-variant-numeric tabular-nums
            letter-spacing 0.1rem
            &:not(:last-child)
                margin-right 1.5rem
body.dark
    #app
        background #000000
        .time
            margin-right 1.5rem
            -webkit-text-stroke-color #060606
            text-shadow unset


@keyframes well-animation {
    0%, 20% {
        transform scale(1.2)
        opacity 0
    }
    100% {
        transform scale(1)
        opacity 1
    }
}
</style>
