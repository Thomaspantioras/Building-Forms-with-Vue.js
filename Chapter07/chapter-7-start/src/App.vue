<template>
  <div id="app" class="container py-4">
    <div class="row">
      <div class="col-12">
        <form>
          <Renderer 
            v-for="(element, name) in schema" 
            :key="name" 
            :element="element"
            v-model="form[name]"
          />
          <div class="form-group">
            <button 
              @click.prevent="onSubmit" 
              type="submit" 
              class="btn btn-primary"
            >
              Submit
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
// import schema from "@/data/schema.json";
import { parse } from "@/libraries/Api";
import axios from "axios";
import Renderer from "@/components/Renderer";
export default {
  name: "app",
  components: { Renderer },
  data() {
    return {
      // schema: schema,
      schema: {},
      form: {}
    };
  },
  created() {
    axios
      .get("http://localhost:3000/schema")
      .then(response => {
        this.schema = parse(response.data);
      })
      .catch(error => {
        console.log("Network error", error);
      });
  },
  methods: {
    onSubmit() {
      console.log("Submit clicked");
    }
  }
};
</script>