<template>
  <div id="app">
    <div class="comments-outside">
      <div class="comments-header">
        <div class="comments-stats">
            <span><i class="fa fa-thumbs-up"></i> {{ likes }}</span>
            <span><i class="fa fa-comment"></i> {{ comments.length }}</span>
          <span> </span>
          </div>
          <div class="post-owner">
            <div class="avatar">
              <img :src="creator.avatar" alt="">
            </div>
            <div class="username">
              <a href="#">@{{ creator.user }}</a>
            </div>

          </div>
        </div>
        <comments 
          :comments_wrapper_classes="['custom-scrollbar', 'comments-wrapper']"
          :comments="comments"
          :current_user="current_user"
          @submit-comment="submitComment"
        ></comments>

    </div>

  </div>
</template>

<script>
import Comments from './components/Comments.vue'

export default {
  name: 'app',
  components: {
    Comments
  },
  data() {
    return {
      likes: 15,
      creator: {
        avatar: 'http://via.placeholder.com/100x100/a74848',
        user: 'exampleCreator'
      },
      current_user: {
        avatar: 'http://via.placeholder.com/100x100/a74848',
        user: 'exampler'
      },
      comments: [
        {
          id: 1,
          user: 'example',
          avatar: 'http://via.placeholder.com/100x100/a74848',
          text: 'lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor lorem ipsum dolor ',
          date: '',
        },


      ]
    }
  },
  created() {
    if(localStorage.getItem('comments'))
      this.comments = JSON.parse(localStorage.getItem('comments'));
  },
  methods: {
    submitComment: function(reply) {
        var date = new Date();
        var h = date.getHours();
        var m = date.getMinutes();
        var x = h >= 12 ? 'pm' : 'am';
        h = h % 12;
        h = h ? h : 12;
        m = m < 10 ? '0'+m: m;
        var mytime= h + ':' + m + ' ' + x;

      this.comments.push({
        id: this.comments.length + 1,
        user: this.current_user.user,
        avatar: this.current_user.avatar,
        text: reply,
        date: mytime
      });
      localStorage.setItem('comments', JSON.stringify(this.comments));
    },
      timeFormat: function(date) {

          return mytime;
      }
  }



}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

a {
  text-decoration: none;
}

hr {
  display: block;
  height: 1px;
  border: 0;
  border-top: 1px solid #ececec;
  margin: 1em 0;
  padding: 0;
}

.comments-outside {
  box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.3);
  margin: 0 auto;
  max-width: 600px;
}

.comments-header {
  background-color: #C8C8C8;
  padding: 10px;
  align-items: center;
  display: flex;
  justify-content: space-between;
  color: #333;
  min-height: 80px;
  font-size: 20px;
}

.comments-header .comments-stats span {
  margin-left: 10px;
}

.post-owner {
  display: flex;
  align-items: center;
}

.post-owner .avatar > img {
  width: 30px;
  height: 30px;
  border-radius: 100%;
}

.post-owner .username {
  margin-left: 5px;
}

.post-owner .username > a {
  color: #333;
}
</style>
