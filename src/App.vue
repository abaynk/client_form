<template>
<div>
  <form @submit.prevent="submit">
    <div class='form' id='attr'>
      <legend class='title' id='main'>Общая Информация:</legend>      
      <div class='field' :class="{ 'form-group--error': !$v.surname.required }">
        <label class='form-label' for='surname'>Фамилия*:</label>
        <div class='error' v-if='!$v.surname.required'>Обязательное поле!</div>
        <input class='form-input' v-model='surname' placeholder="Иванов" @input="setSurname($event.target.value)" type='text' id='surname' name='surname'/>
      </div>
      <div class='field' :class="{ 'form-group--error': !$v.name.required }">
        <label class='form-label' for='name'>Имя*:</label>
        <div class='error' v-if='!$v.name.required'>Обязательное поле!</div>    
        <input class='form-input' v-model='name' placeholder="Иван" @input="setName($event.target.value)" type='text' id='name' name='name'/>
      </div>
      <div class='field'>
        <label class='form-label' for='fname'>Отчество:</label>
        <input class='form-input' v-model='fatherName' placeholder="Иванович" @input="setFatherName($event.target.value)" type='text' id='fname' name='fname'/>
      </div>
      <div class='field' :class="{ 'form-group--error': !$v.dateOfBirth.required }">
        <label class='form-label' for='date'>Дата рождения*:</label>
        <div class='error' v-if='!$v.dateOfBirth.required'>Обязательное поле!</div>
        <input class='form-input' v-model='dateOfBirth' @input="setDateOfBirth($event.target.value)" type='date' id='date' name='date'/>
      </div>
      <div class='field' :class="{ 'form-group--error': !$v.phone.required }">
        <label class='form-label' for='phone'>Номер телефона*:</label>
        <div class='error' v-if='!$v.phone.required'>Обязательное поле!</div>
        <div class='error' v-else-if="!$v.phone.numeric">Номер должен состоять из 11 цифр!</div>
        <div class='error' v-else-if="!$v.phone.minLength">Формат: 7XxxXxxXxXx</div>
        <input class='form-input' v-model='phone' @input="setPhone($event.target.value)" type='tel' id='phone' name='phone' placeholder='79291234567' pattern='[7][0-9]{3}[0-9]{3}[0-9]{2}[0-9]{2}'/>
      </div>
      <div class='field'>
        <legend class='form-label'>Пол:</legend>
        <label class='form-label-radio' for='male'>Мужчина</label>
        <input class='form-input-radio' v-model='gender' @input="setGender($event.target.value)" type='radio' id='male' name='gender' value='муж'/><br>
        <label class='form-label-radio' for='female'>Женщина</label>
        <input class='form-input-radio' v-model='gender' @input="setGender($event.target.value)" type='radio' id='female' name='gender' value='жен'/><br>
        <label class='form-label-radio' for='pnts'>Предпочитаю не указывать</label>
        <input class='form-input-radio' v-model='gender' @input="setGender($event.target.value)" type='radio' id='pnts' name='gender' value='конф'/><br>
        <label class='form-label-radio' for='other'>Другое</label>
        <input class='form-input-radio' v-model='gender' @input="setGender($event.target.value)" type='radio' id='other' name='gender' value='другое'/><br>
      </div>
      <div class='field' :class="{ 'form-group--error': !$v.group.required }">
        <label class='form-label' for="group">Группа клиентов*:</label><br>
        <small>(для выбора нескольких зажмите ctrl)</small><br>
        <div class='error' v-if="!$v.group.required">Обязательное поле!</div>
        <select class='form-input' v-model='group' @input="setGroup($event.target.value)" name="group" id="group" multiple size=3>
          <option value="vip">VIP</option>
          <option value="проблемные">Проблемные</option>
          <option value="ОМС">ОМС</option>
        </select> 
      </div>
      <div class='field'>
        <label class='form-label' for='doctor'>Выберите лечащего врача:</label>
        <select class='form-input' v-model='doctor' @input="setDoctor($event.target.value)" name='doctor' id='doctor'>
          <option selected value='Иванов'>Иванов</option>
          <option value='Захаров'>Захаров</option>
          <option value='Чернышева'>Чернышева</option>
        </select>
      </div>
      <div class='field'>
        <label class='form-label' for='sms'>Не отправлять СМС!</label>
        <input class='form-input-radio' type='checkbox' @input="setSms($event.target.value)" id='sms' name='sms' value='не отправлять'>
      </div>
    </div>
    <div class='form' id='adresse'>
      <legend class='title' id='adres'>Адрес:</legend>
      <div class='field'>
        <label class='form-label' for='index'>Индекс:</label>
        <input class='form-input' v-model='index' placeholder="127427" @input="setIndex($event.target.value)" type='text' id='index' name='index'/>
      </div>
      <div class='field'>
        <label class='form-label' for='country'>Страна:</label>
        <select class="form-input" v-model='country' placeholder="Россия" @input="setCountry($event.target.value)" id="country" name='country'>
          <option selected value="RU">Россия</option>
          <option value="KZ">Казахстан</option>
          <option value="UA">Украина</option>
          <option value="BLR">Беларусь</option>
          <option value="other">Другая страна</option>
        </select>
      </div>
      <div class='field'>
        <label class='form-label' for='district'>Область:</label>
        <input class='form-input' v-model='district' placeholder="Московская" @input="setDistrict($event.target.value)" type='text' id='distrct' name='district'/>
      </div>
      <div class='field' :class="{ 'form-group--error': !$v.city.required }">
        <label class='form-label' for='city'>Город*:</label>
        <div class='error' v-if="!$v.city.required">Обязательное поле!</div>
        <input class='form-input' v-model='city' placeholder="Москва" @input="setCity($event.target.value)" type='text' id='city' name='city'/>
      </div>
      <div class='field'>
        <label class='form-label' for='index'>Улица:</label>
        <input class='form-input' v-model='street' placeholder="ул. Академика Королева" @input="setStreet($event.target.value)" type='text' id='street' name='street'/>
      </div>
      <div class='field'>
        <label class='form-label' for='house'>Номер дома:</label>
        <input class='form-input' v-model='house' placeholder="12" @input="setHouse($event.target.value)" type='text' id='house' name='house'/>
      </div>
    </div>
    <div class='form' id='pass'>
      <legend class='title' id='passport'>Паспортные данные:</legend>
      <div class='field' :class="{ 'form-group--error': !$v.document.required }">
        <label class='form-label' for="doc-type">Выберите тип документа*:</label>
        <div class='error' v-if="!$v.document.required">Обязательное поле!</div>
        <select class='form-input' v-model='document' placeholder="Паспорт" @input="setDocument($event.target.value)" name="doc-type" id="doc-type" size=1>
          <option value="паспорт">Паспорт</option>
          <option value="свидетельство">Свидетельство о рождении</option>
          <option value="права">Водительские права</option>
        </select> 
      </div>
      <div class='field'>
        <label class='form-label' for='serie'>Серия документа:</label>
        <input class='form-input' v-model='serie' placeholder="P12345" @input="setSerie($event.target.value)" type='text' id='serie' name='serie'/>
      </div>
      <div class='field'>
        <label class='form-label' for='docNumber'>Номер документа:</label>
        <input class='form-input' v-model='docNumber' placeholder="N12345" @input="setDocNumber($event.target.value)" type='text' id='docNumber' name='docNumber'/>
      </div>
      <div class='field'>
        <label class='form-label' for='issuedBy'>Орган выдачи:</label>
        <input class='form-input' v-model='issuedBy' placeholder="Орган выдачи" @input="setIssuedBy($event.target.value)" type='text' id='issuedBy' name='issuedBy'/>
      </div>
      <div class='field' :class="{ 'form-group--error': !$v.dateOfIssue.required }">
        <label class='form-label' for='dateOfIssue'>Дата выдачи*:</label>
        <div class='error' v-if="!$v.dateOfIssue.required">Обязательное поле!</div>
        <input class='form-input' v-model='dateOfIssue' @input="setDateOfIssue($event.target.value)" type='date' id='dateOfIssue' name='dateOfIssue'/>
      </div>
    </div>
    <div class='form-submit'> 
      <button class='form-input-submit' type='submit' :disabled='submitStatus===`PENDING`'>Отправить</button>
      <p class="typo__a" v-if="submitStatus === 'OK'">Спасибо, {{$v.name.$model}} {{$v.surname.$model}}!</p>
      <p class="typo__p" v-if="submitStatus === 'ERROR'">Пожалуйста заполните выделенные поля!</p>
      <p class="typo__b" v-if="submitStatus === 'PENDING'">Отправляю...</p>
    </div>
  </form>
  <div class='credits'>
    <p id='credits'>Designed and coded by Abay Nurpeissov</p>
  </div>
  </div>
</template>


<script>
import { required, minLength, numeric } from 'vuelidate/lib/validators'

export default {
  data() {
    return {
      surname: '',
      name: '',
      fatherName: '',
      dateOfBirth: 0,
      phone: '',
      gender: '',
      group: '',
      doctor: '',
      sms: 'отправлять',
      index: '',
      country: '',
      district: '',
      city: '',
      street: '',
      house: '',
      document: '',
      serie: '',
      docNumber: '',
      issuedBy: '',
      dateOfIssue: '',
      submitStatus: null
    }
  },
  validations: {
    surname: {required},
    name: {required},
    dateOfBirth: {required},
    phone: {required, minLength: minLength(11), numeric},
    group: {required},
    city: {required},
    document: {required},
    dateOfIssue: {required}
  },

  methods: {
    setSurname(value) {this.surname = value; this.$v.surname.$touch()},
    setName(value) {this.name = value; this.$v.name.$touch()},
    setFatherName(value) {this.fatherName = value; this.$v.fatherName.$touch()},
    setDateOfBirth(value) {this.dateOfBirth = value; this.$v.dateOfBirth.$touch()},
    setPhone(value) {this.phone = value; this.$v.phone.$touch()},
    setGender(value) {this.gender = value; this.$v.gender.$touch()},
    setGroup(value) {this.group = value; this.$v.group.$touch()},
    setDoctor(value) {this.doctor = value; this.$v.doctor.$touch()},
    setSms(value) {this.sms = value; this.$v.sms.$touch()},
    setIndex(value) {this.index = value; this.$v.index.$touch()},
    setCountry(value) {this.country = value; this.$v.country.$touch()},
    setDistrict(value) {this.district = value; this.$v.district.$touch()},
    setCity(value) {this.city = value; this.$v.city.$touch()},
    setStreet(value) {this.street = value; this.$v.street.$touch()},
    setHouse(value) {this.house = value; this.$v.house.$touch()},
    setDocument(value) {this.document = value; this.$v.document.$touch()},
    setSerie(value) {this.serie = value; this.$v.serie.$touch()},
    setDocNumber(value) {this.docNumber = value; this.$v.docNumber.$touch()},
    setIssuedBy(value) {this.issuedBy = value; this.$v.issuedBy.$touch()},
    setDateOfIssue(value) {this.dateOfIssue = value; this.$v.dateOfIssue.$touch()},
    submit() {
      this.$v.$touch()
      if (this.$v.$invalid) {
        this.submitStatus = 'ERROR'
      } else {
        this.submitStatus = 'PENDING'
        setTimeout(() => {
          this.submitStatus = 'OK'
        }, 500);
      }
    }
  }
}

</script>

<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap')
%form-shared
  border-radius: 5px
  padding: 20px
  margin: 10px
legend
  width: 100%
%input-shared
  width: 100%
  padding: 12px 20px
  margin: 8px 0
  display: inline-block
  border: 1px solid #ccc
  border-radius: 4px
  box-sizing: border-box
@media (min-width: 480px)
  form
    width: 50%
form
  // width: 70%
  margin: auto
  border-radius: 5px
  background-color: #1b4332
  padding: 20px
.form
  @extend %form-shared
  background-color: #95d5b2
.form-submit
  @extend %form-shared
  text-align: center
.form-input
  @extend %input-shared
.form-input:hover
  border-color: #52b788
.form-input:focus
  border-color: #2d6a4f
.form-input-submit
  @extend %input-shared
  background-color: #95d5b2
  width: 50%
  border: none
  color: #081c15
  font-family: 'Roboto', sans-serif
  font-size: 20px
.form-input-submit:hover
  background-color: #74c69d
.form-input-submit:focus
  background-color: #52b788
.typo__p
  font-size: 18px
  font-family: 'Roboto', sans-serif
  color: #dc2f02
  opacity: 0.8
.typo__b
  font-size: 18px
  font-family: 'Roboto', sans-serif
  color: #ffba08
  opacity: 0.8
.typo__a
  font-size: 30px
  font-family: 'Roboto', sans-serif
  color: #00b4d8
  opacity: 0.8
.title
  font-size: 40px
  font-family: 'Roboto', sans-serif
  color: #081c15
.form-label
  font-size: 20px
  font-family: 'Roboto', sans-serif
  color: #081c15
.error, small
  font-size: 14px
  font-family: 'Roboto', sans-serif
  color: #9d0208
  opacity: 0.8
small
  color: #1b4332
.form-label-radio
  font-family: 'Roboto', sans-serif
  font-size: 16px
  padding: 10px
  bottom: 10px
.form-group--error
  animation-name: shakeError
  animation-fill-mode: forwards
  animation-duration: .6s
  animation-timing-function: ease-in-out
  
@keyframes shakeError
  0%
    transform: translateX(0)
  15%
    transform: translateX(0.375rem)
  30%
    transform: translateX(-0.375rem)
  45%
    transform: translateX(0.375rem)
  60%
    transform: translateX(-0.375rem)
  75%
    transform: translateX(0.375rem)
  90%
    transform: translateX(-0.375rem)
  100%
    transform: translateX(0)

.credits
  text-align: center
#credits
  font-family: 'Roboto', sans-serif
  font-size: 14px
</style>
