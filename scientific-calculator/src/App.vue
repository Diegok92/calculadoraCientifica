<template>
	<div id="app">
		<header class="text-center p-5">
			<h1>Calculadora Científica Profesional</h1>
			<p class="lead">
				Realiza cálculos avanzados y convierte unidades de manera eficiente,
				todo en un solo lugar.
			</p>
		</header>

		<div class="container">
			<div class="row">
				<div class="col-md-6 mb-4">
					<CalculatorComponent />
				</div>
				<div class="col-md-6 mb-4">
					<ConverterComponent />
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import CalculatorComponent from "./components/CalculatorComponent.vue";
import ConverterComponent from "./components/ConverterComponent.vue";

export default {
	name: "App",
	components: {
		CalculatorComponent,
		ConverterComponent,
	},
};
</script>

<style>
body {
	background: linear-gradient(to right, #6a11cb, #2575fc);
	font-family: "Roboto", sans-serif;
	color: #fff;
}

p {
	color: white;
}
</style>
