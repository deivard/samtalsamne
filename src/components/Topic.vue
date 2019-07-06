<template>
  <div id="wrapper"
    class=""
  >
    <font-awesome-icon icon="angle-left" 
      class="angle text-4xl opacity-25 mt-3"
      @click="newTopic('right')"
    />
    <font-awesome-icon icon="angle-right"  
      class="angle text-4xl opacity-25 mt-3"
      :style="{ color: 'white'}"
      @click="newTopic('left')"  
    />
    <div id="topicWrapper"
      ref="topicWrapper"
    >
      <span class="block">
        <h3 class="text-xl mx-4" > {{ topic.topic }}</h3>
        <hr>
      </span>
      <button id="moreButton"
        class="text-sm w-auto float-right text-hairline mt-3 mr-3"
        v-show="!showBackground"
        @click="toggleBackground"
      >
        Berätta mer...
      </button>
    </div>
    <transition name="slide-fade">
      <div id="backgroundWrapper"
        class="inline-block px-4 py-2 text-left"
        v-show="showBackground"
        v-html="topic.background"
      >
      </div>
    </transition>
    <button id="lessButton"
      class="text-sm w-auto text-hairline mt-3"
      v-show="showBackground"
      @click="toggleBackground"
    >
      Okej, jag fattar!
    </button>
  </div>
</template>

<script>
import { faAngleRight, faAngleLeft } from '@fortawesome/free-solid-svg-icons'
import { timeout } from 'q';
import { setTimeout } from 'timers';

export default {
  name: "Topic",
  props: ["topic"],
  components: {

  },
  data(){
    return {
      showBackground: false
    }
  },
  methods: {
    toggleBackground: function (){
      this.showBackground = !this.showBackground
    },

    // Triggers animations and emits an event so that the parent component can change the topic
    newTopic: function(slideOutDirection) {
      this.showBackground = false;
      var classListOut = "slide-leave-right"
      var classListIn = "slide-enter-left"
      if(slideOutDirection === "left") {
        classListOut = "slide-leave-left"
        classListIn = "slide-enter-right"
      }
      this.$refs.topicWrapper.classList = classListOut
      setTimeout(() => {
        this.$emit('newTopic');
        this.$refs.topicWrapper.classList = classListIn
      }, 300)
    }
  }
  

}
</script>

<style scoped>
#wrapper {
  display: grid;
  max-width: 30em;
  grid-template-columns: 1fr 6fr 1fr;
  align-content: center;
  
}

#topicWrapper {
  grid-row: 1;
  grid-column: 2;
}

#backgroundWrapper {
  grid-row: 2;
  grid-column: 1/4;
}

#lessButton{
  grid-row: 3;
  grid-column: 2;
  justify-self: center;
}

.angle {
  justify-self: center;
}

.hidden {
  display:none;
}

hr {
  content: '';
  display: block;
  /* top: 20%; */
  width: 40%;
  border-top: 2px solid gray;
}


/* ANIMATIONS AND CLASSES RELATED TO ANIMATIONS */
/* -------------------------------------------- */
@keyframes leave-left {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: -3em; opacity: 0;}
}
@-moz-keyframes leave-left {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: -3em; opacity: 0;}
}
@-webkit-keyframes leave-left {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: -3em; opacity: 0;}
}
@-ms-keyframes leave-left {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: -3em; opacity: 0;}
}
@-o-keyframes leave-left {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: -3em; opacity: 0;}
}


@keyframes leave-right {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: 3em; opacity: 0;}
}
@-moz-keyframes leave-right {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: 3em; opacity: 0;}
}
@-webkit-keyframes leave-right {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: 3em; opacity: 0;}
}
@-ms-keyframes leave-right {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: 3em; opacity: 0;}
}
@-o-keyframes leave-right {
  0% { position: relative; left: 0; opacity: 1; }
  100% { position: relative; left: 3em; opacity: 0;}
}


@keyframes enter-from-left {
  0% { position: relative; left: -3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-moz-keyframes enter-from-left {
  0% { position: relative; left: -3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-webkit-keyframes enter-from-left {
  0% { position: relative; left: -3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-ms-keyframes enter-from-left {
  0% { position: relative; left: -3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-o-keyframes enter-from-left {
  0% { position: relative; left: -3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}

@keyframes enter-from-right {
  0% { position: relative; left: 3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-moz-keyframes enter-from-right {
  0% { position: relative; left: 3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-webkit-keyframes enter-from-right {
  0% { position: relative; left: 3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-ms-keyframes enter-from-right {
  0% { position: relative; left: 3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
@-o-keyframes enter-from-right {
  0% { position: relative; left: 3em; opacity: 0; }
  100% { position: relative; left: 0; opacity: 1;}
}
#moreButton,#lessButton{
  -webkit-animation: fadein 1s; /* Safari, Chrome and Opera > 12.1 */
  -moz-animation: fadein 1s; /* Firefox < 16 */
  -ms-animation: fadein 1s; /* Internet Explorer */
  -o-animation: fadein 1s; /* Opera < 12.1 */
  animation: fadein 1s;
}
@keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}
/* Firefox < 16 */
@-moz-keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}
/* Safari, Chrome and Opera > 12.1 */
@-webkit-keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}
/* Internet Explorer */
@-ms-keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}
/* Opera < 12.1 */
@-o-keyframes fadein {
    from { opacity: 0; }
    to   { opacity: 1; }
}
.slide-fade-enter-active {
  transition: all .5s ease;
}
.slide-fade-leave-active {
  transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active below version 2.1.8 */ {
  transform: translateY(10px);
  opacity: 0;
}


.slide-fade-active {
  transition: all .5s ease-out;
}

.slide-leave-left  {
  animation: leave-left .5s;
  -webkit-animation:leave-left .5s;
  -moz-animation:leave-left .5s;
  -ms-animation:leave-left .5s;
  -o-animation:leave-left .5s;
  animation-fill-mode: forwards;
  -webkit-animation-fill-mode: forwards;
  -moz-animation-fill-mode: forwards;
  -ms-animation-fill-mode: forwards;
  -o-animation-fill-mode: forwards;
}
.slide-leave-right {
  animation: leave-right .5s;
  -webkit-animation:leave-right .5s;
  -moz-animation:leave-right .5s;
  -ms-animation:leave-right .5s;
  -o-animation:leave-right .5s;
  animation-fill-mode: forwards;
  -webkit-animation-fill-mode: forwards;
  -moz-animation-fill-mode: forwards;
  -ms-animation-fill-mode: forwards;
  -o-animation-fill-mode: forwards;

}
.slide-enter-left {
  animation: enter-from-left .5s;
  -webkit-animation:enter-from-left .5s;
  -moz-animation:enter-from-left .5s;
  -ms-animation:enter-from-left .5s;
  -o-animation:enter-from-left .5s;
  animation-fill-mode: forwards;
  -webkit-animation-fill-mode: forwards;
  -moz-animation-fill-mode: forwards;
  -ms-animation-fill-mode: forwards;
  -o-animation-fill-mode: forwards;
}
.slide-enter-right {
  animation: enter-from-right .5s;
  -webkit-animation:enter-from-right .5s;
  -moz-animation:enter-from-right .5s;
  -ms-animation:enter-from-right .5s;
  -o-animation:enter-from-right .5s;
  animation-fill-mode: forwards;
  -webkit-animation-fill-mode: forwards;
  -moz-animation-fill-mode: forwards;
  -ms-animation-fill-mode: forwards;
  -o-animation-fill-mode: forwards;
}

</style>
