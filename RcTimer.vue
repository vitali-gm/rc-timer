<template>
    <div class="timer">
        <div>
            <div class="timer__number">{{ timer.days }}</div>
            <div v-if="!noTitles" class="timer__text">
                {{ declensionDate(timer.days, ['День', 'Дня', 'Дней']) }}
            </div>
        </div>

        <div class="timer__separator">:</div>

        <div>
            <div class="timer__number">{{ timer.hours }}</div>
            <div v-if="!noTitles" class="timer__text">
                {{ declensionDate(timer.hours, ['Час', 'Часа', 'Часов']) }}
            </div>
        </div>

        <div class="timer__separator">:</div>

        <div class="timer__text">
            <div class="timer__number">{{ timer.minutes }}</div>
            <div v-if="!noTitles" class="timer__text">
                {{ declensionDate(timer.minutes, ['Минута', 'Минуты', 'Минут']) }}
            </div>
        </div>

        <div class="timer__separator">:</div>

        <div>
            <div class="timer__number">{{ timer.seconds }}</div>
            <div v-if="!noTitles" class="timer__text">
                {{ declensionDate(timer.seconds, ['Секунда', 'Секунды', 'Секунд']) }}
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: 'RcTimer',

        props: {
            expire: {
                type: String,
                default: '2020-05-02 23:59:59',
            },

            noTitles: {
                type: Boolean,
                default: false,
            },

            noZero: {
                type: Boolean,
                default: false,
            },
        },

        data: () => ({
            date: new Date(),
        }),

        computed: {
            timer: function () {
                let timer = {
                    days: 0,
                    hours: 0,
                    minutes: 0,
                    seconds: 0,
                }
                const t = Date.parse(this.expire) - Date.parse(this.date)
                if (t >= 0) {
                    const seconds = Math.floor((t / 1000) % 60)
                    const minutes = Math.floor((t / 1000 / 60) % 60)
                    const hours = Math.floor((t / (1000 * 60 * 60)) % 24)
                    const days = Math.floor(t / (1000 * 60 * 60 * 24))

                    timer = {
                        days: days,
                        hours: hours,
                        minutes: minutes,
                        seconds: seconds,
                    }
                }

                return this.noZero ? timer : this.transform(timer)
            },
        },

        methods: {
            declensionDate(number, titles) {
                const cases = [2, 0, 1, 1, 1, 2]
                return titles[
                    number % 100 > 4 && number % 100 < 20
                        ? 2
                        : cases[number % 10 < 5 ? number % 10 : 5]
                    ]
            },

            transform(props) {
                Object.entries(props).forEach(([key, value]) => {
                    props[key] = value < 10 ? `0${value}` : value
                })

                return props
            },
        },

        created() {
            setInterval(() => {
                this.date = new Date()
            }, 1000)
        },
    }
</script>

<style lang="stylus" scoped>
    .timer
        display inline-flex

        &__number
        &__separator
            font-size 23px
            font-weight bold
            line-height 27px
            letter-spacing -.43px
            text-align center

        &__separator
            margin 0 6px

        &__text
            text-transform uppercase
            font-size 10px
            line-height 18px
            text-align center
</style>
