<template>
  <div class="comment-reply">
    <!-- 导航栏 -->
    <van-nav-bar :title="comment.reply_count > '0' ? `${comment.reply_count}条回复` : '暂无回复'">
      <van-icon slot="left" name="cross" @click="$emit('close')" />
    </van-nav-bar>
    <div class="scroll-wrap">
      <!-- 当前评论项 -->
      <comment-item :comment="comment" />

      <!-- 评论回复列表 -->
      <van-cell title="全部回复"></van-cell>
      <comment-list :list="commentList" :artid="comment.com_id" type="c"></comment-list>
    </div>
    <!-- 底部发布评论 -->
    <div class="post-wrap">
      <van-button class="post-btn" size="small" round @click="isPostShow = true">写评论</van-button>
    </div>

    <!-- 发布评论 -->
    <van-popup v-model="isPostShow" position="bottom">
      <comment-post :artid="comment.com_id" @post-success="onPostSuccess" type="a"></comment-post>
    </van-popup>
  </div>
</template>

<script>
import CommentItem from './comment-item'
import CommentList from './comment-list'
import CommentPost from './comment-post'
export default {
  name: 'CommentReply',
  components: {
    CommentItem,
    CommentList,
    CommentPost
  },
  data () {
    return {
      isPostShow: false,
      commentList: []
    }
  },
  created () {
  },
  mounted () {
  },
  methods: {
    onPostSuccess (data) {
      this.comment.reply_count++
      this.isPostShow = false
      this.commentList.unshift(data.new_obj)
    }
  },
  watch: {
  },
  computed: {
  },
  props: {
    comment: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped lang="less">
.scroll-wrap {
  position: fixed;
  top: 220px;
  left: 0;
  right: 0;
  bottom: 88px;
  overflow-y: auto;
}

.post-wrap {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 88px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #fff;
  border-top: 1px solid #d8d8d8;
  .post-btn {
    width: 60%;
  }
}
</style>
