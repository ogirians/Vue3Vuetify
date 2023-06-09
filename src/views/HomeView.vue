<script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <v-container fluid>
    <v-text-field
      v-model="tanggal_from"
      type = "date"
      :rules="nameRules"
      :counter="10"
      label="tanggal mulai"
      required
    ></v-text-field>
    <v-text-field
      v-model="tanggal_to"
      type = "date"
      :rules="nameRules"
      :counter="10"
      label="tanggal selesai"
      required
    ></v-text-field>
      <h1 class="mb-5"> 
        Table laporan
      </h1>
      <v-data-table
        v-model:items-per-page="itemsPerPage"
        :headers="headers"
        :items="desserts"
        item-value="name"
        class="elevation-1"
      ></v-data-table>

    <v-btn theme="light" color="primary" class="my-5" @click="sendIo">klikk</v-btn>

  </v-container>
</template>

<script>
import PusherClient from 'pusher-js';
import io from 'socket.io-client';

export default {
  data () {
      return {
        socket : io('http://172.9.1.157:3233'),
        tanggal_from : '',
        tanggal_to : '',
        itemsPerPage: 5,
        headers: [
          {
            title: 'Dessert (100g serving)',
            align: 'start',
            sortable: false,
            key: 'name',
          },
          { title: 'Calories', align: 'end', key: 'calories' },
          { title: 'Fat (g)', align: 'end', key: 'fat' },
          { title: 'Carbs (g)', align: 'end', key: 'carbs' },
          { title: 'Protein (g)', align: 'end', key: 'protein' },
          { title: 'Iron (%)', align: 'end', key: 'iron' },
        ],
        desserts: [
          {
            name: 'Frozen Yogurt',
            calories: 159,
            fat: 6.0,
            carbs: 24,
            protein: 4.0,
            iron: '1',
          },
          {
            name: 'Jelly bean',
            calories: 375,
            fat: 0.0,
            carbs: 94,
            protein: 0.0,
            iron: '0',
          },
          {
            name: 'KitKat',
            calories: 518,
            fat: 26.0,
            carbs: 65,
            protein: 7,
            iron: '6',
          },
          {
            name: 'Eclair',
            calories: 262,
            fat: 16.0,
            carbs: 23,
            protein: 6.0,
            iron: '7',
          },
          {
            name: 'Gingerbread',
            calories: 356,
            fat: 16.0,
            carbs: 49,
            protein: 3.9,
            iron: '16',
          },
          {
            name: 'Ice cream sandwich',
            calories: 237,
            fat: 9.0,
            carbs: 37,
            protein: 4.3,
            iron: '1',
          },
          {
            name: 'Lollipop',
            calories: 392,
            fat: 0.2,
            carbs: 98,
            protein: 0,
            iron: '2',
          },
          {
            name: 'Cupcake',
            calories: 305,
            fat: 3.7,
            carbs: 67,
            protein: 4.3,
            iron: '8',
          },
          {
            name: 'Honeycomb',
            calories: 408,
            fat: 3.2,
            carbs: 87,
            protein: 6.5,
            iron: '45',
          },
          {
            name: 'Donut',
            calories: 452,
            fat: 25.0,
            carbs: 51,
            protein: 4.9,
            iron: '22',
          },
        ],
      }
    },
  computed: {
      virtualDesserts () {
        return [...Array(10000).keys()].map(i => {
          const dessert = { ...this.desserts[i % 10] }
          dessert.name = `${dessert.name} #${i}`

          return dessert
        })
      },
    },
  created() {
    // const socket = io('http://localhost:3233/');

    this.socket.on('chat message', (data) => {
      alert(data);
    });


    // PusherClient.logToConsole = true;
    // var pusherclient = new PusherClient('4ed2cd399a138fc25a0d', {
    //   cluster: 'ap1'
    // });
    //   var channel = pusherclient.subscribe('my-channel');
    //   channel.bind('my-event', function(data) {
    //     alert(JSON.stringify(data));
    // });
  },
  methods : {
    sendIo(){
      // const socketSend = io('http://localhost:3233/');
      this.socket.emit("chat message", "hello broadcast");
    }
  }

}
</script>