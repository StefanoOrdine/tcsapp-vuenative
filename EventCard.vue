<template>
  <nb-card>
    <nb-card-item cardBody>
      <placeholder-box
        width="100%"
        :height="200"
        :onReady="isReady"
      >
        <image
          :source="{ uri: imageUrl }"
          :style="{ height: 200, width: null, flex: 1 }"
        />
      </placeholder-box>
    </nb-card-item>
    <nb-card-item>
      <html-view :value="title" />
    </nb-card-item>
    <nb-card-item>
      <html-view :value="getTruncatedText(text)" />
    </nb-card-item>
  </nb-card>
</template>

<script>
import axios from 'axios'
import { truncate } from 'lodash'
import HTMLView from 'react-native-htmlview';
import Placeholder from 'rn-placeholder';

export default {
  components: {
    HTMLView,
    'placeholder-box': Placeholder.Box
  },
  created: function () {
    axios
      .get(this.imageUri)
      .then(({ data: { guid: { rendered } } }) => { this.imageUrl = rendered; this.isReady = true })
      .catch(console.log)
  },
  props: ['title', 'text', 'imageUri'],
  data: function () {
    return {
      imageUrl: null,
      isReady: false
    }
  },
  methods: {
    getTruncatedText (text) {
      return truncate(text, { length: 150 });
    }
  }
}
</script>
