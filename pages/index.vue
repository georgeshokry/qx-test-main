<template>
  <div class="container mx-auto flex flex-wrap">
    <div class="h-full p-4 w-full lg:w-1/3 sm:w-1/2">
      <CalenderHeader :selected-date="selectedDate" />
    </div>
    <div class="h-full w-full lg:w-1/3 sm:w-1/2">
      <calender @choose-date="chooseDate" />
    </div>
    <div class="h-full p-4 w-full lg:w-1/3 sm:w-1/2">
      <Sessions :sessions-list="filteredSession" @remove-session="removeSession" />
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import calender from "~/components/calender/calender"
import CalenderHeader from "~/components/header/CalenderHeader"
import Sessions from "~/components/sessions/Sessions"
export default {
  components: {
    calender,
    CalenderHeader,
    Sessions
  },
  props: {},
  data() {
    return {
      sessions: [
        {
          company_name: 'Baraka (YC S21)',
          company_logo:
            'https://upload.wikimedia.org/wikipedia/en/thumb/d/d3/Starbucks_Corporation_Logo_2011.svg/640px-Starbucks_Corporation_Logo_2011.svg.png',
          company_description: 'Investing. Empowered.',
          start_date: '2023-12-21 11:00:06',
          end_date: '2023-12-21 11:30:06',

          zoom_link: 'https://zoom.us/j/1234567890?pwd=1234567890',
          id: '12562'
        },
        {
          company_name: 'Memorisely',
          company_logo:
            'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSi16u9yD2j4H1UhDIEcw6JxbNjBvShnDRL6_-17iNKjiXbQgFQpM0yQzPa7SDNLU3JeVs&usqp=CAU',
          company_description: 'E-Learning',
          start_date: '2023-12-21 11:00:06',
          end_date: '2023-12-21 11:30:06',
          zoom_link: 'https://zoom.us/j/1234567890?pwd=1234567890',
          id: '9851651'
        },
        {
          company_name: 'Memorisely',
          company_logo:
            'https://img.freepik.com/premium-vector/saudi-arabia-tour-travel-logo-umrah-hajj-company-icon_18099-3718.jpg',
          company_description: 'The Evolution of A Revolution',
          start_date: '2023-12-23 11:00:06',
          end_date: '2023-12-23 11:30:06',
          zoom_link: 'https://zoom.us/j/1234567890?pwd=1234567890',
          id: '89513212'
        },
        {
          company_name: 'Swvl',
          company_logo:
            'https://miro.medium.com/max/936/1*dn6zull3VcGzGMVDdjYItA.jpeg',
          company_description: 'الشوبنغ لعبتنا - Shopping is our thing',
          start_date: '2023-12-23 11:00:06',
          end_date: '2023-12-23 11:30:06',
          zoom_link: 'https://zoom.us/j/1234567890?pwd=1234567890',
          id: '898453'
        },
        {
          company_name: 'Basket باسكت',
          company_logo:
            'https://cdn2.hubspot.net/hub/145335/file-407359001-png/blog-files/pepsi.png',
          company_description:
            'Lorem ipsum dolor sit amet consectetur adipisicing elit. Quisquam, quod.',
          start_date: '2023-12-23 11:00:06',
          end_date: '2023-12-23 11:30:06',
          zoom_link: 'https://zoom.us/j/1234567890?pwd=1234567890',
          id: '89559889'
        },
      ],
      selectedDate: '',
      filteredSession: []
    }
  },
  head: {},
  computed: {},
  watch: {},
  mounted() { },
  methods: {
    chooseDate(dateChosen) {
      this.selectedDate = dateChosen
      this.filterSessionsByDate()
    },
    filterSessionsByDate() {
      this.filteredSession = this.sessions.filter((session) => {
        return moment(new Date(session.start_date)).day() === moment(new Date(this.selectedDate)).day()
      })
    },
    removeSession(sessionId) {
      this.filteredSession = this.filteredSession.filter((session) => {
        return session.id !== sessionId
      })
    }
  },
}
</script>
