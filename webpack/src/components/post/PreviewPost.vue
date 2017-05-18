<template lang="html">
  <div class="">
    <h1 class="header">Preview</h1>
    <div class="item active">
      <div class="item-header row">
        <div class="col-xs-6 item-main">
          <div class="box">
            <h4 class="job-title">{{position.title}}</h4>
            <p class="job-type">{{position.type}}</p>
            <p class="job-salary">{{position.salary}}</p>
            <p class="job-category">{{position.category}}</p>
          </div>
        </div>
        <div class="col-xs-3 item-sub">
          <div class="box">
            <h4 class="company">{{company.name}}</h4>
            <p class="location">{{company.location}}</p>
          </div>
        </div>
        <div class="col-xs-2 item-meta">
          <div class="box">
            <span>{{position.createdAt}}</span>
          </div>
        </div>
        <div class="col-xs-1 item-action">
          <div class="box">
          </div>
        </div>
      </div>
      <div class="job-detail">
        <div class="row">
          <div class="col-sm-12 col-md-6">
            <h6>Contact:</h6>
            <ul class='job-contact'>
              <li><a v-bind:href="'mailto:' + company.email">{{company.email}}</a></li>
              <li><a v-bind:href="'http://' + company.website">{{company.website}}</a></li>
            </ul>
          </div>
          <div class="col-sm-12 col-md-6">
            <div class="description">
              <MarkdownView v-bind:rawMarkdown="position.description"></MarkdownView>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
import MarkdownView from '../positions/PositionMarkdownView'

export default {
  props: ['position', 'company'],
  components: {
    MarkdownView
  }
}
</script>

<style scoped lang="scss">

</style>
