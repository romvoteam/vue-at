<template>
  <div id="app">
    <at :members="members" :on-search="findMembers" name-key="name" v-model="html" :ats="['@', '#']" :ats-classes="['mention', 'hashtag']">
      <!-- custom: same as default slot -->
      <!-- <template slot="item" scope="s">
        <span v-text="s.item"></span>
      </template> -->

      <span slot="embeddedItem" slot-scope="s">
        <span class="tag"><img class="avatar" :src="s.current.avatar">{{ s.current.name }}</span>
      </span>

      <!-- custom: with avatars -->
      <template slot="item" scope="s">
        <img :src="s.item.avatar">
        <span v-text="s.item.name"></span>
      </template>

      <div class="editor"
        contenteditable></div>
    </at>
  </div>
</template>

<script>
// import At from 'vue-at'
// import At from '../dist/vue-at'
// import AtTa from '../dist/vue-at-textarea'
import At from './At.vue'
import AtTa from './AtTextarea.vue'

let members = [
  /* eslint-disable */
  "Roxie Miles","grace.carroll",
  "小浩",
  "Helena Perez","melvin.miller",
  "椿木",
  "myrtie.green","elsie.graham","Elva Neal",
  "肖逵",
  "amy.sandoval","katie.leonard","lottie.hamilton",
  /* eslint-enable */
]

let hashtags = [
  /* eslint-disable */
  "Roxie Miles2","grace.carroll",
  "小浩",
  "Helena Perez","melvin.miller",
  "椿木",
  "myrtie.green","elsie.graham","Elva Neal",
  "肖逵",
  "amy.sandoval","katie.leonard","lottie.hamilton",
  /* eslint-enable */
]
members = members.map((v, i) => {
  return {
    avatar: `https://randomuser.me/api/portraits/men/${i % 5}.jpg`,
    name: v
  }
})
hashtags = hashtags.map((v, i) => {
  return {
    avatar: `https://randomuser.me/api/portraits/men/${i % 5}.jpg`,
    name: v
  }
})

export default {
  components: { At, AtTa },
  name: 'app',
  data () {
    const data = {
      members,
      members2: members,
      text: '',
      html: ''
    }
    return data
  },
  methods: {
    findMembers(symbol) {
      this.members = [];

      setTimeout(() => {
        if (symbol === '@') {
          this.members = this.members2;
        }

        if (symbol === '#') {
          this.members = hashtags;
        }
      }, 2500);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 30px;
}

.tag {
  border-radius: 5px;
  background: beige;
  border: 1ps outset yellow;
}
.editor {
  width: 400px;
  height: 200px;
  overflow: auto;
  white-space: pre-wrap;
  border: solid 2px rgba(0,0,0,.5);
}

.avatar {
  max-width: 1em;
  vertical-align: middle;
}
textarea {
  padding: 0;
  font-size: inherit;
  resize: none;
}

/* override styles */
#app .atwho-li {
  padding: 0 4px;
}
#app .atwho-li img {
  height: 100%;
  width: auto;
  -webkit-transform: scale(.8);
}
#app .atwho-li span {
  padding-left: 8px;
}
#app .atwho-wrap {
  display: inline-block;
  vertical-align: top;
  margin-left: 40px;
  margin-top: 30px;
}

.mention .tag {
  background: red;
  color: white;
}

.hashtag .tag {
  background: cyan;
  color: yellowgreen;
}
</style>
