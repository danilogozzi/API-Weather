<template v-slot:default>
  <v-container>
    <v-row>
      <v-col cols="12">
        <v-simple-table class="cx-wheater">
          <thead>
            <tr>
              <th class="text-left">City</th>
              <th class="text-left">Temp</th>
              <th class="text-left">Min</th>
              <th class="text-left">Max</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(w, id) in wheaters" :key="id">
              <td>
                {{ w.name }}
              </td>
              <td v-for="(desc, id) in w.weather" :key="id">
                {{ desc.description }}
              </td>
              <td>
                {{ w.main.temp_min }}
              </td>
              <td>
                {{ w.main.temp_max }}
              </td>
            </tr>
          </tbody>
          <br />
          <div>
            <v-autocomplete
              v-model="valueCity"
              :items="items"
              dense
              filled
              label="City"
            >
            </v-autocomplete>
            <v-btn @click="getWheater()" rounded color="success mr-5" dark>
              Add City
            </v-btn>
            <v-btn @click="removeWheater()" rounded color="error" dark>
              Remove City
            </v-btn>
          </div>
        </v-simple-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
// @ is an alias to /srcs
import axios from "axios";

export default {
  data() {
    return {
      valueCity: null,
      choiceUser: "",
      items: [
        "Alabama",
        "Alaska",
        "American Samoa",
        "Arizona",
        "Arkansas",
        "California",
        "Colorado",
        "Connecticut",
        "Delaware",
        "District Of Columbia",
        "Federated States Of Micronesia",
        "Florida",
        "Georgia",
        "Guam",
        "Hawaii",
        "Idaho",
        "Illinois",
        "Indiana",
        "Iowa",
        "Kansas",
        "Kentucky",
        "Louisiana",
        "Maine",
        "Marshall Islands",
        "Maryland",
        "Massachusetts",
        "Michigan",
        "Minnesota",
        "Mississippi",
        "Missouri",
        "Montana",
        "Nebraska",
        "Nevada",
        "New Hampshire",
        "New Jersey",
        "New Mexico",
        "New York",
        "North Carolina",
        "North Dakota",
        "Northern Mariana Islands",
        "Ohio",
        "Oklahoma",
        "Oregon",
        "Palau",
        "Pennsylvania",
        "Puerto Rico",
        "Rhode Island",
        "South Carolina",
        "South Dakota",
        "Tennessee",
        "Texas",
        "Utah",
        "Vermont",
        "Virgin Islands",
        "Virginia",
        "Washington",
        "West Virginia",
        "Wisconsin",
        "Wyoming",
      ],
      wheaters: []
    };
  },
  methods: {
    removeWheater() {
      this.choiceUser = this.valueCity;
      this.wheaters.splice(this.wheaters.indexOf(this.wheaters),1)
},
    getWheater() {
      this.choiceUser = this.valueCity;
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.choiceUser}, US&appid=3279a157d3415d50d8ee506b681b3727&lang=pt_br&units=imperial`
        )
        .then((res) => {
          this.wheaters.push(res.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style>
.cx-wheater{
  max-width: 20rem;
  min-width: 15rem;
  border: 1px solid #0003;
  border-radius: 15px;
  height: 100%;
  padding: 1rem;
}
</style>
