<template>
  <div class="home">
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
</style>

<script>
export default {
  data: function() {
    return {
      message: "People_App",
      message_2: "Superheros",
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
  created: function() {},
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
