<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  let nvDepense = {
    nom: "",
    montant: "",
  };

  function handleSubmit() {
    if (nvDepense.nom.trim() !== "") {
      dispatch("nv-depense", {
        nom: nvDepense.nom,
        montant: nvDepense.montant,
      });
      nvDepense.nom = nvDepense.montant = "";
    }
  }
</script>

<form on:submit|preventDefault={handleSubmit} class="form-group my-4">
  <label for="depense">Nom de la Depense</label>
  <input
    bind:value={nvDepense.nom}
    class="form-control"
    type="text"
    name="depense"
    id="depense" />
  <label for="montant">Montant</label>
  <input
    bind:value={nvDepense.montant}
    class="form-control"
    type="number"
    name="montant"
    id="montant" />
  <button class="btn btn-primary mt-3">Ajouter une dépense</button>
</form>
