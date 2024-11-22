<template>
	<div class="card converter-card">
		<div class="card-body">
			<h3 class="card-title text-center">Conversor de Unidades</h3>
			<input
				type="number"
				v-model.number="value"
				class="form-control mb-3"
				placeholder="Ingrese el valor a convertir"
			/>
			<div class="form-group mb-3">
				<label for="categorySelect">Categoría:</label>
				<select
					v-model="selectedCategory"
					class="form-control"
					id="categorySelect"
					@change="updateUnits"
				>
					<option
						v-for="category in categories"
						:key="category.name"
						:value="category.name"
					>
						{{ category.name }}
					</option>
				</select>
			</div>
			<div class="form-group mb-3">
				<label for="fromUnit">Convertir desde:</label>
				<select v-model="fromUnit" class="form-control" id="fromUnit">
					<option v-for="unit in availableUnits" :key="unit" :value="unit">
						{{ unit }}
					</option>
				</select>
			</div>
			<div class="form-group mb-3">
				<label for="toUnit">Convertir a:</label>
				<select v-model="toUnit" class="form-control" id="toUnit">
					<option v-for="unit in availableUnits" :key="unit" :value="unit">
						{{ unit }}
					</option>
				</select>
			</div>
			<button @click="convert" class="btn btn-primary w-100 mb-3">
				Convertir <i class="fas fa-exchange-alt"></i>
			</button>
			<div v-if="result !== null" class="mt-3 text-center result">
				<strong>Resultado: </strong> {{ result }}
			</div>
		</div>
	</div>
</template>

<script>
import convert from "convert-units";

export default {
	data() {
		return {
			value: null,
			selectedCategory: "Longitud",
			fromUnit: "",
			toUnit: "",
			result: null,
			categories: [
				{
					name: "Longitud",
					units: ["mm", "cm", "m", "km", "in", "ft", "yd", "mi"],
				},
				{
					name: "Área",
					units: ["mm2", "cm2", "m2", "ha", "km2", "in2", "ft2", "ac", "mi2"],
				},
				{
					name: "Volumen",
					units: [
						"mm3",
						"cm3",
						"ml",
						"l",
						"kl",
						"m3",
						"km3",
						"tsp",
						"Tbs",
						"in3",
						"fl-oz",
						"cup",
						"pnt",
						"qt",
						"gal",
						"ft3",
						"yd3",
					],
				},
				{
					name: "Velocidad",
					units: ["m/s", "km/h", "mph", "knot"],
				},
				{
					name: "Masa",
					units: ["mcg", "mg", "g", "kg", "mt", "oz", "lb", "t"],
				},
				{
					name: "Presión",
					units: ["Pa", "hPa", "kPa", "MPa", "bar", "torr", "psi", "atm"],
				},
				{
					name: "Temperatura",
					units: ["C", "F", "K", "R"],
				},
			],
			availableUnits: [],
		};
	},
	created() {
		this.updateUnits();
	},
	methods: {
		updateUnits() {
			const category = this.categories.find(
				(cat) => cat.name === this.selectedCategory
			);
			this.availableUnits = category.units;
			this.fromUnit = this.availableUnits[0];
			this.toUnit = this.availableUnits[1];
		},
		convert() {
			try {
				this.result = convert(this.value).from(this.fromUnit).to(this.toUnit);
			} catch (e) {
				alert(
					"Error en la conversión. Asegúrese de que las unidades seleccionadas sean compatibles."
				);
			}
		},
	},
};
</script>

<style scoped>
.converter-card {
	border-radius: 15px;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
	background: #ffffff33;
	color: #fff;
}
.result {
	font-size: 1.5rem;
	color: #00ff7f;
}
</style>
