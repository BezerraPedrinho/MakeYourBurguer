<template>
  <Messeger :msg="msg" v-show="msg" />
  <div class="burger-table">
    <div>
      <div class="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Client:</div>
        <div>Bread:</div>
        <div>Meat</div>
        <div>Options:</div>
        <div>Actions:</div>
      </div>
    </div>
    <div class="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.name }}</div>
        <div>{{ burger.bread }}</div>
        <div>{{ burger.meat }}</div>
        <div>
          <ul>
            <li v-for="(option, index) in burger.optionsdata" :key="index">
              {{ option }}
            </li>
          </ul>
        </div>
        <div>
          <select
            name="stats"
            class="stats"
            @change="updatedBurger($event, burger.id)"
          >
            <option value="">Select</option>
            <option
              v-for="stat in stats"
              :key="stat.id"
              :value="stat.type"
              :selected="burger.stats === stat.type"
            >
              {{ stat.type }}
            </option>
          </select>
          <button @click="deleteBurger(burger.id)" class="delete-btn">
            Cancel
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Messeger from "./Messeger.vue";
export default {
  name: "DashBoard",
  data() {
    return {
      burgers: null,
      burger_id: null,
      stats: [],
      msg: null,
    };
  },
  components: {
    Messeger,
  },
  methods: {
    async getOrders() {
      const req = await fetch("http://localhost:3000/burgers");
      const data = await req.json();
      this.burgers = data;
      console.log(data);
      this.getStats();
    },
    async getStats() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();
      this.stats = data;
      console.log(data);
    },
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE",
      });
      const res = await req.json();
      this.msg = `Your order it was canceled`;

      setTimeout(() => {
        this.msg = "";
      }, 3000);
      this.getOrders();
    },
    async updatedBurger(event, id) {
      const option = event.target.value;
      const dataJson = JSON.stringify({ stats: option });
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: { "Content-type": "application/json" },
        body: dataJson,
      });
      const res = await req.json();
      this.msg = `Your order ${res.id} updated to ${res.stats}`;

      setTimeout(() => {
        this.msg = "";
      }, 3000);

      console.log(res);
    },
  },

  mounted() {
    this.getOrders();
  },
};
</script>

<style scoped>
.burger-table {
  min-width: 1090px;
  max-width: 1200px;
  margin: 0 auto;
}
.burger-table-heading,
.burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
}

.burger-table-heading {
  font-weight: bold;
  padding: 12px;
  border-bottom: 3px double #333;
}

.burger-table-heading div,
.burger-table-row div {
  width: 19%;
}

.burger-table-row {
  width: 100%;
  padding: 12px;
  border-bottom: 1px solid #ccc;
}

.burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
}
select {
  padding: 12px 6px;
  margin-left: 12px;
}

.delete-btn {
  background-color: #222;
  font-weight: bold;
  border: 2px solid #222;
  color: #fcba03;
  padding: 10px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: 0.5s;
}
.delete-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>
