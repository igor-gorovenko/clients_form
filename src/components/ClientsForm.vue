<template>
	<div class="main">
		<div class="container">
			<form class="create-new-client" @submit="createClients">
				<h1 class="title">Создание нового пользователя</h1>
				<h3 class="title">Атрибуты формы</h3>
				<div class="user-details">
					<div class="form-group">
						<label for="last-name">Фамилия</label>
						<input id="last-name" class="form-control" v-model.trim="form.lastName" />
					</div>

					<div class="form-group">
						<label for="first-name">Имя</label>
						<input
							id="first-name"
							class="form-control is-invalid"
							type="text"
							v-model.trim="form.firstName"
						/>
						<p class="invalid-feedback">Error</p>
					</div>

					<div class="form-group">
						<label for="middle-name">Отчество</label>
						<input
							id="middle-name"
							class="form-control"
							type="text"
							v-model.trim="form.middleName"
						/>
					</div>

					<div class="form-group">
						<label for="">Дата рождения</label>
						<input class="form-control" type="text" />
					</div>

					<div class="form-group">
						<label for="">Номер телефона</label>
						<input class="form-control" type="number" />
					</div>

					<label for="">Пол</label>

					<div class="form-group gender">
						<input class="radio" type="radio" value="male" id="male" v-model="form.gendere" />
						<label for="male">Мужчина</label>
						<input class="radio" type="radio" value="female" id="female" v-model="form.gendere" />
						<label for="female">Женщина</label>
					</div>

					<div class="form-group">
						<label for="client">Группа клиентов</label>
						<select id="client" class="form-control" v-model="form.yourClients" multiple>
							<option v-for="(client, index) in clients" :key="index">
								{{ client.label }}
							</option>
						</select>
					</div>

					<div class="form-group">
						<label for="doctor">Лечащий врач</label>
						<select id="doctor" class="form-control" v-model="form.doctor">
							<option v-for="(doctor, index) in doctors" :value="doctor.value" :key="index">
								{{ doctor.label }}
							</option>
						</select>
					</div>

					<div class="form-group">
						<input id="checkbox" type="checkbox" v-model="form.agreeWithDontSendMessages" />
						<label class="label" for="checkbox">Не отправлять СМС</label>
					</div>

					<button class="button">Создать аккаунт</button>
				</div>
			</form>
		</div>
	</div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength } from 'vuelidate/lib/validators'

export default {
	mixins: [validationMixin],
	data() {
		return {
			form: {
				firstName: '',
				lastName: '',
				middleName: '',
				doctor: 'Ivanov',
				yourClients: ['VIP'],
				agreeWithDontSendMessages: false,
				gendere: 'male',
			},

			doctors: [
				{
					label: 'Иванов',
					value: 'Ivanov',
				},
				{
					label: 'Захаров',
					value: 'Zakharov',
				},
				{
					label: 'Чернышева',
					value: 'Chernysheva',
				},
			],
			clients: [
				{
					label: 'VIP',
					value: 'VIP',
				},
				{
					label: 'Проблемные',
					value: 'trable',
				},
				{
					label: 'ОМС',
					value: 'CHI',
				},
			],
		}
	},
	validations: {
		form: {
			firstName: {
				required,
				minLength: minLength(5),
			},
			lastName: { required },
			middleName: { required },
		},
	},
	methods: {
		createClients() {
			this.$v.form.touch()
			if (this.$v.form.$error) {
				console.log('Валидация прошла успешно')
			}
		},
	},
}
</script>

<style scoped>
* {
	font-size: 18px;
	line-height: 133%;
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	border: none;
}
h1 {
	font-size: 2.5em;
	line-height: 133%;
	margin: 16px 0 32px 0;
}
h3 {
	font-size: 1.5em;
	margin: 24px 0 24px 0;
}
.main {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 40px;
}
.container {
	max-width: 640px;
	width: 100%;
	background: #f7f7f7;
	padding: 40px 56px;
}
.container .title {
	font-size: 32;
	font-weight: 500;
	position: relative;
}

.form-group {
	width: 100%;
	margin: 8px 0 32px 0;
}

.form-group #client {
	height: max-content;
	padding: 16px 0 0 24px;
}

.form-group.gender label {
	margin: 0 24px 0 0;
}

.form-group .radio {
	margin: 0 8px 16px 0;
}

.form-group #checkbox {
	width: 24px;
	border: none;
}

.form-group .form-control {
	width: 100%;
	background: none;
	border: 1px solid rgb(178, 178, 189);
	box-sizing: border-box;
	height: 44px;
	padding: 0 0 0 16px;
	margin: 8px 0 0 0;
}

.button {
	box-sizing: border-box;
	margin: 32px 0 24px 0;
	width: 100%;
	height: 56px;
	border: none;
	color: white;
	background: cornflowerblue;
}
</style>
