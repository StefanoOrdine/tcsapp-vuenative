<template>
  <view>
    <event-card-placeholder
      v-for="event in eventList"
      :key="event.id"
      :onReady="isReady"
    >
      <event-card
        :title="getTitle(event)"
        :text="getText(event)"
        :imageUri="getImageHref(event)"
      />
    </event-card-placeholder>
  </view>
</template>

<script>
import axios from 'axios'
import { get } from 'lodash'
import Placeholder from 'rn-placeholder';

import EventCard from './EventCard'
import EventCardPlaceholder from './EventCardPlaceholder'

export default {
  components: {
    EventCard,
    EventCardPlaceholder: Placeholder.connect(EventCardPlaceholder),
    'placeholder-box': Placeholder.Box
  },
  created: function () {
    axios
      .get('https://torinocodingsociety.it/wp-json/wp/v2/events')
      .then(({ data }) => { this.eventList = data; this.isReady = true })
  },
  data: function() {
    return {
      eventList: Array(5).fill().map((_, id) => ({ id })),
      isReady: false
    }
  },
  methods: {
    getImageHref (event) {
      return get(event, '_links.wp:featuredmedia.0.href')
    },
    getTitle (event) {
      return get(event, 'title.rendered')
    },
    getText (event) {
      return get(event, 'content.rendered')
    }
  }
}
</script>
