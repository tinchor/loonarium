<template>
  <div class="comment-composer">
    <textarea
      class="composer-textarea"
      v-model="commentText"
      rows="5"
      placeholder="Enter something insightful about what's on screen right now!"
    />
    <br/>
    <button
      class="btn composer-button"
      @click="submitComment"
    >Post at ~{{elapsedTime}}</button>
  </div>
</template>

<script>
export default {
  name: 'comment-composer',
  props: {
    elapsedSeconds: {
      type: Number,
      default: 0.0
    },
  },
  computed: {
    elapsedTime () {
      const totalSeconds = Math.floor(this.elapsedSeconds)
      let minutes = Math.floor(totalSeconds / 60)
      let seconds = totalSeconds % 60
      if (minutes < 10) minutes = '0' + minutes
      if (seconds < 10) seconds = '0' + seconds
      return `${minutes}:${seconds}`
    }
  },
  data () {
    return {
      commentText: ''
    }
  },
  methods: {
    clearTextAreaFn () {
      this.commentText = '' 
      console.log('???')
    },
    submitComment () {
      this.$emit('post', {
        time: this.elapsedSeconds,
        text: this.commentText,
        clearTextAreaFn: this.clearTextAreaFn
      })
    }
  }
}
</script>

<style lang="scss">
.comment-composer {
  color: black;
}

.composer-textarea {
  width: 100%;
}

.composer-button {
  font-size: 14px;
}
</style>
