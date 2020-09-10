<template>
	<div class="cabezera">
		<div class="titulo">
			<h1>Filtro de Gatitos bonitos</h1>
		</div>
		<div class="main">
			<div class="option">
				<label>Título:</label>
				<label>Filtro:</label>
				<label>Color:</label>
				<label>Tamaño:</label>
			</div>
			<div class="inputS">
				<input v-model="title" />
				<select v-model="filterSelect">
					<option disabled selected>Selecciona</option>
					<option @click="filterSelect = item" v-for="item in filter" :key="item.id" :value="item">
						{{ item }}
					</option>
				</select>
				<div class="selectC">
					<select class="color" v-model="colorSelect">
						<option disabled selected>Selecciona</option>
						<option @click="colorSelect = item" v-for="item in colors" :key="item.id" :value="item">
							{{ item }}
						</option>
					</select>
					<div :style="{ 'background-color': this.colorSelect }" class="circulo"></div>
				</div>
				<input v-model.number="size" type="number" min="1" />
			</div>
		</div>
		<div class="gif-Cat">
			<button @click="getCat">Quiero ver mi gatito</button>
			<div>
				<img v-if="imgSrc" :src="imgSrc" alt="GatoSinFoto" />
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'HomePrincipal',
	data() {
		return {
			title: '',
			imgSrc: '',
			filter: ['negative', 'blur', 'mono', 'sepia', 'paint', 'pixel'],
			colors: ['black', 'gray', 'red', 'green', 'yellow', 'blue'],
			size: null,
			filterSelect: 'Selecciona:',
			colorSelect: 'Selecciona:',
		};
	},
	methods: {
		getCat() {
			this.imgSrc = `https://cataas.com/cat/gif/says/${this.title}?filter=${this.filterSelect}&color=${this.colorSelect}&size=${this.size}`;
		},
	},
};
</script>

<style lang="scss">
body {
	padding: 0;
	margin: 0;
}
.cabezera {
	display: grid;
	grid-template-columns: 1fr;
	grid-template-rows: 1fr 2fr 3fr;
	background-color: #add8e6;
}
.titulo,
.select,
.gif-Cat {
	display: flex;
	flex-flow: column wrap;
	justify-content: center;
	text-align: center;
}
.titulo {
	margin: 50px 200px;
	h1 {
		font-size: 50px;
	}
}
.main {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	grid-template-rows: 100%;
	background-color: #f08080;
	.option,
	.inputS {
		display: flex;
		flex-flow: column wrap;
		justify-content: center;
	}
	.option {
		align-content: flex-end;
		label {
			margin: 12px;
			text-align: right;
			font-size: 20px;
			color: white;
		}
	}
	.selectC {
		display: flex;
		flex-flow: row wrap;
		justify-content: space-between;
		align-content: center;
		.color {
			width: 50%;
		}
		.circulo {
			width: 20px;
			height: 20px;
			border-radius: 50%;
			margin: 10px;
		}
	}
	.inputS {
		align-content: flex-start;
		input,
		select {
			margin: 10px;
			font-size: 1.3rem;
		}
	}
}
.gif-Cat {
	justify-content: start;
	padding: 2rem 30%;
	button {
		line-height: 2;
		font-size: 1.25rem;
		border-radius: 5px;
		margin-bottom: 2rem;
	}
}
</style>
