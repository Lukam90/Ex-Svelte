<script>
import Modal from "./Modal.svelte";
import AddPersonForm from "./AddPersonForm.svelte";

let showModal = false;

let people = [
	{ id: 1, name: "yoshi", beltColour: "black", age: 25 },
	{ id: 2, name: "mario", beltColour: "orange", age: 45 },
	{ id: 3, name: "luigi", beltColour: "brown", age: 35 }
]

const handleClick = (id) => {
	people = people.filter((person) => person.id != id)
};

const toggleModal = () => {
	showModal = ! showModal;
};
</script>

<Modal message="Hey, I'm a prop value!" {showModal} on:click={toggleModal}>
	<h3>Add a New Person</h3>

	

	<div slot="title">
		<h3>Add a New Person</h3>
	</div>
</Modal>

<main>
	<button on:click|once={toggleModal}>Open Modal</button>

	{#each people as person (person.id)}
	<div>
		<h4>{person.name}</h4>

		{#if person.beltColour === "black"}
		<p><strong>MASTER</strong></p>
		{/if}

		<p>{person.age} years old, {person.beltColour} belt</p>

		<button on:click={handleClick(person.id)}>delete</button>
	</div>
	{:else}
		<p>There are no people to show.</p>
	{/each}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>