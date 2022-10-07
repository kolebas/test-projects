<template>
  <div>
    <h1>{{ msg }}</h1>
    <div class="filter">
      <select name="Поле" v-model="filter.field">
        <option
          v-for="(item, index) in headers.filter(
            (item) => item.filtered === true
          )"
          :key="index"
          :value="item.filterFiled"
        >
          {{ item.title }}
        </option>
      </select>

      <select name="Условие" v-model="filter.condition">
        <option
          v-for="(item, index) in filterCondition"
          :key="index"
          :value="item"
        >
          {{ item }}
        </option>
      </select>
      <input type="text" v-model="filter.value"/>
      <button @click="filteringData()">Найти</button>
    </div>
    <div class="table">
      <div class="table__header">
        <div
          class="table__header-item"
          v-for="(item, index) in headers"
          :key="index"
        >
          <p>{{ item.title }}</p>
        </div>
      </div>
      <div
        class="table__rows"
        v-for="(item, index) in rowsItems.filter(
          (el, idx) => idx <= countPagination && idx > countPagination - 5
        )"
        :key="index"
      >
        <p class="table__row-item">{{ item.date }} {{ index }}</p>
        <p class="table__row-item">{{ item.title }}</p>
        <p class="table__row-item">{{ item.value }}</p>
        <p class="table__row-item">{{ item.distance }}</p>
      </div>
      <div v-if="rowsItems.length === 0"><p>Ничего не найдено</p></div>
    </div>
    <div class="pagination_buttons">
      <button
        class="pagination_button-item"
        v-for="(item, index) in Math.floor(rowsItems.length / paggintaionProps)"
        :key="index"
        @click="setPaginationSize(item)"
      >
        {{ item }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "StartTable",
  props: {
    msg: { type: String },
    headers: { type: Array },
    rows: { type: Array },
    filterCondition: {
      type: Array,
      default: () => ["равно", "содержит", "больше", "меньше"],
    },
    paggintaionProps: { type: Number, default: 5 },
  },
  data: () => ({
    countPagination: 5,
    rowsItems: [],
    filter: {
      field: null,
      condition: null,
      value: null,
    },
  }),
  mounted() {
    this.rowsItems = this.rows;
  },
  methods: {
    setPaginationSize(val) {
      this.countPagination = this.paggintaionProps * val;
    },
    filteringData() {
      this.rowsItems = this.rows.filter((item) => {
        if (this.filter.condition === "равно") {
          return item[this.filter.field] == this.filter.value;
        } else if (this.filter.condition === "содержит") {
          return item[this.filter.field].toString().includes(this.filter.value);
        } else if (this.filter.condition === "больше") {
          return item[this.filter.field] > this.filter.value;
        } else if (this.filter.condition === "меньше") {
          return item[this.filter.field] < this.filter.value;
        }
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.filter {
  display: flex;
  margin: 0 0 10px 10px;
  gap: 5px;
}

.table {
  border: solid 1px #eceff1;
  border-radius: 5px;
  width: 1280px;
}

.table__header {
  display: flex;
  justify-content: center;
  background-color: #eceff1;
  gap: 5%;
  border-bottom: solid 2px #eeeeee;
  font-weight: 600;
}

.table__header-item {
  width: 25%;
}

.table__rows {
  display: flex;
  justify-content: center;
  background-color: #fafafa;
  gap: 5%;
  border-bottom: solid 1px #eeeeee;
}

.table__rows:last-child {
  border-bottom: none;
}

.table__rows:nth-child(2n) {
  background-color: #ffffff;
}

.table__rows:hover {
  border: solid 1px #B3E5FC;
  cursor: pointer;
}

.table__row-item {
  width: 25%;
}

.pagination_buttons {
  margin: 1% 0;
}

.pagination_button-item {
  margin-right: 5px;
}

.pagination_button-item:hover {
  cursor: pointer;
}

.pagination_button-item:last-child {
  margin-right: 0;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
