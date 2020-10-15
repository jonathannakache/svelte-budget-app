<script>
  import Form from "./Form.svelte";
  import Card from "./Card.svelte";
  import { v4 as uuidv4 } from "uuid";
  import { afterUpdate, onMount } from "svelte";

  onMount(() => {
    const dataFromStorage = localStorage.getItem("cards");
    if (dataFromStorage) {
      cards = JSON.parse(dataFromStorage);
    }
  });
  afterUpdate(() => {
    localStorage.setItem("cards", JSON.stringify(cards));
  });
  $: total = cards.reduce((acc, curr) => {
    acc = acc + curr.montant;
    return acc;
  }, 0);
  let cards = [
    {
      id: uuidv4(),
      nom: "iPad pro",
      montant: 950,
    },
    {
      id: uuidv4(),
      nom: "Macbook Pro",
      montant: 1500,
    },
  ];
  function nvDepense(event) {
    let newCard = {
      id: uuidv4(),
      nom: event.detail.nom,
      montant: event.detail.montant,
    };
    cards = [...cards, newCard];
  }

  function handleDelete(event) {
    const newCards = cards.filter((card) => card.id !== event.detail.id);
    cards = newCards;
  }
</script>

<div class="container">
  <Form on:nv-depense={nvDepense} />
  <h2>Montant total : {total} euros</h2>
  {#each cards as card (card.id)}
    <Card
      nom={card.nom}
      montant={card.montant}
      id={card.id}
      on:suppr-element={handleDelete} />
  {/each}
</div>
