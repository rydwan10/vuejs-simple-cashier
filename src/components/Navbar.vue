<template>
  <nav class="navbar navbar-rounded navbar-expand-lg navbar-light bg-light mb-1">
    <div class="container">
      <img
        class="navbar-brand d-inline-block align-top"
        width="40px"
        height
        src="../assets/logo.png"
      />
      <a class="navbar-brand" href="#">Cashier System</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item active px-1 py-1">
            <router-link class="btn btn-sm nav-link" to="/">Dashboard</router-link>
          </li>
          <!-- <li class="nav-item active px-1 py-1">
            <router-link class="btn btn-sm nav-link" to="/about">About</router-link>
          </li>-->
          <li class="nav-item active px-1 py-1">
            <router-link class="btn btn-sm nav-link" to="/history">History</router-link>
          </li>
          <li class="nav-item active px-1 py-1">
            <a class="btn btn-sm nav-link" href="#">Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
};
</script>

<style scoped>
ul > li {
  width: 100%;
}
ul > li > a {
  font-family: Arial, Helvetica, sans-serif;
  background: rgba(9, 156, 209, 0.877) !important;
}

@media (max-width: 995px) {
  ul {
    align-items: center;
  }
  ul > li {
    width: 90%;
  }
}
</style>