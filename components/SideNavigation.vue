<template>
  <div class="SideNavigation">
    <div class="SideNavigation-HeadingContainer sp-flex">
      <v-icon
        class="SideNavigation-HeadingIcon sp-inline-block"
        :aria-label="$t('Navi Open')"
        @click="openNavi"
      >
        mdi-menu
      </v-icon>
      <nuxt-link to="/" class="SideNavigation-HeadingLink">
        <!-- <div class="SideNavigation-Logo">
          <img src="/logo.svg" :alt="$t('Gifu Prefectural Government')" />
        </div> -->
        <h1 class="SideNavigation-Heading">
          {{ $t('Gifu Prefectural Government') }}<br />
          {{ $t('COVID-19') }}<br />{{ $t('Measures site') }}
        </h1>
      </nuxt-link>
    </div>
    <v-divider class="SideNavigation-HeadingDivider" />
    <div class="sp-none" :class="{ open: isNaviOpen }">
      <v-icon
        class="SideNavigation-ListContainerIcon sp-inline-block"
        :aria-label="$t('Navi Close')"
        @click="closeNavi"
      >
        mdi-close
      </v-icon>
      <v-list :flat="true">
        <v-container
          v-for="(item, i) in items"
          :key="i"
          class="SideNavigation-ListItemContainer"
          @click="closeNavi"
        >
          <ListItem :link="item.link" :icon="item.icon" :title="item.title" />
          <v-divider v-show="item.divider" class="SideNavigation-Divider" />
        </v-container>
      </v-list>
      <div class="SideNavigation-Footer">
        <div class="SideNavigation-SocialLinkContainer">
          <a
            href="https://twitter.com/gifukenkiki"
            target="_blank"
            rel="noopener"
          >
            <img src="/twitter.png" alt="Twitter" />
          </a>
          <a
            href="https://www.facebook.com/minamodayori/"
            target="_blank"
            rel="noopener"
          >
            <img src="/facebook.png" alt="Facebook" />
          </a>
        </div>
        <small class="SideNavigation-Copyright" lang="en">
          Copyright &copy; 2020 ICT LABO -GIFU- All Rights
          Reserved.
        </small>
      </div>
    </div>
  </div>
</template>

<i18n>
{
  "ja": {
    "Navi Open": "サイドメニュー項目を開く",
    "Navi Close": "サイドメニュー項目を閉じる",
    "COVID-19": "新型コロナウイルス感染症",
    "Measures site": "対策サイト",
    "Gifu Prefectural Government": "岐阜県",
    "COVID-19 Task Force": "新型コロナウイルス感染症対策本部",
    "The latest updates": "県内の最新感染動向",
    "If you have any symptoms": "新型コロナウイルス感染症が心配なときに",
    "for Families with children": "お子様をお持ちの皆様へ",
    "for Citizens": "県民の皆様へ",
    "for Business person": "事業者の皆さまへ",
    "for Lodging business": "宿泊事業者の皆さまへ",
    "Cancelled public events": "県主催イベント・県有文化施設等の対応状況",
    "Government official website": "岐阜県公式ホームページ",
    "About us": "当サイトについて"
  }
}
</i18n>

<script>
import ListItem from '@/components/ListItem'

export default {
  components: {
    ListItem
  },
  props: {
    isNaviOpen: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    items() {
      return [
        {
          icon: 'mdi-chart-timeline-variant',
          title: this.$t('The latest updates'),
          link: '/'
        },
        {
          icon: 'covid',
          title: this.$t('If you have any symptoms'),
          link: '/flow',
          divider: true
        },
        {
          icon: 'parent',
          title: this.$t('for Families with children'),
          link: '/parent'
        },
        {
          icon: 'mdi-account-multiple',
          title: this.$t('for Citizens'),
          link: 'https://www.pref.gifu.lg.jp/kinkyu-juyo-joho/shingata_corona.html'
        },
        {
          icon: 'mdi-domain',
          title: this.$t('for Business person'),
          link: '/worker',
        },
        {
          icon: 'mdi-home-city',
          title: this.$t('for Lodging business'),
          link: '/lodging',
          divider: true
        },
        {
          title: this.$t('Cancelled public events'),
          link:
            'https://www.pref.gifu.lg.jp/shingata_corona_enki.html'
        },
        {
          title: this.$t('About us'),
          link: '/about'
        },
        {
          title: this.$t('Government official website'),
          link: 'https://www.pref.gifu.lg.jp/',
          divider: true
        }
      ]
    }
  },
  methods: {
    openNavi() {
      this.$emit('openNavi')
    },
    closeNavi() {
      this.$emit('closeNavi')
    }
  }
}
</script>

<style lang="scss" scoped>
.SideNavigation {
  position: relative;
  height: 100%;
  background: $white;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.15);
  &-HeadingContainer {
    padding: 1.25em 0 1.25em 1.25em;
    align-items: center;
    @include lessThan($small) {
      padding: 7px 0 7px 20px;
    }
  }
  &-HeadingIcon {
    display: none;
    margin-right: 16px;
  }
  &-HeadingLink {
    @include lessThan($small) {
      display: flex;
      align-items: center;
    }
    text-decoration: none;
  }
  &-ListContainerIcon {
    display: none;
    margin: 24px 16px 0;
  }
  &-ListItemContainer {
    padding: 2px 20px;
  }
  &-Logo {
    margin: 20px 16px 0 0;
    width: 110px;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-Heading {
    margin-top: 8px;
    font-size: 13px;
    color: #898989;
    padding: 0.5em 0;
    text-decoration: none;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-HeadingDivider {
    margin: 0px 20px 4px;
    @include lessThan($small) {
      display: none;
    }
  }
  &-Divider {
    margin: 12px 0;
  }
  &-Footer {
    padding: 20px;
    background-color: $white;
  }
  &-SocialLinkContainer {
    display: flex;
    & img {
      width: 30px;
      &:first-of-type {
        margin-right: 10px;
      }
    }
  }
  &-Copyright {
    display: block;
    margin-top: 10px;
    font-size: 8px;
    line-height: 1.2;
    color: $gray-1;
    font-weight: bold;
  }
}
.open {
  @include lessThan($small) {
    position: absolute;
    top: 0;
    left: 0;
    display: block !important;
    width: 100%;
    z-index: 100;
    background-color: $white;
  }
}
@include lessThan($small) {
  .sp-flex {
    display: flex;
  }
  .sp-inline-block {
    display: inline-block;
  }
  .sp-none {
    display: none;
  }
}
</style>
