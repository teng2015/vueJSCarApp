<template>
  <div id="app">
    <div class="Center-Container is-Inline">
      <a class="navigation navigation-prev " aria-label="Previous page: State" value="v-a" id="a" name="view" v-on:click="changeViewLeft">
          <i class="fa fa-angle-left"></i>
      </a>
      <timeline></timeline>
      <div class="Center-Block">
          <transition name="component-fade" mode="out-in">
            <keep-alive>
              <component v-bind:is="view"></component>
            <keep-alive>
          </transition>
      </div>
      <a class="navigation navigation-next " aria-label="Next page: Mutations" style="margin-right: 0px;" value="v-b" id="b" name="view" v-on:click="changeViewRight">
          <i class="fa fa-angle-right"></i>
      </a>
    </div>
  </div>
</template>

<script>
import state1 from './components/state1'
import state2 from './components/state2'
import state3 from './components/state3'
import timeline from './components/timeline'

export default {
  name: 'app',
  data () {
    return {
      view: 'state-1'
    }
  },
  components: {
    state1,
    timeline,
    'state-1': {
      template: '<state1/>',
      components: { state1 }
    },
    'state-2': {
      template: '<state2>',
      components: { state2 }
    },
    'state-3': {
      template: '<state3>',
      components: { state3 }
    }
  },
  methods: {
    changeViewRight: function () {
      if (parseInt(this.view.slice(-1)) <= 4) {
        var x = parseInt(this.view.slice(-1))
        this.view = 'state-' + (x + 1).toString()
      }
    },
    changeViewLeft: function () {
      if (parseInt(this.view.slice(-1)) > 1) {
        var x = parseInt(this.view.slice(-1))
        this.view = 'state-' + (x - 1).toString()
      }
    }
  }
}
</script>

<style>
.navigation.navigation-prev {
  left: 0;
}
.navigation.navigation-next {
  right: 0;
}
.fa {
    display: inline-block;
    font: normal normal normal 14px/1 FontAwesome;
    font-size: inherit;
    text-rendering: auto;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}
.fa-angle-right:before {
    content: "\f105";
}
.fa-angle-left:before {
    content: "\f104";
}
@media (max-width: 1240px)
.navigation {
    position: static;
    top: auto;
    max-width: 50%;
    width: 50%;
    display: inline-block;
    float: left;
}
.navigation {
    position: absolute;
    top: 50px;
    bottom: 0;
    margin: 0;
    max-width: 150px;
    min-width: 90px;
    display: flex;
    justify-content: center;
    align-content: center;
    flex-direction: column;
    font-size: 40px;
    color: #ccc;
    text-align: center;
    -webkit-transition: all 350ms ease;
    -moz-transition: all 350ms ease;
    -o-transition: all 350ms ease;
    transition: all 350ms ease;
}
a {
    text-decoration: none;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  .Center-Container.is-Flexbox {
    display: -webkit-box;
    display: -moz-box;
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
    -webkit-box-align: center;
       -moz-box-align: center;
       -ms-flex-align: center;
    -webkit-align-items: center;
            align-items: center;
    -webkit-box-pack: center;
       -moz-box-pack: center;
       -ms-flex-pack: center;
    -webkit-justify-content: center;
            justify-content: center;
  }
}
.component-fade-enter-active, .component-fade-leave-active {
  transition: opacity .3s ease;
}
.component-fade-enter, .component-fade-leave-active {
  opacity: 0;
}
.Center-Block {
  display: inline-block;
}
</style>
