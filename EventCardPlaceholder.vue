<template>
  <nb-card>
    <nb-card-item cardBody>
      <placeholder-box
        width="100%"
        :height="200"
      />
    </nb-card-item>
    <nb-card-item>
      <placeholder-box
        width="50%"
        :height="20"
      />
    </nb-card-item>
    <nb-card-item>
      <placeholder-box
        width="95%"
        :height="50"
      />
    </nb-card-item>
  </nb-card>
</template>

<script>
import Placeholder from 'rn-placeholder'

export default {
  components: {
    'placeholder-box': Placeholder.Box
  }
}
</script>
