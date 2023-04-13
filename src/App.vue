<template>
  <div class="row d-flex justify-content-around">
    <h1 class="align-self-center">Ironhack contacts</h1>
    <div class="column d-flex justify-content-around">
    <button @click="addRandomContact" type="button" class="btn btn-primary">Add Contact</button>
    <button @click="sortByName" type="button" class="btn btn-primary">Sort by Name</button>
    <button @click="sortByPopularity" type="button" class="btn btn-primary">Sort by Popularity</button>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Picture</th>
          <th scope="col">Name</th>
          <th scope="col">Popularity</th>
          <th scope="col">Won Oscar</th>
          <th scope="col">Won Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in contactsList" :key="contact.id">
          <td class="w-25">
            <img :src="contact.pictureUrl" alt="contact.name" class="img-fluid img-thumbnail" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity }}</td>
          <td v-if="contact.wonOscar" class="w-25">
            <img src="./assets/trophy.png" alt="trophy logo" class="img-fluid trophy">
          </td>
          <td v-if="contact.wonEmmy" class="w-25">
            <img src="./assets/trophy.png" alt="trophy logo" class="img-fluid trophy">
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import contacts from "./contacts.json";

export default {
  name: "App",
  data() {
    return {
      contactsList: [],
    }
  },
  mounted() {
    this.contactsList = contacts.slice(0, 5)
  },
  methods: {
    addRandomContact() {
      const filteredContacts = contacts.filter(contact => !this.contactsList.includes(contact));
      if (filteredContacts.length === 0) {
        return;
      }
      const randomIndex = Math.floor(Math.random() * filteredContacts.length);
      const randomContact = filteredContacts[randomIndex];
      this.contactsList.push(randomContact);
    },

    sortByName() {
      this.contactsList.sort(function (a, b) {
        if (a.name < b.name) {
          return -1;
        }
        if (a.name > b.name) {
          return 1;
        }
        return 0;
      });

    },

    sortByPopularity() {
      this.contactsList.sort(function (a, b) {
        if (a.popularity > b.popularity) {
          return -1;
        }
        if (a.popularity < b.popularity) {
          return 1;
        }
        return 0;
      });
    }


  }
};
</script>

<style>
.trophy {
  width: 60px
}
</style>
