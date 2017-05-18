<template lang="html">
  <div>



<div class="row">
  <div class="col-sm-9">
    <div class="search-wrapper">
      <input type="text" placeholder="SEARCH..." class="search-bar" v-model="searchText">
    </div>
  </div>
  <div class="col-sm-3 post-wrapper">
      <router-link to="/post-a-job" class="btn btn-blue">Post a Job</router-link>
  </div>
</div>
  <div class="position-list">


    <PositionItem
      v-for="position in filterPositions"
      v-bind:position="position"
      v-bind:removeActive="removeActive"
      v-bind:key="position.title"
    >
    </PositionItem>
    <div class="loadCompleted" v-if="loadCompleted">
      <p>
        This is our all positions.
      </p>
    </div>
    <div class="loadMore" v-else>
      <button type="button" name="button" class="btn btn-blue " v-on:click="loadMore" v-show="!loadCompleted">Load More</button>
    </div>
    <div class="row list-footer">
      <div class="col-sm-3">
        <router-link to="/" class="brand-logo-footer">Tech Jobs</router-link>
      </div>
      <div class="col-sm-offset-6 col-sm-3">
        <router-link to="/manage-positions" class="link-footer">Manage Positions</router-link>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import PositionItem from './PositionItem'
import { mapGetters } from 'vuex'

export default {
  components: {
    PositionItem
  },
  data () {
    return {
      searchText: ''
    }
  },
  computed: {
    ...mapGetters({
      positions: 'allPositions',
      loadCompleted: 'loadCompleted'
    }),
    filterPositions: function () {
      const filterText = this.searchText
      const filteredPositions = this.positions.filter(function (position) {
        return position.title.includes(filterText) ||
               position.company.name.includes(filterText) ||
               position.category.includes(filterText)
      })
      return filteredPositions
    },
    checkLoadAll: function () {
      console.log(this.loadCompleted)
      return this.$store.state.loadCompleted
    }
  },
  created () {
    this.$store.dispatch('getInitialPositions')
  },
  methods: {
    routeToPostJob () {
      this.$router.push('/post-a-job')
    },
    removeActive () {
      const activatedItem = this.$el.querySelector('.item.active')
      if (activatedItem) {
        activatedItem.classList.remove('active')
      }
    },
    loadMore () {
      this.$store.dispatch('getNextPositions')
    }
  }
}
</script>

<style scoped lang="scss">
$base-color: rgb(0,0,0);
$alt-color: rgb(255, 255, 255);
$sm-display: 48rem;
$transition-duration: 0.1s;
$color-blue: #2196f3;
.post-wrapper {
  text-align:right;
}

.search-wrapper {
  width: 100%;
  //background-color: $base-color;
  cursor: text;
  transition-duration: $transition-duration;
  transition-property: all;
  transition-timing-function: ease-in;

  .search-bar {
    cursor: text;
    width: 100%;
    border-radius:5px;
    padding: 10px 20px;
    border:1px solid $color-blue;
    font-size: 1.2em;
    color: black;
    letter-spacing: 1px;
    margin-bottom:20px;

    &:focus {
      cursor: text;
      background-color: $alt-color;
      color: $base-color;
      outline: none;
    }

    &:focus + .form-icon {
      color: $base-color;
    }
  }

  .search-bar::-webkit-input-placeholder {
    color: black;
    letter-spacing: 1px;
  }
}

.list-footer {
  border-top: 1px solid $base-color;
  margin: 0;
  padding: 0;
  margin-top: 2rem;
  padding-top: 2rem;
  margin-bottom: 2rem;

  .brand-logo-footer {
    padding-left: 6rem;
    font-size: 2rem;
    color: $base-color;
    text-decoration: none;
  }

  .link-footer {
    color: $base-color;
    text-decoration: none;
    font-size: 1.3rem;

    &:hover {
      text-decoration: underline;
    }
  }
}
.loadCompleted {
  font-size: 2rem;
  text-align: center;
}

.loadMore {
  text-align: center;
}
.post-button.btn-sm {
  width: inherit;
  padding: 1rem 2rem;
}

@media (max-width: $sm-display) {
  .search-wrapper, .post-wrapper {
      height: 6rem;
      font-size: 2rem;
  }

  .search-wrapper .search-bar {
    height: 6rem;
    padding-left: 3rem;
    font-size: 2rem;
  }


  .post-wrapper {
    padding-left: 3rem;
    line-height: 6rem;
    .post-link {
      height: 3rem;
      font-size: 2rem;
      line-height: 3rem;
    }
  }
}
</style>
