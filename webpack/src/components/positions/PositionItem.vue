<template lang="html">
  <div class="item">
    <div class="item-header row" v-on:click="toggleItem()">
      <div class="col-xs-10 item-main">
        <div class="box">
          <h2 class="job-title">{{position.title}}</h2>
          <p class="job-type">
            {{position.type}}
          </p>
          <p class="job-category">{{position.category}}</p>


          <p class="company">{{position.salary}} • {{position.company.name}} • {{position.company.location}}</p>
          <DaysAgo v-bind:createdAt="position.createdAt"></DaysAgo>
        </div>
          </div>
      <div class="col-xs-2 item-action">
        <div class="box">
          <button class="btn btn-green item-button item-button-expand">
            View
          </button>
          <button class="btn btn-red item-button item-button-narrow">
            Close
          </button>

        </div>
      </div>
    </div>
    <div class="job-detail">
      <div class="row">

        <div class="col-sm-12">
          <div class="description">
            <MarkdownView v-bind:rawMarkdown="position.description"></MarkdownView>
          </div>
        </div>
        <div class="col-sm-12">
          <h6>Contact:</h6>
          <ul class='job-contact'>
            <li><a v-bind:href="'mailto:' + position.company.email">{{position.company.email}}</a></li>
            <li><a v-bind:href="'http://' + position.company.website">{{position.company.website}}</a></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MarkdownView from './PositionMarkdownView'
import DaysAgo from './PositionDaysAgo'

function findPos (obj) {
  let curtop = 0
  if (obj.offsetParent) {
    do {
      curtop += obj.offsetTop
      obj = obj.offsetParent
    } while (obj)
    return [curtop]
  }
}

export default {
  props: ['position', 'removeActive'],
  components: {
    MarkdownView,
    DaysAgo
  },
  methods: {
    toggleItem () {
      const item = this.$el
      const itemClassList = item.classList
      if (itemClassList.contains('active')) {
        itemClassList.toggle('active')
      } else {
        this.removeActive()
        itemClassList.add('active')
        window.scroll(0, findPos(item))
      }
    }
  }
}
</script>

<style scoped lang="scss">
$base-color: rgb(0,0,0);
$alt-color: rgb(255, 255, 255);
$gray-color-hover: rgba(191, 191, 191, 0.5);
$sm-display: 48rem;
$line-height: 6rem;
$transition-duration: 0.1s;
.row {

  align-content: center;
  align-items: center;
}
.item {
  margin:20px 0;
  border-radius:5px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  padding: 20px;
  pointer-events: auto;
  transition:all 350ms ease-in-out;
  background-color:white;

  &:hover {
    transform:scale(1.025);
    box-shadow: 0 2px 20px rgba(0,0,0,0.1);
    .item-action .item-button {
    }
  }

  a {
    //color: $alt-color;
    text-decoration: none;
    &:hover {
      text-decoration: underline;
    }
  }

  .item-header {
    cursor: pointer;
  }
  .job-title {
    transition: font-size $transition-duration ease-in;
    font-size: 2.2rem;
    display:inline-block;
    margin-bottom: 1rem;
    margin-right:10px;
    font-weight:normal;
  }
  .job-type {
    display: inline-block;
    line-height: 1rem;
    background: #9E9E9E;
    color: white;
    padding: 5px;
    border-radius: 2px;
    vertical-align:1px;
  }

  .item-sub .location,
  .job-category,
  .job-salary,
  .job-type {
    transition: font-size $transition-duration ease-in;
    margin: 0;
    font-size: 1.3rem;
  }

  .item-meta {
    font-size: 1.2rem;
    line-height: $line-height;
  }

  .job-category,
  .job-salary {
    display: none;
  }

  .item-action {
    text-align: center;
    align-content: center;
    .item-button {
    //   line-height: $line-height;
    cursor: pointer;
    //   background: transparent;
    //   border: none;
    //   font-size: 2rem;
    //
    //   &:hover {
    //     font-weight: bold;
    //   }
    //
     &:focus {
        outline: none;
      }
    }
  }

  .item-button-narrow {
    display: none;
  }

  .job-detail {
    display: none;
    padding-top: 2rem;

    .job-contact {
      list-style: none;
      font-size: 1.3rem;
      -webkit-margin-before: 0;
      -webkit-margin-after: 0;
      -webkit-margin-start: 0;
      -webkit-margin-end: 0;
      -webkit-padding-start: 0;
    }

    .description {
      font-size: 1.5 rem;
      color:black;
    }
  }
}
// When Activated

.item.active {
transform:scale(1.025);
margin:50px 0;
box-shadow: 0 2px 20px rgba(0,0,0,0.1);
  .company,
  .job-title {
    //font-size: 2.5rem;
  }

  .item-sub .location,
  .job-category,
  .job-salary,
  .job-type {
    //font-size: 1.5rem;
  }

  .item-meta {
    //font-size: 1.3rem;
  }


  .job-category,
  .job-salary {
    //display: inherit;
  }

  .item-button {
    //color: $alt-color;
  }

  .item-button-expand {
    display: none;
  }

  .item-button-narrow {
    display: inherit;
  }
  .job-detail {
    display: inherit;
  }
}

// Responsive
@media (max-width: $sm-display) {
  .item {
    padding: 3rem;

    .company,
    .job-title {
      font-size: 1.5em;
    }

    .item-sub .location,
    .job-category,
    .job-salary,
    .job-type {
      margin: 0;
      font-size: 1.1rem;
    }
  }

  .item.active {
    padding: 3rem;

    .company,
    .job-title {
      font-size: 1.7em;
    }

    .job-detail {
      //padding-top: 1rem;
    }

    .item-sub .location,
    .job-category,
    .job-salary,
    .job-type {
      font-size: 1.2rem;
    }

    .job-apply {
      width: 100%;
    }

    .item-meta {
      line-height: inherit;
    }
  }
}

</style>
