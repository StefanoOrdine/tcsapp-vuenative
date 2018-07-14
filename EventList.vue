<template>
  <view>
    <event-card v-for="event in eventList" :key="event.id"
      :title="event.title.rendered"
      :text="event.content.rendered"
      :imageUri="event._links['wp:featuredmedia'][0].href"
    />
  </view>
</template>

<script>
import axios from 'axios'

import EventCard from './EventCard'

export default {
  components: { EventCard },
  created: function () {
    axios
      .get('https://torinocodingsociety.it/wp-json/wp/v2/events')
      .then(({ data }) => this.eventList = data)
  },
  data: function() {
    return { eventList: [] }
  },
  methods: {}
}
</script>
