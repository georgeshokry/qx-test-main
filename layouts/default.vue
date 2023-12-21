<template>
  <div>
    <client-only>
      <div class="justify container mx-auto flex flex-col items-center gap-[40px] pt-[100px]">
        <div class=" w-fit cursor-pointer rounded-[8px] bg-[#000] py-[6px] px-[11px] text-inverted hover:brightness-125"
          @click="changeLanguage">
          {{ $t('language') }}
        </div>
        <div class="container" :dir="lang === 'en' ? 'ltr' : 'rtl'">
          <Nuxt />
        </div>
      </div>
    </client-only>
  </div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
      lang: this.$i18n.fallbackLocale,
    }
  },
  head: {},
  computed: {},
  watch: {},
  mounted() { this.setUserLang() },
  methods: {
    changeLanguage() {
      if (this.lang === 'ar') {
        this.lang = 'en'
        this.$i18n.locale = 'en'
      } else {
        this.lang = 'ar'
        this.$i18n.locale = 'ar'
      }
      localStorage.setItem('user-lang', this.$i18n.locale)
    },
    setUserLang() {
      if (localStorage.getItem('user-lang')) {
        this.lang = localStorage.getItem('user-lang')
      } else {
        localStorage.setItem('user-lang', this.$i18n.fallbackLocale)
      }
      this.$i18n.locale = this.lang
    }
  },
}
</script>
