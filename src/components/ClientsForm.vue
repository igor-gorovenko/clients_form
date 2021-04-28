<template>
	<div class="main">
		<div class="container">
			<form class="create-new-client" @submit.prevent="createClients">
				<h1 class="title">Создание нового пользователя</h1>
				<h3 class="title">Основная информация</h3>
				<div class="user-details">
					<div class="form-group">
						<label for="last-name">Фамилия*</label>
						<input
							id="last-name"
							class="form-control"
							:class="$v.form.lastName.$error ? 'is-invalid' : ''"
							type="text"
							v-model.trim="$v.form.lastName.$model"
						/>
						<p
							v-if="$v.form.lastName.$dirty && !$v.form.lastName.required"
							class="invalid-feedback"
						>
							Обязательное поле!
						</p>
						<p
							v-if="$v.form.lastName.$dirty && !$v.form.lastName.minLength"
							class="invalid-feedback"
						>
							Здесь должно быть 3 или более символов!
						</p>
					</div>

					<div class="form-group">
						<label for="first-name">Имя*</label>
						<input
							id="first-name"
							class="form-control"
							:class="$v.form.firstName.$error ? 'is-invalid' : ''"
							type="text"
							v-model.trim="$v.form.firstName.$model"
						/>
						<p
							v-if="$v.form.firstName.$dirty && !$v.form.firstName.required"
							class="invalid-feedback"
						>
							Обязательное поле!
						</p>
						<p
							v-if="$v.form.firstName.$dirty && !$v.form.firstName.minLength"
							class="invalid-feedback"
						>
							Здесь должно быть 3 или более символов!
						</p>
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
						<label for="date-birthd">Дата рождения*</label>
						<input
							id="date-birthd"
							class="form-control"
							:class="$v.form.dateBirthd.$error ? 'is-invalid' : ''"
							type="date"
							v-model.trim="$v.form.dateBirthd.$model"
						/>

						<p
							v-if="$v.form.dateBirthd.$dirty && !$v.form.dateBirthd.required"
							class="invalid-feedback"
						>
							Обязательное поле!
						</p>
					</div>

					<div class="form-group">
						<label for="mobile-number">Номер телефона*</label>
						<input
							id="mobile-number"
							class="form-control"
							:class="$v.form.mobileNumber.$error ? 'is-invalid' : ''"
							type="number"
							v-model.trim="$v.form.mobileNumber.$model"
						/>
						<p
							v-if="$v.form.mobileNumber.$dirty && !$v.form.mobileNumber.required"
							class="invalid-feedback"
						>
							Обязательное поле!
						</p>
						<p
							v-if="$v.form.mobileNumber.$dirty && !$v.form.mobileNumber.minLength"
							class="invalid-feedback"
						>
							Номер должен начинаться с '+7' <br />
							и содержать 11 цифр.
						</p>
						<p
							v-if="$v.form.mobileNumber.$dirty && !$v.form.mobileNumber.maxLength"
							class="invalid-feedback"
						>
							Номер должен начинаться с '+7' <br />
							и содержать не более 11 цифр.
						</p>
					</div>

					<label for="">Пол</label>

					<div class="form-group gender">
						<input class="radio" type="radio" value="male" id="male" v-model="form.gendere" />
						<label for="male">Мужчина</label>
						<input class="radio" type="radio" value="female" id="female" v-model="form.gendere" />
						<label for="female">Женщина</label>
					</div>

					<div class="form-group">
						<label for="client">Группа клиентов* </label>

						<select id="client" class="form-control" v-model="form.yourClients" multiple>
							<option v-for="(client, index) in clients" :key="index">
								{{ client.label }}
							</option>
						</select>

						<p>(Можно выбрать несколько.)</p>
					</div>

					<div class="form-group">
						<label for="doctor">Лечащий врач</label>
						<select id="doctor" class="form-control" v-model="form.doctor">
							<option v-for="(doctor, index) in doctors" :value="doctor.value" :key="index">
								{{ doctor.label }}
							</option>
						</select>
					</div>

					<h3 class="title">Адрес</h3>

					<div class="form-group">
						<label for="index-number">Индекс</label>
						<input id="index-number" type="number" class="form-control" />
						<p></p>
					</div>

					<div class="form-group">
						<label for="country">Страна</label>
						<input id="country" type="text" class="form-control" />
					</div>

					<div class="form-group">
						<label for="region">Область</label>
						<input id="region" type="text" class="form-control" />
					</div>

					<div class="form-group">
						<label for="city">Город*</label>
						<input
							id="city"
							class="form-control"
							:class="$v.form.yourCity.$error ? 'is-invalid' : ''"
							type="text"
							v-model.trim="$v.form.yourCity.$model"
						/>
						<p
							v-if="$v.form.yourCity.$dirty && !$v.form.yourCity.required"
							class="invalid-feedback"
						>
							Обязательное поле!
						</p>
						<p
							v-if="$v.form.yourCity.$dirty && !$v.form.yourCity.minLength"
							class="invalid-feedback"
						>
							Здесь должно быть 5 или более символов!
						</p>
					</div>

					<div class="form-group">
						<label for="street">Улица</label>
						<input id="street" type="text" class="form-control" />
					</div>

					<div class="form-group">
						<label for="house">Дом</label>
						<input id="house" type="text" class="form-control" />
					</div>

					<h3 class="title">Паспорт</h3>

					<div class="form-group">
						<label for="type-document">Тип документа*</label>

						<select id="type-document" class="form-control" v-model="form.typeDocument">
							<option v-for="(typeDocument, index) in documents" :key="index">
								{{ typeDocument.label }}
							</option>
						</select>
					</div>

					<div class="form-group">
						<label for="house">Серия</label>
						<input id="house" type="text" class="form-control" />
					</div>

					<div class="form-group">
						<label for="house">Номер</label>
						<input id="house" type="text" class="form-control" />
					</div>

					<div class="form-group">
						<label for="house">Кем выдан</label>
						<input id="house" type="text" class="form-control" />
					</div>

					<div class="form-group">
						<label for="issue-date">Дата выдачи*</label>
						<input
							id="issue-date"
							class="form-control"
							:class="$v.form.iddueDate.$error ? 'is-invalid' : ''"
							type="date"
							v-model.trim="$v.form.iddueDate.$model"
						/>

						<p
							v-if="$v.form.iddueDate.$dirty && !$v.form.iddueDate.required"
							class="invalid-feedback"
						>
							Обязательное поле!
						</p>
					</div>

					<p>*Поле обязательное для заполнения.</p>
				</div>

				<div class="form-group">
					<input id="checkbox" type="checkbox" v-model="form.agreeWithDontSendMessages" />
					<label class="label" for="checkbox">Не отправлять СМС</label>
				</div>

				<button type="submit" class="button">Создать аккаунт</button>

				<p v-if="$v.form.iddueDate.$dirty && !this.$v.form.$error">
					Клиент успешно создан!
				</p>
			</form>
		</div>
	</div>
</template>

<script>
import { validationMixin } from 'vuelidate'
import { required, minLength, maxLength } from 'vuelidate/lib/validators'

export default {
	mixins: [validationMixin],
	data() {
		return {
			form: {
				firstName: '',
				lastName: '',
				middleName: '',
				dateBirthd: '',
				doctor: 'Ivanov',
				yourClients: ['VIP'],
				agreeWithDontSendMessages: false,
				gendere: 'male',
				mobileNumber: '',
				typeDocument: 'Паспорт',
				yourCity: '',
				iddueDate: '',
			},

			documents: [
				{
					label: 'Паспорт',
					value: 'Passport',
				},
				{
					label: 'Свидетельство о рождении',
					value: 'Birth certificate',
				},
				{
					label: 'Водительское удостоверение',
					value: 'Driver is license',
				},
			],

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
				minLength: minLength(3),
			},

			lastName: {
				required,
				minLength: minLength(3),
			},

			dateBirthd: {
				required,
			},

			mobileNumber: {
				required,
				minLength: minLength(11),
				maxLength: maxLength(11),
			},

			yourCity: {
				required,
				minLength: minLength(5),
			},

			iddueDate: {
				required,
			},
		},
	},
	methods: {
		createClients() {
			this.$v.form.$touch()
			if (!this.$v.form.$error) {
				console.log('Валидация прошла успешно')
			}
		},
	},
}
</script>

<style scoped>
* {
	font-size: 1em;
	line-height: 133%;
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	border: none;
}

h1 {
	font-size: 2.5em;
	font-weight: 500;
	line-height: 133%;
	margin: 16px 0 32px 0;
}

h3 {
	font-size: 1.5em;
	font-weight: 500;
	margin: 24px 0 24px 0;
}

.main {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 40px;
	background: #f7f7f7;
}

.container {
	max-width: 800px;
	width: 100%;
	background: #ffffff;
	padding: 40px 56px;
}

.form-group {
	font-size: 1.2em;
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

.form-group p {
	margin: 8px 0 0 0;
	font-size: 1em;
}

.invalid-feedback {
	color: red;
}

.form-group .is-invalid {
	border-color: red;
}

@media screen and (max-width: 768px) {
	h1 {
		font-size: 2em;
		margin: 16px 0 24px 0;
	}

	h3 {
		font-size: 1.3em;
		margin: 32px 0 20px 0;
	}

	.main {
		padding: 20px;
	}

	.container {
		max-width: 800px;
		width: 100%;
		background: #ffffff;
		padding: 20px;
	}

	.form-group {
		font-size: 1em;
		margin: 8px 0 20px 0;
	}

	.form-group #client {
		padding: 16px 0 0 16px;
	}

	.form-group .form-control {
		width: 100%;
		background: none;
		border: 1px solid rgb(178, 178, 189);
		box-sizing: border-box;
		height: 40px;
		padding: 0 0 0 16px;
		margin: 8px 0 0 0;
	}

	.button {
		box-sizing: border-box;
		margin: 24px 0;
		width: 100%;
		height: 56px;
		border: none;
		color: white;
		background: cornflowerblue;
	}

	.form-group p {
		margin: 8px 0 0 0;
		font-size: 1em;
	}

	.invalid-feedback {
		color: red;
	}

	.form-group .is-invalid {
		border-color: red;
	}
}

@media screen and (max-width: 480px) {
	* {
		font-size: 16px;
		line-height: 133%;
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		border: none;
	}

	h1 {
		font-size: 1.6em;
		font-weight: 500;
		line-height: 133%;
		margin: 16px 0 24px 0;
	}

	h3 {
		font-size: 1.15em;
		font-weight: 500;
		margin: 16px 0 16px 0;
	}

	.main {
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 0px;
		background: #fff;
	}

	.container {
		max-width: 480px;
		width: 100%;
		background: #ffffff;
		padding: 16px 16px;
	}

	.form-group {
		font-size: 1em;
		width: 100%;
		margin: 8px 0 16px 0;
	}

	.form-group #client {
		height: max-content;
		padding: 16px 0 0 16px;
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

	.form-group p {
		margin: 8px 0 0 0;
		font-size: 1em;
	}

	.invalid-feedback {
		color: red;
	}

	.form-group .is-invalid {
		border-color: red;
	}
}
</style>
