<template>
	<v-container>
		<v-layout row wrap mb-1>
			<v-spacer></v-spacer>
			<v-flex xs2 d-flex align-center>
				<v-select
					solo
					hide-details
					label="Toggle Columns"
					:items="headers"
					item-text="text"
					return-object
					v-model="filteredHeaders"
					multiple
					cache-items
				>
					<template v-slot:selection="{ item, index }">
						<span v-if="index === 1" class="grey--text caption">{{ filteredHeaders.length }} Columns Visible</span>
					</template>
				</v-select>
			</v-flex>
		</v-layout>

		<v-data-table :headers="filteredHeaders" :items="mockData" class="elevation-1" item-key="id"> </v-data-table>
	</v-container>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";

@Component
export default class DataGrid extends Vue {
	private headers = [
		{ text: "#", value: "id" },
		{ text: "First Name", value: "first_name" },
		{ text: "Last Name", value: "last_name" },
		{ text: "Email", value: "email" },
		{ text: "Gender", value: "gender" },
		{ text: "Ip Address", value: "ip_address" }
	];
	private filteredHeaders = this.headers;
	private mockData = [
		{
			id: 1,
			first_name: "Katrinka",
			last_name: "Douris",
			email: "kdouris0@tripod.com",
			gender: "Female",
			ip_address: "156.100.63.139"
		},
		{
			id: 2,
			first_name: "Prentice",
			last_name: "Heliot",
			email: "pheliot1@wsj.com",
			gender: "Male",
			ip_address: "106.129.158.182"
		},
		{
			id: 3,
			first_name: "Mahala",
			last_name: "Yuryatin",
			email: "myuryatin2@blinklist.com",
			gender: "Female",
			ip_address: "220.57.210.228"
		},
		{
			id: 4,
			first_name: "Roarke",
			last_name: "McGennis",
			email: "rmcgennis3@prweb.com",
			gender: "Male",
			ip_address: "6.151.170.23"
		},
		{
			id: 5,
			first_name: "Lewie",
			last_name: "Losebie",
			email: "llosebie4@istockphoto.com",
			gender: "Male",
			ip_address: "68.205.227.165"
		},
		{
			id: 6,
			first_name: "Armand",
			last_name: "Udie",
			email: "audie5@washington.edu",
			gender: "Male",
			ip_address: "91.26.16.23"
		},
		{
			id: 7,
			first_name: "Karoly",
			last_name: "Crus",
			email: "kcrus6@nydailynews.com",
			gender: "Male",
			ip_address: "112.92.211.190"
		},
		{
			id: 8,
			first_name: "Arlene",
			last_name: "Paynter",
			email: "apaynter7@simplemachines.org",
			gender: "Female",
			ip_address: "195.152.218.130"
		},
		{
			id: 9,
			first_name: "Heinrick",
			last_name: "Arkill",
			email: "harkill8@ft.com",
			gender: "Male",
			ip_address: "200.227.50.61"
		},
		{
			id: 10,
			first_name: "Federico",
			last_name: "Tack",
			email: "ftack9@a8.net",
			gender: "Male",
			ip_address: "19.221.72.20"
		}
	];

	@Watch("filteredHeaders")
	onFilteredChanged(items: [], oldItems: []) {
		if (items === oldItems) return;
		items.sort((a: any, b: any) => {
			return this.headers.indexOf(a) - this.headers.indexOf(b);
		});
	}
}
</script>
