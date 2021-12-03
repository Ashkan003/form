<template>
  <div id="app">
    <head>
      <link
        href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css"
        rel="stylesheet"
        integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3"
        crossorigin="anonymous"
      />
    </head>
    <div>
      <form>
        <div v-for="(input, i) in inputs" :key="i">
          <label :for="input.id">{{ input.label }}</label>
          <div>
            <input
              v-if="
                input.type === 'text' ||
                input.type === 'number' ||
                input.type === 'date'
              "
              :type="input.type"
              :id="input.id"
              :placeholder="input.placeholder"
              v-model="fieldsData[input.id]"
            />
            <input
              v-if="input.type === 'checkbox'"
              :type="input.type"
              :id="input.id"
              :placeholder="input.placeholder"
              v-model="fieldsData[input.id]"
            />
            <select
              aria-label="Default select example"
              v-if="input.type === 'select'"
              id=""
              v-model="fieldsData[input.id]"
            >
              <option v-for="(option, i) in input.options" :key="i">
                {{ option.value }}
              </option>
            </select>
          </div>
        </div>
        <fieldset v-for="input in inputs" :key="input.id">
          <legend v-if="input.type === 'radio'"></legend>
          <div v-if="input.type === 'radio'">
            <div v-for="(option, i) in input.options" :key="i">
              <input
                type="radio"
                name="gridRadios"
                :id="i"
                :value="option.value"
                v-model="fieldsData[input.id]"
              />
              <label :for="i">{{ option.text }}</label>
            </div>
          </div>
        </fieldset>
        <div v-for="input in inputs" :key="input.id">
          <div v-if="input.type === 'checkboxMultiple'">
            <div v-for="(option, i) in input.options" :key="i">
              <div>
                <input
                  type="checkbox"
                  :id="i"
                  :value="option.value"
                  v-model="fieldsData[input.id]"
                />
                <label :for="i">{{ option.text }}</label>
              </div>
            </div>
          </div>
        </div>
        <button
          type="submit"
          class="btn btn-primary"
          @click.prevent="submitHandler()"
        >
          Submit
        </button>
      </form>
    </div>
    <router-view />
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputs: [
        { type: "text", placeholder: "عنوان", label: "عنوان", id: "title" },
        {
          type: "select",
          placeholder: "",
          label: "تاریخ تولد",
          id: "birthday",
          options: [
            { value: "0", text: "صفر" },
            { value: "1", text: "یک" },
          ],
        },
        {
          type: "checkboxMultiple",
          placeholder: "",
          label: "check",
          id: "check",
          options: [
            { value: "0", text: "صفر" },
            { value: "1", text: "یک" },
          ],
        },
        {
          type: "checkbox",
          placeholder: "",
          label: "check",
          id: "check1",
        },
        {
          type: "radio",
          placeholder: "",
          label: "radio button",
          id: "radio",
          options: [
            { value: "0", text: "صفر" },
            { value: "1", text: "یک" },
          ],
        },
      ],
      fieldsData: [],
    };
  },
  methods: {
    submitHandler() {
      JSON.stringify({
        type: this.type,
        placeholder: this.placeholder,
        label: this.label,
        id: this.id,
        options: this.options,
      });
      console.log(this.fieldsData);
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  margin: 0;
  background: #eee !important;
}

form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.8em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
</style>
