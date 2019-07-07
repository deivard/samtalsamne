<template>
  <div id="app">
    <the-navbar class=""></the-navbar>
    <div id="bodyWrapper"
      class="flex flexwrap justify-center"
    >
      <div id="topicWrapper"
        class="text-center mt-10"
      >
        <Topic :topic="activeTopic"
          @newTopic="setNewRandomTopic"
        ></Topic>
      </div>
    </div>
    <hr class="my-4">
    <div id="categoriesWrapper" class="mx-auto">
      <CategoriesGroup
        :categories="categories"
      >
      </CategoriesGroup>

    </div>

  </div>
</template>

<script>
import TheNavbar from './components/TheNavbar.vue'
import Topic from './components/Topic'
import CategoriesGroup from './components/CategoriesGroup'

export default {
  name: 'app',
  components: {
    TheNavbar,
    Topic,
    CategoriesGroup
  },
  data() {
    return {
      activeTopic: {},
      activeCategory: "",
      seenTopics: [],
      categories: ["allmänt", "politik", "filosofi", "kontroversiellt", "dejt"],
      dummyTopics: [
        { 
          id: "1",
          topic: "Tror du att global warming är påhittat?",
          background: `<p>No prey, no pay keel hempen halter tackle gangway Jack Tar me hornswaggle capstan ballast. Brigantine Davy Jones' Locker plunder skysail mutiny shrouds clap of thunder Privateer crack Jennys tea cup Gold Road. Chantey lugger reef yardarm parley spike Barbary Coast snow transom Brethren of the Coast.</p> 
                        <p>Reef sails Arr rutters scourge of the seven seas long boat provost shrouds clipper bounty tender. Handsomely reef sails dance the hempen jig rope's end gangway nipperkin gally deadlights chandler pillage. List to go on account sloop hearties reef loaded to the gunwalls take a caulk crimp pink Gold Road.</p>
                        <p>Furl man-of-war plunder avast boatswain yard no prey, no pay Chain Shot knave bilged on her anchor. Gun ye Letter of Marque maroon gunwalls starboard matey log code of conduct hempen halter. Chantey bilged on her anchor Pieces of Eight hulk haul wind tackle league matey Jack Tar case shot.</p>
                        `
        },
        {
          id: "2",
          topic: "Om du bara fick kolla på en filmgenre resten av livet, vilken skulle du välja?",
          background: ` Carrot cake carrot cake chupa chups pastry jelly beans cake I love icing. Tootsie roll I love cake wafer chupa chups bear claw lollipop. Jujubes macaroon jelly pudding I love jelly-o chocolate cake danish. Tart lollipop jujubes croissant toffee.
                        Cookie marzipan powder topping. Gummi bears apple pie powder pie. Chupa chups apple pie dessert jujubes cake chocolate bar.
                        `
        },
        {
          id: "3",
          topic: "Om du kunde ta tjänstledigt i ett halvår, var skulle du åka och vad skulle du göra?",
          background: ` Carrot cake carrot cake chupa chups pastry jelly beans cake I love icing. Tootsie roll I love cake wafer chupa chups bear claw lollipop. Jujubes macaroon jelly pudding I love jelly-o chocolate cake danish. Tart lollipop jujubes croissant toffee.
                        Cookie marzipan powder topping. Gummi bears apple pie powder pie. Chupa chups apple pie dessert jujubes cake chocolate bar.
                        `
        },
        {
          id: "4",
          topic: "Skulle du hellre jobba fyra 10-timmarsdagar eller fem 8-timmarsdagar i veckan?",
          background: ` Carrot cake carrot cake chupa chups pastry jelly beans cake I love icing. Tootsie roll I love cake wafer chupa chups bear claw lollipop. Jujubes macaroon jelly pudding I love jelly-o chocolate cake danish. Tart lollipop jujubes croissant toffee.
                        Cookie marzipan powder topping. Gummi bears apple pie powder pie. Chupa chups apple pie dessert jujubes cake chocolate bar.
                        `
        },
        {
          id: "5",
          topic: "Om du fick bestämma världens åttonde underverk, vad skulle du välja då?",
          background: ` Carrot cake carrot cake chupa chups pastry jelly beans cake I love icing. Tootsie roll I love cake wafer chupa chups bear claw lollipop. Jujubes macaroon jelly pudding I love jelly-o chocolate cake danish. Tart lollipop jujubes croissant toffee.
                        Cookie marzipan powder topping. Gummi bears apple pie powder pie. Chupa chups apple pie dessert jujubes cake chocolate bar.
                        `
        },
        {
          id: "6",
          topic: "Du får undervisa i valfritt ämne på universitet, vad väljer du?",
          background: ` Carrot cake carrot cake chupa chups pastry jelly beans cake I love icing. Tootsie roll I love cake wafer chupa chups bear claw lollipop. Jujubes macaroon jelly pudding I love jelly-o chocolate cake danish. Tart lollipop jujubes croissant toffee.
                        Cookie marzipan powder topping. Gummi bears apple pie powder pie. Chupa chups apple pie dessert jujubes cake chocolate bar.
                        `
        },
        {
          id: "7",
          topic: "Vilken uppfinning önskar du var din från början?",
          background: ` Carrot cake carrot cake chupa chups pastry jelly beans cake I love icing. Tootsie roll I love cake wafer chupa chups bear claw lollipop. Jujubes macaroon jelly pudding I love jelly-o chocolate cake danish. Tart lollipop jujubes croissant toffee.
                        Cookie marzipan powder topping. Gummi bears apple pie powder pie. Chupa chups apple pie dessert jujubes cake chocolate bar.
                        `
        },
        {
          id: "8",
          topic: "Gjorde Hitler fel?",
          background: ` I love cheese, especially cauliflower cheese st. agur blue cheese. When the cheese comes out everybody's happy smelly cheese paneer brie airedale rubber cheese goat edam. Camembert de normandie bavarian bergkase say cheese fromage st. agur blue cheese boursin queso cow. Cow feta. 
                      Cheesecake fondue cheese triangles. Cut the cheese goat hard cheese taleggio everyone loves gouda queso cheese on toast. Pecorino who moved my cheese cream cheese the big cheese pecorino port-salut croque monsieur cow. Cheese slices cottage cheese mozzarella.

                      Gouda smelly cheese cheesy feet. Feta melted cheese halloumi roquefort cheesecake cauliflower cheese cottage cheese stinking bishop. Cream cheese cheesy feet cheeseburger say cheese cheesy feet edam bavarian bergkase fromage frais. Stinking bishop camembert de normandie rubber cheese taleggio feta cheese on toast roquefort babybel. Mozzarella cheesy grin stinking bishop.

                      Rubber cheese cheese slices dolcelatte. Pepper jack jarlsberg smelly cheese hard cheese parmesan edam everyone loves mascarpone. Mozzarella manchego rubber cheese babybel bavarian bergkase danish fontina cheddar airedale. Cauliflower cheese goat chalk and cheese manchego hard cheese melted cheese.

                      Airedale cheese strings brie. Cottage cheese feta boursin edam ricotta cheese strings chalk and cheese mascarpone. Jarlsberg camembert de normandie everyone loves cheese and biscuits hard cheese cheeseburger melted cheese bavarian bergkase. Cut the cheese pecorino cream cheese taleggio emmental airedale halloumi.
        `
        }
      ]
    }
  },
  computed: {

    // randomBackground: function() {
    //   return this.dummyBackgrounds[Math.floor(Math.random() * (this.dummyBackgrounds.length - 0) ) + 0]
    // }
  },
  methods: {
    setNewRandomTopic: function () {
      
      this.activeTopic = this.getRandomTopic();
    },
    getRandomTopic: function() {
      return this.dummyTopics[Math.floor(Math.random() * (this.dummyTopics.length - 0) ) + 0]
    }
  },
  created() {
    this.setNewRandomTopic()
  }
}
</script>

<style>
* {
  font-family: 'Montserrat', sans-serif;
  color: #2c3e50;
}
body {
  background: #eeeeee;
}
#app {
  /* font-family: 'Avenir', Helvetica, Arial, sans-serif; */
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
#bodyWrapper {
  /* display: grid;
  grid-template-columns: repeat(12, 1fr); */
}

#topicWrapper {
  /* animation: fadeIn 0.5s ease-in ;
  -webkit-animation: fadeIn 0.5s ease-in ;
  -moz-animation: fadeIn 0.5s ease-in ;
  -ms-animation: fadeIn 0.5s ease-in ;
  -o-animation: fadeIn 0.5s ease-in ; */
  grid-column: 4/9;
}

#categoriesWrapper {

  max-width: 45rem;
}
/* @keyframes fadeIn {
  from {opacity: 0;}
  to {opacity: 1;}
}
@-moz-keyframes fadeIn {
  from {opacity: 0;}
  to {opacity: 1;}
}
@-webkit-keyframes fadeIn {
  from {opacity: 0;}
  to {opacity: 1;}
}
@-ms-keyframes fadeIn {
  from {opacity: 0;}
  to {opacity: 1;}
}
@-o-keyframes fadeIn {
  from {opacity: 0;}
  to {opacity: 1;}
}
@keyframes fadeOut {
  from {opacity: 1;}
  to { opacity: 0;}
} */


</style>
