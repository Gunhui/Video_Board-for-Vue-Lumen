<template>
    <div :style="{ 'margin-left': offset + 'px' }" class="comment">
        <span><b>Anonymous</b> - {{timestamp}}</span>
        <p>{{comment.body}}</p>
        <a v-if="!isReplying" @click="isReplying = true">Reply</a>
        <reply-comment @commentPosted="isReplying = false" :parent="comment.id" :post="comment.post_id" v-if="isReplying"></reply-comment>
    </div>
</template>

<script>
import ReplyComment from "./ReplyComment";

export default {
  name: "comment",
  props: ["comment", "offset"],
  components: {
    ReplyComment
  },
  data() {
    return {
      isReplying: false
    };
  },
  computed: {
    timestamp() {
      return moment.utc(this.comment.created_at).fromNow();
    }
  }
};
</script>

<style lang="scss" scoped>
p {
  white-space: pre-wrap;
}
.columns {
  margin-top: 0;
}
</style>
