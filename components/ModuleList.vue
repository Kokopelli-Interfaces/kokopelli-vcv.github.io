<template lang='pug'>
.module-list
  ttl.title(v-if='title', :level='2') {{ title }}
  ul
    li(v-for='module in modules')
      nuxt-link.module-link(
        :to='{ name: "categorySlug-moduleSlug", params: { categorySlug: module.category.slug, moduleSlug: module.slug } }'
      )
        .name-section
          .module-name {{ module.name }}
          .module-function {{ module.function }}
        .price-section
          price-label.label
          | {{ module.price ? '$' + module.price : $t('free') }}
        arrow.arrow
</template>

<script>
import Arrow from '~/assets/images/icons/arrow-right.svg?inline'
import PriceLabel from '~/assets/images/icons/label.svg?inline'
import Ttl from '~/components/Title'

export default {
  props: {
    modules: {
      type: Array,
      default: () => ([])
    },
    title: {
      type: String,
      default: ''
    }
  },
  components: {
    Arrow,
    PriceLabel,
    Ttl
  }
}
</script>

<style lang='scss' scoped>
@import "~/assets/sass/breakpoints.scss";

.module-list {
  .title {
    margin-bottom: 20px;
  }
  ul {
    margin-top: 0;
    margin-bottom: 0;
    padding-left: 0;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
    grid-gap: 20px 60px;

    @include phone {
      grid-gap: 20px 40px;
    }

    li {
      list-style: none;
      font-size: 14px;

      .module-link {
        display: flex;
        align-items: center;
        height: 100%;

        &:hover {
          text-decoration: underline;
        }

        .name-section {
          margin-right: auto;
          padding-right: 10px;
          display: flex;
          flex-direction: column;
          justify-content: center;

          .module-name {
            font-family: 'Montserrat';
            font-weight: 600;
            font-size: 15px;
          }
          .module-function {
            opacity: .6;
            margin-top: 4px;
          }
        }

        .price-section {
          display: flex;
          align-items: center;
          margin-right: 30px;

          .label {
            margin-right: 20px;
          }
        }

        .arrow {
          flex-shrink: 0;
        }
      }
    }
  }
}
</style>
