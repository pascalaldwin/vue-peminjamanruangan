<!-- Bagian buat Tampilan Calendarnya - Dari API Vuetify !-->
<template>
  <div>
    <v-sheet
      tile
      height="54"
      color="grey lighten-3"
      class="d-flex"
    >
      <v-btn
        icon
        class="ma-2"
        @click="$refs.calendar.prev()"
      >
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <v-select
        v-model="type"
        :items="types"
        dense
        outlined
        hide-details
        class="ma-2"
        label="type"
      ></v-select>
      <v-select
        v-model="mode"
        :items="modes"
        dense
        outlined
        hide-details
        label="event-overlap-mode"
        class="ma-2"
      ></v-select>
      <v-select
        v-model="weekday"
        :items="weekdays"
        dense
        outlined
        hide-details
        label="weekdays"
        class="ma-2"
      ></v-select>
      <v-spacer></v-spacer>
      <v-btn
        icon
        class="ma-2"
        @click="$refs.calendar.next()"
      >
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
    </v-sheet>
    <v-sheet height="600">
      <v-calendar
        ref="calendar"
        v-model="value"
        :weekdays="weekday"
        :type="type"
        :events="events"
        :event-overlap-mode="mode"
        :event-overlap-threshold="30"
        :event-color="getEventColor"
        @change="getEvents"
      ></v-calendar>
    </v-sheet>
  </div>
</template>

<script>
  export default {
    //script buat default calendarnya
    data:() =>({
      today: new Date().toISOString().substr(0,10),
      focus: new Date().toISOString().substr(0,10),
      type:"month",
      typeToLabel: {
        month:"Month",
        week: "Week",
        day: "Day",
        "4day":"4 Days"
      },
      name:null,
      details:null,
      start:null,
      end:null,
      color:"#1976D2",
      currentlyEditing:null,
      selectedEvent:{},
      selectedElement:null,
      selectedOpen:false,
      event:[],
      dialog:false
    }),
    mounted(){
      this.getEvents(); //declare buat manggil event
    },
    methods: {
      async getEvents(){
        let snapshot = await db.collection('vue-peminjamanlab').get(); //nunggu info dari DB
        let events = [];
        snapshot.forEach(doc => {
          console.log(doc);
        });
      }
    }
  }
</script>