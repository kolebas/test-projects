<template>
  <div id="app">
    <StartTable
      msg="Привет я таблица"
      :headers="headers"
      :rows="rows"
      :paggintaionProps="5"
    />
  </div>
</template>

<script>
import StartTable from "./components/StartTable.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    StartTable,
  },
  data: () => ({
    headers: [
      { id: 0, title: "Дата", filtered: false },
      { id: 1, title: "Название", filtered: true, filterFiled: "title" },
      { id: 2, title: "Количество", filtered: true, filterFiled: "value" },
      { id: 3, title: "Расстояние", filtered: true, filterFiled: "distance" },
    ],
    rows: [
      {
        id: 0,
        title: "Забег в сочи",
        date: Date.now().toString(),
        value: 25,
        distance: 250,
      },
      {
        id: 1,
        title: "Забег в честь дня города",
        date: Date.now(),
        value: 15,
        distance: 50,
      },
      {
        id: 2,
        title: "Юбилейный спринт",
        date: Date.now(),
        value: 5,
        distance: 100,
      },
      { id: 3, title: "Забег", date: Date.now(), value: 99, distance: 750 },

      {
        id: 4,
        title: "Забег в сочи",
        date: Date.now().toString(),
        value: 25,
        distance: 250,
      },
      {
        id: 5,
        title: "Забег в честь дня города",
        date: Date.now(),
        value: 15,
        distance: 50,
      },
      {
        id: 6,
        title: "Юбилейный спринт 6",
        date: Date.now(),
        value: 5,
        distance: 100,
      },
      { id: 7, title: "Забег", date: Date.now(), value: 99, distance: 750 },

      {
        id: 8,
        title: "Забег в сочи",
        date: Date.now().toString(),
        value: 25,
        distance: 250,
      },
      {
        id: 9,
        title: "Забег в честь дня города",
        date: Date.now(),
        value: 15,
        distance: 50,
      },
      {
        id: 10,
        title: "Юбилейный спринт 10",
        date: Date.now(),
        value: 5,
        distance: 100,
      },
      { id: 11, title: "Забег", date: Date.now(), value: 99, distance: 750 },

      {
        id: 12,
        title: "Забег в сочи",
        date: Date.now().toString(),
        value: 25,
        distance: 250,
      },
      {
        id: 13,
        title: "Забег в честь дня города",
        date: Date.now(),
        value: 15,
        distance: 50,
      },
      {
        id: 14,
        title: "Юбилейный спринт 14",
        date: Date.now(),
        value: 5,
        distance: 100,
      },
      { id: 3, title: "Забег", date: Date.now(), value: 99, distance: 750 },

      {
        id: 0,
        title: "Забег в сочи",
        date: Date.now().toString(),
        value: 25,
        distance: 250,
      },
      {
        id: 1,
        title: "Забег в честь дня города",
        date: Date.now(),
        value: 15,
        distance: 50,
      },
      {
        id: 2,
        title: "Юбилейный спринт",
        date: Date.now(),
        value: 5,
        distance: 100,
      },
      { id: 3, title: "Забег", date: Date.now(), value: 99, distance: 750 },
    ],
  }),
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      const options = {
        method: "POST",
        url: "https://trains.p.rapidapi.com/",
        headers: {
          "content-type": "application/json",
          "X-RapidAPI-Key":
            "eee4b99860msh703ba67a330f308p179199jsnf60a93e846e5",
          "X-RapidAPI-Host": "trains.p.rapidapi.com",
        },
        data: '{"search":"Rajdhani"}',
      };
      axios
        .request(options)
        .then((response) => {
          response.data.forEach(element => {
            this.rows.push(
              {
                id: element.data.id,
                title: element.name,
                date: element.data.arriveTime,
                distance: element.data.to_id,
                value: element.train_num
              }
            )
          });
          console.log(this.rows)
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: center;
}
</style>
