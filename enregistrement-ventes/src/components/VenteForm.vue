<template>
  <div class="container">
    <h2>Enregistrement de Vente</h2>
    <form @submit.prevent="enregistrerVente">
      <div class="mb-3">
        <label for="reference" class="form-label">Référence du produit</label>
        <input type="text" class="form-control" id="reference" v-model="nouvelleVente.reference">
      </div>
      <div class="mb-3">
        <label for="designation" class="form-label">Désignation</label>
        <input type="text" class="form-control" id="designation" v-model="nouvelleVente.designation">
      </div>
      <div class="mb-3">
        <label for="quantite" class="form-label">Quantité vendue</label>
        <input type="number" class="form-control" id="quantite" v-model.number="nouvelleVente.quantite">
      </div>
      <div class="mb-3">
        <label for="prix" class="form-label">Prix de vente</label>
        <input type="number" class="form-control" id="prix" v-model.number="nouvelleVente.prix">
      </div>
      <button type="submit" class="btn btn-primary">Enregistrer</button>
    </form>

    <div v-if="message" class="alert alert-success mt-3">{{ message }}</div>

    <h2>Ventes enregistrées</h2>
    <table class="table table-striped mt-3">
      <thead>
        <tr>
          <th>Référence</th>
          <th>Désignation</th>
          <th>Quantité</th>
          <th>Prix</th>
          <th>Total</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(vente, index) in ventes" :key="index">
          <td>{{ vente.reference }}</td>
          <td>{{ vente.designation }}</td>
          <td>{{ vente.quantite }}</td>
          <td>{{ vente.prix }}</td>
          <td>{{ vente.quantite * vente.prix }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const nouvelleVente = ref({
  reference: '',
  designation: '',
  quantite: 0,
  prix: 0,
});

const ventes = ref([]);
const message = ref('');

function enregistrerVente() {
  if (nouvelleVente.value.reference && nouvelleVente.value.designation && nouvelleVente.value.quantite > 0 && nouvelleVente.value.prix > 0) {
    ventes.value.push({ ...nouvelleVente.value });
    message.value = 'Vente enregistrée avec succès !';
    nouvelleVente.value = { reference: '', designation: '', quantite: 0, prix: 0 }; 
  } else {
    message.value = 'Veuillez remplir tous les champs correctement.';
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  margin-top: 20px;
}
</style>
