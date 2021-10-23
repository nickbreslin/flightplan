<template>
  <div class="container-fluid">
    <div class="alert alert-secondary mt-3 text-center shadow">
      <h1 class="text-uppercase m-0">Flight Plan</h1>
    </div>

    <div class="row">
      <div class="col-sm-8">
        <div class="alert alert-success mb-3 text-center shadow">
          <h2 class="text-uppercase m-0">Game Board</h2>
        </div>
        <div class="alert alert-secondary mb-3 text-center shadow">
          <h2 class="text-uppercase m-0">instructions</h2>
        </div>
      </div>
      <div class="col-sm-4">
        <div class="card shadow mb-3 shadow">
          <div class="card-header h3 text-uppercase text-center">planes</div>
          <div class="card-body text-center"></div>
        </div>
        <div class="card shadow mb-3 shadow">
          <div class="card-header h3 text-uppercase text-center">
            Available Destinations
          </div>
          <div class="card-body text-center"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Main",
  components: {},
};
</script>
