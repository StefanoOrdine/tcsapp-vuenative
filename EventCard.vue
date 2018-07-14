<template>
  <nb-card>
    <nb-card-item cardBody>
      <image
        :source="{ uri: imageUrl }"
        :style="{ height: 200, width: null, flex: 1 }"
      />
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

export default {
  components: {
    HTMLView
  },
  created: function () {
    axios
      .get(this.imageUri)
      .then(({ data: { guid: { rendered } } }) => { this.imageUrl = rendered })
      .catch(console.log)
  },
  props: ['title', 'text', 'imageUri'],
  data: function () {
    return {
      imageUrl: 'iVBORw0KGgoAAAANSUhEUgAAASwAAACkCAQAAACH4Nv/AAABM0lEQVR42u3SMQ0AAAzDsJU/6aHoUcmGECUHBZEAY2EsjAXGwlgYC4yFsTAWGAtjYSwwFsbCWGAsjIWxwFgYC2OBsTAWxgJjYSyMBcbCWBgLjIWxMBYYC2NhLDAWxsJYYCyMhbHAWBgLY4GxMBbGAmNhLIwFxsJYGAuMhbEwFhgLY2EsMBbGwlhgLIyFscBYGAtjgbEwFsYCY2EsjAXGwlgYC4yFsTAWGAtjYSwwFsbCWBgLjIWxMBYYC2NhLDAWxsJYYCyMhbHAWBgLY4GxMBbGAmNhLIwFxsJYGAuMhbEwFhgLY2EsMBbGwlhgLIyFscBYGAtjgbEwFsYCY2EsjAXGwlgYC4yFsTAWGAtjYSwwFsbCWGAsjIWxwFgYC2OBsTAWxgJjYSyMBcbCWBgLjIWxWPScIQClvSO/qwAAAABJRU5ErkJggg=='
    }
  },
  methods: {
    getTruncatedText (text) {
      return truncate(text, { length: 150 });
    }
  }
}
</script>
