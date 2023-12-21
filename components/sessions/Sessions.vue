<template>
    <div>
        <div v-if="sessionsList.length > 0">
            <div v-for="(session, index) in sessionsList" :key="index"
                class="p-2 mb-3 border-2 border-muted-btn rounded-xl justify-center">
                <div class="cursor-pointer">
                    <div class="flex flex-row gap-3">
                        <div class="basis-1/6">
                            <img width="50px" height="60px" class="border-2 border-muted-btn rounded-xl"
                                :src="session.company_logo" :alt="session.company_name">
                        </div>
                        <div>
                            <h3 class="text-xl font-bold">{{ session.company_name }}</h3>
                            <h6 class="text-lg">{{ session.company_description }}</h6>
                        </div>
                    </div>
                    <div class="flex">
                        <p class="text-c-b-gray-dark pt-2">
                            <span class="text-3xl">→</span>
                            {{ startEndTime(session.start_date) }} {{ $t('to') }} {{ startEndTime(session.end_date) }}
                        </p>
                    </div>
                    <div class="pt-3">
                        <button class="p-3 px-4 rounded-xl bg-active text-white"
                            style="background: var(--border-secondary);" @click="joinSession(session.id)">
                            {{ $t('join') }}
                        </button>
                        <button class="p-3 px-4 rounded-xl" @click="removeSession(session.id)">
                            {{ $t('dismiss') }}
                        </button>
                    </div>
                </div>
            </div>
        </div>
        <div v-else class="p-2 mb-3 border-2 border-muted-btn rounded-xl block justify-center items-center">
            <img width="400px" height="550px" src="~/assets/svg/music.svg" alt="no-sessions" />
            <div class="text-center">
                <p class="text-xl px-3">
                    {{ $t('no-sessions') }}
                    <span class='font-bold'>{{ $t('upcoming') }}</span>
                    {{ $t('no-sessions-second') }}
                </p>
            </div>
        </div>

    </div>
</template>

<script>
import moment from 'moment';
export default {
    props: {
        sessionsList: {
            type: Array,
            default() {
                return []
            },
            require: true
        }
    },
    methods: {
        startEndTime(timestamp) {
            moment.locale(this.$i18n.locale)
            return moment(new Date(timestamp)).format('h:mm a')
        },
        joinSession(sessionId) {
            window.open('https://zoom.us/', '_blank')
        },
        removeSession(sessionId) {
            this.$emit('remove-session', sessionId)
        }
    }
}
</script>