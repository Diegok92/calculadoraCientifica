<template>
	<div class="card calculator-card">
		<div class="card-body">
			<h3 class="card-title text-center">Calculadora Científica</h3>
			<input type="text" v-model="input" class="form-control mb-3" />
			<div class="button-grid">
				<button
					@click="appendInput(char)"
					v-for="char in buttons"
					:key="char"
					class="btn btn-outline-light"
				>
					{{ char }}
				</button>
				<button @click="calculateResult" class="btn btn-success">
					<i class="fas fa-equals"></i>
				</button>
				<button @click="clearLast" class="btn btn-warning">
					<i class="fas fa-backspace"></i>
				</button>
				<button @click="clearInput" class="btn btn-danger">
					<i class="fas fa-trash"></i>
				</button>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			input: "",
			buttons: [
				"7",
				"8",
				"9",
				"/",
				"4",
				"5",
				"6",
				"*",
				"1",
				"2",
				"3",
				"-",
				"0",
				".",
				"+",
				"sin(",
				"cos(",
				"tan(",
				"log(",
				"sqrt(",
				"(",
				")",
			],
		};
	},
	methods: {
		appendInput(char) {
			this.input += char;
		},
		clearInput() {
			this.input = "";
		},
		clearLast() {
			this.input = this.input.slice(0, -1);
		},
		calculateResult() {
			try {
				this.input = eval(this.input).toString();
			} catch (e) {
				alert("Error en la expresión");
			}
		},
	},
};
</script>

<style scoped>
.calculator-card {
	border-radius: 15px;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
	background: #ffffff33;
	color: #fff;
	animation: slideIn 1s ease-in-out;
}

.button-grid {
	display: grid;
	grid-template-columns: repeat(4, 1fr);
	gap: 10px;
}

button {
	height: 50px;
	font-size: 1.2rem;
}

@keyframes slideIn {
	from {
		transform: translateY(20px);
		opacity: 0;
	}
	to {
		transform: translateY(0);
		opacity: 1;
	}
}
</style>
