<template>
  <section  class="think" >
    <div class="head" :class="{'mobile': mobileLayout}">
      <p class="font-futura">CREATE ART WITH CODE</p>
    </div>
    <div class="article">
      <articleView
        :articleList = "list"
        :haveMoreArt="haveMoreArt"
        @loadMore="loadMore"></articleView>
    </div>
  </section>
</template>

<script>

const articleView = () => import('~components/common/article.vue')

export default {

  scrollToTop: true,

  head: {
    title: 'code'
  },

  transition: 'fade',

  fetch ({ store }) {
    return store.dispatch('getArtList', { type: 1 })
  },

  data () {
    return {}
  },

  computed: {

    mobileLayout () {
      return this.$store.state.options.mobileLayout
    },

    list () {
      return this.$store.state.article.art.list
    },


    haveMoreArt () {
      return this.$store.state.article.art.pagination.current_page
              !== this.$store.state.article.art.pagination.total_page
    }
  },

  components: {
    articleView
  },

  methods: {
    loadMore () {
      this.$store.dispatch('getArtList', {
        current_page: this.$store.state.article.art.pagination.current_page + 1,
        type: 1,
      })
    }
  }
}
</script>


<style lang="scss" scoped>

@import '~assets/scss/variable.scss';
@import '~assets/scss/mixin.scss';


.head {
  display: grid;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 20rem;
  margin-bottom: $normal-pad;
  font-size: 1.3rem;
  color: $black;
  background: $module-bg;
  // background: $module-bg url() no-repeat center 55%;  
  p {

  }
}

.head.mobile {
  height: 10rem;
}
</style>
