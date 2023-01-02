<template lang="pug">
.container
	h1 Login
	form(@submit.prevent='efetuarLogin')
		.form-group
			label E-mail
			input.form-control(type='email', v-model='usuario.email')
		
		.form-group
			label Senha
			input.form-control(type='password', v-model='usuario.senha')

		button.btn.btn-primary.btn-block(type='submit') Entrar
</template>

<script lang="js">
export default{
	data(){
		return{
			usuario:{}
		}
	},
	methods:{
		efetuarLogin(){
			this.$http.post('auth/login',this.usuario)
				.then(response => {
					console.log(response)
					localStorage.setItem('token', response.data.access_token)
					this.$router.push({ name: 'gerentes' })
				})
				.catch(error => console.log(error))
		}
	}
}
</script>