<!-- src/App.vue -->
<template>
  <div id="app">
    <VenteForm @vente-enregistree="ajouterVente" />
    <VentesTable :ventes="ventes" />
  </div>
</template>

<script>
import VenteForm from './components/VenteForm.vue';

export default {
  components: {
    VenteForm,
    VentesTable,
  },
  data() {
    return {
      ventes: [],
    };
  },
  methods: {
    ajouterVente(vente) {
      this.ventes.push(vente);
    },
  },
};
</script>
