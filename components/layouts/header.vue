<template>
  <header v-fix>
    <div class="container header font-futura">
        <div class="header-left">
          <div class="logo">
            <nuxt-link to="/">
              <img src="~static/images/logo.png" alt="" width="36">
              三毛
            </nuxt-link>
          </div> 
          <nav>
            <nuxt-link
              v-for="(list, index) in nav"
              :key="index"
              :to="list.path"
              exact>
                <i :class="list.icon"></i>
                <span>{{ list.name }}</span>
            </nuxt-link>
          </nav>
        </div>
      <div class="saying">
        <carrousel :option="swiperOption" type="text" :con="saying"></carrousel>
      </div>
    </div> 
  </header>
</template>

<script>

import carrousel from '~components/common/carrousel.vue'

export default {
  name: 'header',
  data () {
    return {
      keyword: '',
      open: false,
      nav: [
        { path: '/', name: 'HOME', icon: 'iconfont icon-home'},
        { path: '/code', name: 'CODE', icon: 'iconfont icon-code'},
        { path: '/think', name: 'THINK', icon: 'iconfont icon-read'},
        { path: '/about', name: 'ABOUT', icon: 'iconfont icon-user'},
        { path: '/wall', name: 'WALL', icon: 'iconfont icon-comments'}
      ],
      swiperOption: {
        direction: 'vertical',
        loop: true,
        autoplay: 5000,
        setWrapperSize: true,
        autoHeight: true,
        paginationClickable: true,
        autoplayDisableOnInteraction: false,
        observeParents: true,
        grabCursor: true,
        spaceBetween: 30,
        mousewheelControl: true
      }
    }
  },

  computed: {
    saying () {
      return this.$store.state.hotReview.data.list
    }
  },

  components: { carrousel },

  directives: {
    fix: {
      inserted (el) {
        window.addEventListener('scroll', _ => {
          const top = window.pageYOffset
          if (top > 64) el.classList.add('draken')
          else el.classList.remove('draken')
        })
      },
      unbind () {
        window.onscroll = null
      }
    }
  }
}
</script>

<style lang="scss">

@import '~assets/scss/variable.scss';
@import '~assets/scss/mixin.scss';

header {
  position: fixed;
  top: 0;
  z-index: 999;
  width: 100%;
  height: $header-height;
  background: $module-bg;
  @include box-shadow(0, 1px, 2px, rgba(0,0,0,.05));

  &:hover {
    background: $white;
  }

  &.draken {
    background: $white;
  }

  >.header {
    display: flex;
    justify-content: space-between;
    height: $header-height;
    line-height: $header-height;

    >.header-left {
      display: flex;

      >.logo{

        a {
          color: $black;
          font-size: 2rem;
        }
      }
    }
  }

  nav {
    margin-left: 2rem;

    >a {
      margin-right: 2rem;
      padding: .5rem;
      color: $disabled;

      >i {
        margin-right: .5rem;
      }

      &:hover {
        color: $black;
      }
    }

    >a.link-active {
      color: $black;
    }
  }

  .saying {
    width: 20.3rem;
    font-size: $font-size-small;
    line-height: $normal-pad;
    overflow: hidden;

    .swiper {
      height: $header-height;
      color: $dividers;

      .item {
        display: flex;
        flex-direction: column;
        justify-content: center;
        height: 100%;

        >.saying-content {
          text-align: left;
        }

        >.saying-author {
          margin-top: .3rem;
          text-align: right;
        }
      }

      &:hover {
        color: $black;
      }
    }
  }
}
</style>
