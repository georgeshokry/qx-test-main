<template>
    <div class="flex justify-between items-center">
        <div>
            <p class="text-2xl font-bold">{{ $t('upcoming-sessions') }}</p>
            <p class="text-lg">{{ localizeSelectedDate }}</p>
        </div>
        <div>
            <img src="~/assets/svg/add.svg" alt="add" />
        </div>
    </div>
</template>

<script>
import moment from 'moment';
export default {
    props: {
        selectedDate: {
            type: String,
            default: '',
            required: true
        }
    },
    data() {
        return {

        }
    },
    computed: {
        localizeSelectedDate() {
            moment.locale(this.$i18n.locale)
            if (!this.selectedDate) {
                return moment().format('dddd, MMMM D, YYYY')
            }
            return moment(new Date(this.selectedDate)).format('dddd, MMMM D, YYYY')
        }
    }

}
</script>