<template>
  <div class="container mx-auto px-4 pt-16">
    <strong>MENTORS</strong>
    <br />
    <br />
    <hr />
    <br />
    <p>
      On this page you can find active mentors in the optiMize community. These
      mentors have agreed to list their information for the optiMize community
      so please be mindful of sharing this information. You can use the search
      bar and filters below to find mentors.
    </p>
    <br />
    <div class="flex items-center border-b border-b-2  py-2">
      <input
        v-model="search"
        class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none"
        type="text"
        placeholder="Search mentor by name"
      />
    </div>
    <hr />
    <div class="cardWrapper">
      <ProfileCard
        v-for="mentor in filteredMentors"
        :key="mentor.mentorId"
        :mentor="mentor"
      />
    </div>
  </div>
</template>

<!-- todo: add script tags, load mentor picker component --->
<script>
import ProfileCard from '../components/ProfileCard'
import mentorsList from '../assets/mentors.json'

export default {
  components: { ProfileCard },
  data() {
    return {
      mentors: [],
      search: ''
    }
  },
  computed: {
    filteredMentors() {
      const searchString = this.search.toUpperCase()
      return this.mentors.filter((mentor) => {
        const mentorFirstName = mentor.firstName.toUpperCase().concat(' ')
        const mentorFullName = mentorFirstName.concat(
          mentor.lastName.toUpperCase()
        )
        return mentorFullName.match(searchString)
      })
    }
  },
  created() {
    this.mentors = mentorsList
  }
  /*
  mounted() {
    this.$axios
      .get(`https://p5mq2fkwwb.execute-api.us-east-2.amazonaws.com/v1/mentors`)
      .then((response) => (this.info = response.body))
      .catch((error) => {
        console.log(error)
        this.errored = true
      })
      .finally(() => (this.loading = false))
  }
  */
}
</script>

<style>
.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
