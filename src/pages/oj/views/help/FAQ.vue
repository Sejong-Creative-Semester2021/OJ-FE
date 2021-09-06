<template>
  <Panel shadow :padding="10">
    <div slot="title">
      {{$t('m.FAQ')}}
    </div>
    <v-expansion-panels focusable>
      <v-expansion-panel v-for="faq in faqs" :key="faq.question">
        <v-expansion-panel-header>
          {{faq.question}}
          <template v-slot:actions>
            <v-icon right>
              {{mdiMenuDown}}
            </v-icon>
          </template>
        </v-expansion-panel-header>
        <v-expansion-panel-content v-html="faq.answer" key="answer" class="content-container">
          {{faq.answer}}
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
  </Panel>
</template>

<script>
  import api from '@oj/api'
  import { mdiMenuDown } from '@mdi/js'

  export default {
    name: 'FAQ',
    data () {
      return {
        mdiMenuDown,
        faqs: [],
        faq: ''
      }
    },
    mounted () {
      this.init()
    },
    methods: {
      init () {
        this.getFAQList()
      },
      getFAQList () {
        api.getFAQList().then(res => {
          this.faqs = res.data.data.results
        })
      }
    }
  }
</script>

<style lang="less" scoped>
  .content-container {
    padding: 20px 20px 20px 20px;
  }
</style>
