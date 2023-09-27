<template>
  <div>
    <p>messeger</p>
    <div>
      <form id="burger-form">
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
            <option value="wholeGrain">whole grain</option>
          </select>
        </div>

        <div class="input-container">
          <label class="input-container__label" for="protain"
            >Select your protain:</label
          >
          <select
            class="input-container__select"
            name="protain"
            id="protain"
            v-model="protain"
          >
            <option value="">Types of protain</option>
            <option value="meat">Meat</option>
          </select>
        </div>

        <div class="input-container input-container__checkbox">
          <label class="input-container__label" for="options">Options:</label>

          <div class="checkbox-container">
            <div class="checkbox-container__path">
              <input
                class="input-container__input checkbox-container__checkbox"
                type="checkbox"
                name="options"
                v-model="options"
                value="salami"
              />
              <span class="checkbox-container__span">Salami</span>
            </div>
            <div class="checkbox-container__path">
              <input
                class="input-container__input checkbox-container__checkbox"
                type="checkbox"
                name="options"
                v-model="options"
                value="salami"
              />
              <span class="checkbox-container__span">Salami</span>
            </div>
            <div class="checkbox-container__path">
              <input
                class="input-container__input checkbox-container__checkbox"
                type="checkbox"
                name="options"
                v-model="options"
                value="salami"
              />
              <span class="checkbox-container__span">Salami</span>
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
export default {
  name: "BurgerForm",
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
