<template>
  <div class="container-fluid">
    <div class="row align-items-center">
      <div class="col-6 px-5 fs-5 pt-1 text-uppercase">
        <h1>Boolflix</h1>
      </div>
      <div class="col-6 px-5">
        <div class="input-group">
          <input
            type="text"
            class="form-control"
            placeholder="Cerca un film o una serie"
            aria-label="Cerca un film o una serie"
            aria-describedby="basic-addon2"
            v-model="search"
            @keyup.enter="$emit('performSearch', search)"
          />
          <div class="input-group-append">
            <button
              class="btn btn-outline-secondary"
              type="button"
              @click="cerca"
            >
              Cerca
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AppSearch",
  data() {
    return {
      search: "",
    };
  },
  methods: {
    cerca() {
      this.$emit("performSearch", this.search);
      this.search = "";
    },
  },
};
</script>

<style lang="scss"></style>
