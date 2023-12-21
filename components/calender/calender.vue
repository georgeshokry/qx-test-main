<template>
    <div class="swiper">
        <div class="swiper-wrapper">
            <div v-for="(day, index) in dates" :id="'day-' + index" :key="index" class="swiper-slide"
                @click="chooseDate(day.fullDate)">
                <div class="day-item border-2 border-muted-btn rounded-2xl"
                    :class="{ 'day-item--active': activeSelectedDate(day.fullDate) }">
                    <div class="day-item__day" :class="{ 'day-item__day--active': activeSelectedDate(day.fullDate) }">
                        {{ day.dayName }}
                    </div>
                    <div class="day-item__number" :class="{ 'day-item__number--active': activeSelectedDate(day.fullDate) }">
                        {{ day.dayNumber }}
                    </div>
                </div>
            </div>
        </div>
        <div class="swiper-button-prev"></div>
        <div class="swiper-button-next"></div>
    </div>
</template>
  

<script>
import { Swiper, Navigation, Pagination, Autoplay } from 'swiper';
import moment from 'moment';
import 'swiper/swiper-bundle.min.css'
export default {
    data() {
        return {
            swiperRef: null,
            dates: [],
            selectedDate: ''
        }
    },
    watch: {
        "$i18n.locale": {
            handler(newVal) {
                this.startCalender(newVal)
                this.$nextTick(() => {// to resect the first day again after changing the lang
                    this.swiperRef.rtl = newVal === 'ar'
                    this.initSwiper()
                    document.getElementById('day-0').click()
                })
            }
        }
    },
    mounted() {
        this.startCalender(this.$i18n.locale)
        this.$nextTick(() => {
            this.initSwiper()
            this.selectedDate = moment(new Date).toLocaleString()
            document.getElementById('day-0').click()
        })
    },
    methods: {
        startCalender(lang) {
            moment.locale(lang)
            this.dates = []
            for (let index = 0; index < 7; index++) {
                const day = moment().add(index, 'days');

                this.dates.push({
                    dayNumber: day.format('D'),
                    dayName: day.format('ddd'),
                    id: day.day(),
                    fullDate: day.toLocaleString()
                })
            }
        },
        initSwiper() {
            Swiper.use([Navigation, Pagination, Autoplay])

            this.swiperRef = new Swiper('.swiper', {
                direction: 'horizontal',
                loop: false,
                modules: [Navigation, Pagination, Autoplay],
                pagination: {
                    el: '.swiper-pagination',
                    type: 'bullets',
                    clickable: false
                },
                navigation: {
                    nextEl: '.swiper-button-next',
                    prevEl: '.swiper-button-prev'
                },
                slidesPerView: 3,
                spaceBetween: 1,
                setWrapperSize: true,
                rtl: this.$i18n.locale === 'ar'

            })
        },
        chooseDate(date) {
            this.selectedDate = date
            this.$emit('choose-date', date)
        },
        activeSelectedDate(date) {
            return this.selectedDate === date
        }
    }
}
</script>

<style lang="scss" scoped>
.swiper-button-next:after,
.swiper-button-prev:after {
    font-size: 15px;
    color: var(--text-base);
}

.swiper {
    height: 100px;
    overflow: hidden;
    position: relative;
    width: 100%;
}

.swiper-slide {
    align-items: center;
    display: flex;
    justify-content: center;
}

.swiper-button-next,
.swiper-container-rtl .swiper-button-prev {
    right: -8px;
    left: auto;
    position: absolute;
}

.swiper-button-prev,
.swiper-container-rtl .swiper-button-next {
    left: -8px;
    right: auto;
    position: absolute;
}
</style>
