<template>
  <div>
    <Messeger :msg="msg" v-show="msg" />
    <div>
      <form id="burger-form" @submit="createBurguer">
        <div class="input-container">
          <label class="input-container__label" for="name">Your Name</label>
          <input
            class="input-container__input"
            type="text"
            id="name"
            name="name"
            v-model="name"
            placeholder="Inset your name"
          />
        </div>

        <div class="input-container">
          <label class="input-container__label" for="bread "
            >Select your bread:</label
          >
          <select
            class="input-container__select"
            name="bread"
            id="bread"
            v-model="bread"
          >
            <option value="">types of bread</option>
            <option v-for="bread in breads" :key="bread.id" :value="bread.type">
              {{ bread.type }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <label class="input-container__label" for="meat"
            >Select your meat:</label
          >
          <select
            class="input-container__select"
            name="meat"
            id="meat"
            v-model="meat"
          >
            <option value="">Types of meats</option>
            <option value="meat">Meat</option>

            <option v-for="meat in meats" :key="meat.id" :value="meat.type">
              {{ meat.type }}
            </option>
          </select>
        </div>

        <div class="input-container input-container__checkbox">
          <label class="input-container__label" for="options">Options:</label>

          <div class="checkbox-container">
            <div
              class="checkbox-container__path"
              v-for="option in optionsdata"
              :key="option.id"
            >
              <input
                class="input-container__input checkbox-container__checkbox"
                type="checkbox"
                name="options"
                v-model="options[option.type]"
                :value="option.type"
              />
              <span class="checkbox-container__span">{{ option.type }}</span>
            </div>
          </div>
        </div>
        <div class="input-container">
          <input
            class="input-container__input input-container__submit"
            type="submit"
            value="Finish your order!"
          />
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import Messeger from "./Messeger.vue";

export default {
  name: "BurgerForm",
  data() {
    return {
      breads: null,
      meats: null,
      optionsdata: null,
      name: null,
      bread: null,
      meat: null,
      stats: "requested",
      messeger: null,
      options: {},
      msg: null,
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();
      this.breads = data.breads;
      this.meats = data.meats;
      this.optionsdata = data.options;
    },
    async createBurguer(e) {
      e.preventDefault();
      const selectedOptions = Object.keys(this.options).filter(
        (option) => this.options[option]
      );
      const data = {
        nome: this.name,
        bread: this.bread,
        meat: this.meat,
        optionsdata: selectedOptions,
        stats: "Requested",
      };
      const dataJson = JSON.stringify(data);
      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });
      const res = await req.json();
      console.log(res);
      this.msg = `Your order N ${res.id} has been requested`;
      setTimeout(() => {
        this.msg = "";
      }, 3000);
      this.name = "";
      this.bread = "";
      this.meat = "";
      this.options = {};
    },
  },
  mounted() {
    this.getIngredients();
  },
  components: { Messeger },
};
</script>
<style scoped>
#burger-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}
.input-container__label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #fcba03;
}

.input-container__select,
.input-container__input {
  padding: 5px 10px;
  width: 300px;
}
.checkbox-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.checkbox-container__path {
  display: flex;
  align-items: flex-start;
  width: 50%;
  margin-bottom: 20px;
}
.checkbox-container__checkbox {
  display: flex;
  width: auto;
}
.checkbox-container__span {
  margin-left: 6px;
  font-weight: Bold;
}
.input-container__submit {
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
.input-container__submit:hover {
  background-color: transparent;
  color: #222;
}
</style>
