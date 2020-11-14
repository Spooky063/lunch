<template>
	{{ mealtime.name }}
	<div v-if="filteredItems.length > 0">
		<div v-for="items in filteredItems" :key="items.id">
			<div v-for="item in orderedItems(items.items)" :key="item.id">
				<input type="checkbox" id="checkbox" v-model="item.possible" />
				{{ item.name }}
				<span>{{ item.info }}</span>
				<button @click="confirm(`Voulez-vous vraiment supprimer ce plat ?`)">X</button>
			</div>
		</div>
		<button>Ajoute un autre plat</button>
		<button>Déplacer à demain</button>
		<button>Déplacer à semaine pro</button>
	</div>
	<div v-else>
		<div>Rien au menu ce soir :(</div>
		<button>Ajoute ton premier plat</button>
	</div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

interface ItemsData {
	week: number;
	slot: number;
	items: ItemData[];
}

interface ItemData {
	id: number;
	name: string;
	info: string;
	possible: boolean;
	position?: number;
}

const items = [
	{
		week: 0,
		slot: 0,
		items: [
			{
				id: 0,
				name: 'Quiche au saumon',
				info: 'http://monsitedecuisine.com/recette/quiche-au-saumon',
				possible: false,
				position: 1,
			},
			{
				id: 0,
				name: 'Soupe de légumes',
				info: 'Il manque des patates',
				possible: false,
				position: 0,
			},
		],
	},
	{
		week: 0,
		slot: 1,
		items: [
			{
				id: 0,
				name: 'Burger spécial',
				info: "#Le complete signifie que j'ai tous les ingrédients pour faire ce repas",
				possible: true,
				position: 0,
			},
		],
	},
	{
		week: 0,
		slot: 6,
		items: [
			{
				id: 0,
				name: 'Gratin dauphinois',
				info: '',
				possible: false,
				position: 0,
			},
		],
	},
];

interface SlotData {
	id: number;
	name: string;
	position: number;
}

const Slot = defineComponent({
	name: 'Slot',

	props: {
		mealtime: {
			type: Object as PropType<SlotData>,
			required: true,
		},
	},

	methods: {
		confirm: function (text: string) {
			return window.confirm(text);
		},

		orderedItems: function (items: ItemData[]) {
			return items.sort((a, b) => {
				return a.position - b.position;
			});
		},
	},

	setup({ mealtime }) {
		function filteredItems() {
			return items.filter((item: ItemsData) => {
				return item.slot === mealtime.id;
			});
		}

		return { filteredItems: filteredItems() };
	},
});

export default Slot;
</script>
