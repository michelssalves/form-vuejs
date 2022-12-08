<template>
	<div id="app">
		<h1>Registrar Reclamação</h1>
		<div class="conteudo">
			<form class="painel">
				<div class="cabecalho">Formulário</div>
				<Rotulo nome="E-mail">
					<input type="text" v-model="user.email">
					<!--lazy é equivalente ao blur
						<input type="text" v-model.lazy="user.email">
						trim retira os espaços em branco	
						<input type="text" v-model.trim="user.email">
						number transforma o valor em numerico e não string	e so converte se tiver um valor numerico valido
						<input type="text" v-model.number="user.email">
					-->
				</Rotulo>
				<Rotulo nome="Senha">
					<input type="password" v-model="user.password">
				</Rotulo>
				<Rotulo nome="Age">
					<input type="number" v-model="user.age">
				</Rotulo>
				<Rotulo nome="Message">
					<textarea name="" cols="30" rows="5" v-model="message"></textarea>
				</Rotulo>
				<Rotulo nome="Problem Characteristics">
					<span class="mr-4"><input type="checkbox" v-model="features" value="reproduzivel"> Reproduzível</span>
					<span><input type="checkbox" value="intermitente" v-model="features"> Intermitente</span>
				</Rotulo>
				<Rotulo nome="Which Product?">
					<span class="mr-4"><input type="radio" value="web" v-model="product"> Web</span>
					<span class="mr-4"><input type="radio" value="mobile" v-model="product"> Mobile</span>
					<span><input type="radio" value="outro" v-model="product"> Outro</span>
				</Rotulo>
				<Rotulo nome="Priority">
					<select v-model="priority">
						<option v-for="priority in prioritys"
						:key="priority.code"
						:value="priority.code"
					
						>{{ priority.name }}</option>
				
					</select>
				</Rotulo>
				<Rotulo nome="First Complaint?">
					<Escolha />
				</Rotulo>
				<hr>
				<button>Enviar</button>
			</form>
			<div class="painel">
				<div class="cabecalho">Resultado</div>
				<Rotulo nome="E-mail">
					<span>{{ user.email }}</span>
				</Rotulo>
				<Rotulo nome="Password">
					<span>{{ user.password }}</span>
				</Rotulo>
				<Rotulo nome="Age">
					<span>{{ user.age }}</span>
				</Rotulo>
				<Rotulo nome="Message">
					<!--style="white-space: pre;" preserva os espaços do text area-->
					<span style="white-space: pre;">{{ message }}</span>
				</Rotulo>
				<Rotulo nome="Check the Options">
					<span>
						<ul>
							<!--a letra c recebe os valores do array features -->
							<li v-for="c in features" :key="c"> {{ c }}</li>
						</ul>
					</span>
				</Rotulo>
				<Rotulo nome="Which product?">
					<span>{{ product }}</span>
				</Rotulo>
				<Rotulo nome="Priority">
					<span> {{ priority }}</span>
				</Rotulo>
				<Rotulo nome="First Complaint?">
					<span>???</span>
				</Rotulo>
			</div>
		</div>
	</div>
</template>

<script>
import Rotulo from './components/Rotulo.vue'
import Escolha from './components/Escolha.vue'

export default {
	name: 'app',
	components: { Rotulo, Escolha },
	data(){
		return{
			message: '',
			features: [],
			priority: 1,
			prioritys: [
				{code: 1, name: 'Low'},
				{code: 2, name: 'Medium'},
				{code: 3, name: 'High'},
			],
			product: 'wbe',
			user: {
				email: '',
				password: '',
				age: ''
			}
		}
	},
	//temporizador
	created(){
		setTimeout(() => {
			this.email = ''
		}, 5000 )
	}
}
</script>

<style>

body {
	background-color: #ECECEC;
}

#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;

	display: flex;
	flex-direction: column;
}

.conteudo {
	display: flex;
}

.painel {
	flex: 1;
	background: #FFF;
	margin: 0px 10px;
	padding: 20px;
	border: 1px solid #AAA;
	border-radius: 5px;
}

.painel .cabecalho {
	width: 100%;
	background-color: #DDD;
	padding: 10px 0px;
	border-radius: 5px;
	font-size: 1.4rem;
}

#app form button {
	float: right;
	margin: 10px 0px;
	padding: 10px 20px;
	font-size: 1.4rem;
	border-radius: 5px;
	color: #FFF;
	background-color: #2196F3;
}

#app h1 {
	font-weight: 200;
	margin: 20px;
	padding: 0;
}

.mr-4 {
	margin-right: 40px;
}
</style>
