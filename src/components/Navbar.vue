<script>
export default {
  name: "Navbar",
};
</script>

<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container-fluid d-flex align-items-center">
      <!-- Lien vers Superhéro -->
      <router-link class="navbar-brand me-3" to="/">Superhéro</router-link>

      <!-- Lien vers Détail Superhéro -->
      <router-link class="navbar-brand" to="/detail/1"
        >Détail Superhéro</router-link
      >
      <router-link class="navbar-brand" to="/SuperPowerMatcher"
        >SuperPower Matcher</router-link
      >

      <!-- Bouton pour la navigation mobile -->
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNav"
        aria-controls="navbarNav"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <!-- Autres liens de navigation (optionnels) -->
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <li class="nav-item"></li>
        </ul>
      </div>
    </div>
  </nav>
</template>
