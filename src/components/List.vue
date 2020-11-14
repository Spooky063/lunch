<template>
	<div>Voici les plats pour la semaine</div>
	<button>Imprimer la semaine en cours</button>
	<ul>
		<div v-for="slot in slots" :key="slot.id">
			<component :is="getComponent()" :mealtime="slot"></component>
		</div>
	</ul>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import Slot from './Slot.vue';

const slots = [
	{ id: 0, name: 'lundi midi', position: 0 },
	{ id: 1, name: 'lundi soir', position: 1 },
	{ id: 2, name: 'mercredi midi', position: 2 },
	{ id: 3, name: 'mercredi soir', position: 3 },
	{ id: 4, name: 'jeudi midi', position: 4 },
	{ id: 5, name: 'jeud soir', position: 5 },
	{ id: 6, name: 'vendredi midi', position: 6 },
	{ id: 7, name: 'vendredi soir', position: 7 },
	{ id: 8, name: 'samedi midi', position: 8 },
	{ id: 9, name: 'samedi soir', position: 9 },
	{ id: 10, name: 'dimanche midi', position: 10 },
	{ id: 11, name: 'dimanche soir', position: 11 },
];

const List = defineComponent({
	name: 'List',

	setup() {
		function getComponent() {
			return Slot;
		}

		return { slots, getComponent };
	},
});

export default List;
</script>
