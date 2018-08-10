<template>
  <div class="home">
     <div id="map"></div>
    <h2>{{ message }}</h2>
    <h3>{{ message_2 }}</h3>

    <h3>Add a SuperHerO</h3>

     <div>
       Name : <input type="text" v-model="newPerson.name">
       <br><br>
       Bio : <input type="text" v-model="newPerson.bio">
       <br><br>
       <button v-on:click="add_hero()">Add_a_SuperHero</button>

     </div>

     <h2>Number_of_Heros: {{ people.length }}</h2>

    <div v-for = "person in people">
       <h2 v-on:click="toggleBio(person)">{{ person.name }}</h2>
        <p v-if = "person.bioVisible"> {{ person.bio }} </p>
        <button v-on:click="delete_hero(person)">Delete_Hero</button>
    </div>
  </div>
</template>

<style>
.strike {
  text-decoration: line-through;
}

#map {
  height: 500px;
}

</style>

<script>
  /* global google */
export default {
  data: function() {
    return {
      message: "People_App",
      message_2: "Superheros",
      places:[
        {
          name: "Chennai" ,
          latitude:13.0827,
          longitude:80.2707,
          description: "Chennai, on the Bay of Bengal in eastern India, is the capital of the state of Tamil Nadu. The city is home to Fort St. George, built in 1644 and now a museum showcasing the city’s roots as a British military garrison and East India Company trading outpost, when it was called Madras. Religious sites include Kapaleeshwarar Temple, adorned with carved and painted gods, and St. Mary’s, a 17th-century Anglican church."


        },

         {
           name: "Chicago",
          latitude:41.8781,
          longitude:87.6298,
          description:"Chicago, on Lake Michigan in Illinois, is among the largest cities in the U.S. Famed for its bold architecture, it has a skyline punctuated by skyscrapers such as the iconic John Hancock Center, 1,451-ft. Willis Tower (formerly the Sears Tower) and the neo-Gothic Tribune Tower. The city is also renowned for its museums, including the Art Institute of Chicago with its noted Impressionist and Post-Impressionist works."

         }
         
      ],
      people: [
        {
          name: "Tony Stark",
          bio: "He is the Iron man",
          bioVisible: true
        },

        {
          name: "Clark Kent",
          bio: "He is the Super Man",
          bioVisible: true
        },

        {
          name: "Bruce Wayne",
          bio: "He is the BatMan",
          bioVisible: true
        }
      ],

      newPerson: { name: "", bio: "", bioVisible: true }
    };
  },
     mounted: function() {
    var uluru = { lat: -25.344, lng:131.036  };
    var map = new google.maps.Map(document.getElementById("map"), {
      zoom: 8,
      center: { lat: 41.8781, lng:87.6298  }
    });
    var contentString =
      '<div id="content">' +
      '<div id="siteNotice">' +
      "</div>" +
      '<h1 id="firstHeading" class="firstHeading">Uluru</h1>' +
      '<div id="bodyContent">' +
      "<p><b>Uluru</b>, also referred to as <b>Ayers Rock</b>, is a large " +
      "sandstone rock formation in the southern part of the " +
      "Northern Territory, central Australia. It lies 335&#160;km (208&#160;mi) " +
      "south west of the nearest large town, Alice Springs; 450&#160;km " +
      "(280&#160;mi) by road. Kata Tjuta and Uluru are the two major " +
      "features of the Uluru - Kata Tjuta National Park. Uluru is " +
      "sacred to the Pitjantjatjara and Yankunytjatjara, the " +
      "Aboriginal people of the area. It has many springs, waterholes, " +
      "rock caves and ancient paintings. Uluru is listed as a World " +
      "Heritage Site.</p>" +
      '<p>Attribution: Uluru, <a href="https://en.wikipedia.org/w/index.php?title=Uluru&oldid=297882194" target=_blank>' +
      "https://en.wikipedia.org/w/index.php?title=Uluru</a> " +
      "(last visited June 22, 2009).</p>" +
      "</div>" +
      "</div>";
    var infowindow = new google.maps.InfoWindow({
      content: contentString
    });
    var marker = new google.maps.Marker({
      position: uluru,
      map: map,
      title: "Uluru (Ayers Rock)"
    });
    marker.addListener("click", function() {
      infowindow.open(map, marker);
    });



     this.places.forEach(function(place){

         var pl = { lat: place.latitude, lng:place.longitude  };


            var marker = new google.maps.Marker({
            position: pl,
            map: map,
            title: place.name
           });
            var infowindow = new google.maps.InfoWindow({
              content: place.description
            });
            marker.addListener("click", function() {
              infowindow.open(map, marker);
            });


          console.log(place);
     }); 

//      var words = ["apple", "banana", "carrot"];
// words.forEach(function(word) {
//   console.log(word);
// });


  },

  methods: {
    toggleBio: function(inputPerson) {
      if (inputPerson.bioVisible === false) {
        inputPerson.bioVisible = true;
      } else {
        inputPerson.bioVisible = false;
      }
    },

    add_hero: function() {
      this.people.push(this.newPerson);
      this.newPerson = { name: "", bio: "" };
    },

    delete_hero: function(inputPerson) {
      var index = this.people.indexOf(inputPerson);
      this.people.splice(index, 1);
    }
  },
  computed: {}
};
</script>
