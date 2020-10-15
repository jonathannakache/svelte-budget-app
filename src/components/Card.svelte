<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  export let nom;
  export let montant;
  export let id;

  function handleDelete() {
    dispatch("suppr-element", { id: id });
  }
</script>

<style>
  .card {
    position: relative;
  }

  .trash img {
    width: 30px;
    cursor: pointer;
  }
  .trash {
    position: absolute;
    top: 20px;
    right: 20px;
    font-size: 25px;
  }
</style>

<div class="card my-4">
  <div class="card-body">
    <h3>{nom}</h3>
    <p>{montant} Euros</p>
    <i class="trash"><img
        src="ressources/trash-solid.svg"
        on:click={handleDelete}
        alt="trash" /></i>
  </div>
</div>
