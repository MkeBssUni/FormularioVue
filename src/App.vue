<script>
export default {
  data() {
    return {
      form: {
        name: '',
        lastname: '',
        surname: '',
        birthdate: '',
        photo: [],
        email: '',
        phone: '',
        address: {
          street: '',
          number: '',
          postalcode: '',
          city: '',
          state: ''
        }
      },
      errors:{
        errorName: "",
        errorLastname: "",
        errorSurname: "",
        errorBirthdate: "",
        errorPhoto: "",
        errorEmail: "",
        errorPhone: "",
        errorStreet: "",
        errorNumber: "",
        errorPostalcode: "",
        errorCity: "",
      },
      showErrors:{
        errorName: true,
        errorLastname: true,
        errorSurname: true,
        errorBirthdate: true,
        errorPhoto: true,
        errorEmail: true,
        errorPhone: true,
        errorStreet: true,
        errorNumber: true,
        errorPostalcode: true,
        errorCity: true,
      },
      regex:{
        validateName: /^[a-zA-ZÀ-ÿ\s]{1,40}$/,
        validatePostalcode: /^[0-9]{5}$/,
        validateEmail: /^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$/,
        validatePhone: /^[0-9]{10}$/
      }
    }
  },
  methods: {
    verifySize(event) {
      const file = event.target.files[0];
      const size = file.size;
      const maxSize = 3000000;
      if (size > maxSize) {
        this.errors.errorPhoto = "El tamaño de la imagen es mayor a 3MB";
        this.showErrors.errorPhoto = false;
        this.form.photo = [];
      } else {
        this.errors.errorPhoto = "";
        this.showErrors.errorPhoto = true;
      }
    },
    resetErrors(){
      this.errors.errorName = "";
      this.errors.errorLastname = "";
      this.errors.errorSurname = "";
      this.errors.errorBirthdate = "";
      this.errors.errorPhoto = "";
      this.errors.errorEmail = "";
      this.errors.errorPhone = "";
      this.errors.errorStreet = "";
      this.errors.errorNumber = "";
      this.errors.errorPostalcode = "";
      this.errors.errorCity = "";
      this.showErrors.errorName = true;
      this.showErrors.errorLastname = true;
      this.showErrors.errorSurname = true;
      this.showErrors.errorBirthdate = true;
      this.showErrors.errorPhoto = true;
      this.showErrors.errorEmail = true;
      this.showErrors.errorPhone = true;
      this.showErrors.errorStreet = true;
      this.showErrors.errorNumber = true;
      this.showErrors.errorPostalcode = true;
      this.showErrors.errorCity = true;
    },
    checkForm(e){
      console.log("Empieza la validación",this.form)
      this.resetErrors();
      e.preventDefault();

      if(this.form.name == ''){
        this.errors.errorName = "El nombre es requerido";
        this.showErrors.errorName = false;
      }else{
        this.errors.errorName = "";
        if(!this.regex.validateName.test(this.form.name)){
          this.errors.errorName = "Ingresa solo letras";
          this.showErrors.errorName = false;
        }
      }

      if(this.form.lastname == ''){
        this.errors.errorLastname = "El apellido paterno es requerido";
        this.showErrors.errorLastname = false;
      }else{
        this.errors.errorLastname = "";
        if(!this.regex.validateName.test(this.form.lastname)){
          this.errors.errorLastname = "Ingresa solo letras";
          this.showErrors.errorLastname = false;
        }
      }

      if(this.form.surname != ''){
        if(!this.regex.validateName.test(this.form.surname)){
          this.errors.errorSurname = "Ingresa solo letras";
          this.showErrors.errorSurname = false;
        }
      }

      if(this.form.birthdate != ''){
        var today = new Date();
        var birthDate = new Date(this.form.birthdate);

        var age = today.getFullYear() - birthDate.getFullYear();
        var month = today.getMonth() - birthDate.getMonth();

        if (month < 0 || (month === 0 && today.getDate() < birthDate.getDate())) {
          age--;
        }

        if(age < 18){
          this.errors.errorBirthdate = "Debes ser mayor de edad";
          this.showErrors.errorBirthdate = false;
        }
      }else{
        this.errors.errorBirthdate = "La fecha de nacimiento es requerida";
        this.showErrors.errorBirthdate = false;
      }

      if(this.form.address.street == ''){
        this.errors.errorStreet = "La calle es requerida";
        this.showErrors.errorStreet = false;
      }

      if(this.form.address.number == ''){
        this.errors.errorNumber = "El número es requerido";
        this.showErrors.errorNumber = false;
      }else{
        if(this.form.address.number <= 0){
          this.errors.errorNumber = "El número debe ser mayor a 0";
          this.showErrors.errorNumber = false;
        }
      }

      if(this.form.address.postalcode == ''){
        this.errors.errorPostalcode = "El código postal es requerido";
        this.showErrors.errorPostalcode = false;
      }else{
        if(!this.regex.validatePostalcode.test(this.form.address.postalcode)){
          this.errors.errorPostalcode = "El código postal debe ser de 5 dígitos";
          this.showErrors.errorPostalcode = false;
        }
      }

      if(this.form.address.city == ''){
        this.errors.errorCity = "La ciudad es requerida";
        this.showErrors.errorCity = false;
      }

      if(this.form.email == ''){
        this.errors.errorEmail = "El correo electrónico es requerido";
        this.showErrors.errorEmail = false;
      }else{
        if(!this.regex.validateEmail.test(this.form.email)){
          this.errors.errorEmail = "Ingresa un correo electrónico válido";
          this.showErrors.errorEmail = false;
        }
      }

      if(this.form.phone == ''){
        this.errors.errorPhone = "El número de celular es requerido";
        this.showErrors.errorPhone = false;
      }else{
        if(!this.regex.validatePhone.test(this.form.phone)){
          this.errors.errorPhone = "El número de celular debe ser de 10 dígitos";
          this.showErrors.errorPhone = false;
        }
      }
      
      if(this.form.photo.length == 0){
        this.errors.errorPhoto = "La fotografía es requerida";
        this.showErrors.errorPhoto = false;
      }

      if(this.showErrors.errorName && this.showErrors.errorLastname && this.showErrors.errorSurname && this.showErrors.errorBirthdate && this.showErrors.errorPhoto && this.showErrors.errorEmail && this.showErrors.errorPhone && this.showErrors.errorStreet && this.showErrors.errorNumber && this.showErrors.errorPostalcode && this.showErrors.errorCity){
        console.log("Formulario válido");
        console.log(this.form);
      }
    }
  }
}
</script>

<template>
  <div id="app">
    <header>
      <div>
        <b-navbar type="dark" variant="dark">
          <b-navbar-nav>
            <b-nav-item :to="'/'">Mi Formulario en vue</b-nav-item>
          </b-navbar-nav>
        </b-navbar>
      </div>
    </header>
    <main>
      <b-row>
        <b-col cols="12" >
          <div class="container fluid mt-4">
            <b-card title="Formulario de registro" class="shadow">
              <form id="app" @submit="checkForm">
              <b-row>
                <b-col>
                  <!-- Sección de información personal -->
                  <b-card title="Información personal" class="mb-2" style="min-height: 70vh;">

                    <b-form-group class="mb-4" id="input-group-1" label="Nombre" label-for="input-name">

                      <b-form-input id="name" v-model="form.name" type="text" aria-placeholder="Placeholder"></b-form-input>
                      
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorName">
                        {{ errors.errorName }}
                      </b-form-invalid-feedback>

                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-2" label="Apellido Paterno" label-for="input-lastname">

                      <b-form-input id="input-lastname" v-model="form.lastname" type="text" aria-placeholder="Placeholder"></b-form-input>
                      
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorLastname">
                        {{ errors.errorLastname }}
                      </b-form-invalid-feedback>

                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-3" label="Apellido Materno" label-for="input-surname">

                      <b-form-input id="input-surname" v-model="form.surname" type="text" aria-placeholder="Placeholder"></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorSurname">
                        {{ errors.errorSurname }}
                      </b-form-invalid-feedback>
                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-4" label="Fecha de nacimiento" label-for="input-birthdate">

                      <b-form-input id="input-birthdate" v-model="form.birthdate" type="date" aria-placeholder="Placeholder"></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorBirthdate">
                        {{ errors.errorBirthdate }}
                      </b-form-invalid-feedback>

                    </b-form-group>

                    <b-form-group class="mb-4" label="Fotografía" label-for="input-photo" >
                      <b-form-file v-model="form.photo" accept="image/jpeg, image/png" @change="verifySize"></b-form-file>
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorPhoto">
                        {{ errors.errorPhoto }}
                      </b-form-invalid-feedback>
                    </b-form-group>

                  </b-card>
                </b-col>
                <b-col>
                  <!-- Sección de dirección -->
                  <b-card title="Dirección" class="mb-2" style="min-height: 70vh;">

                    <b-form-group class="mb-4" id="input-group-5" label="Calle" label-for="input-street">

                      <b-form-input id="input-street" type="text" aria-placeholder="Placeholder" v-model="form.address.street"></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorStreet">
                        {{ errors.errorStreet }}
                      </b-form-invalid-feedback>
                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-6" label="Número" label-for="input-number">

                      <b-form-input id="input-number" type="number" aria-placeholder="Placeholder" v-model="form.address.number"></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorNumber">
                        {{ errors.errorNumber }}
                      </b-form-invalid-feedback>

                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-7" label="Código postal" label-for="input-postalcode">

                      <b-form-input id="input-postalcode" type="text" aria-placeholder="Placeholder" v-model="form.address.postalcode"></b-form-input>
                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorPostalcode">
                        {{ errors.errorPostalcode }}
                      </b-form-invalid-feedback>

                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-8" label="Ciudad" label-for="input-city">
                      <b-form-input id="input-city" type="text" aria-placeholder="Placeholder" v-model="form.address.city"></b-form-input>

                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorCity">
                        {{ errors.errorCity }}
                      </b-form-invalid-feedback>

                    </b-form-group>
                  </b-card>
                </b-col>
              </b-row>
              <b-row>
                <b-col>
                  <!-- Sección de información de contacto correo, número celular -->
                  <b-card title="Información de contacto" class="mb-2 mt-4">

                    <b-form-group class="mb-4" id="input-group-9" label="Correo electrónico" label-for="input-email">
                      <b-form-input id="input-email" type="email" aria-placeholder="Placeholder"  v-model="form.email"></b-form-input>

                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorEmail">
                        {{ errors.errorEmail }}
                      </b-form-invalid-feedback>
                    </b-form-group>

                    <b-form-group class="mb-4" id="input-group-10" label="Número de celular" label-for="input-phone">
                      <b-form-input id="input-phone" type="tel" aria-placeholder="Placeholder" v-model="form.phone"></b-form-input>

                      <b-form-invalid-feedback id="input-live-feedback" style="color: crimson;" :state="showErrors.errorPhone">
                        {{ errors.errorPhone }}
                      </b-form-invalid-feedback>
                    </b-form-group>
                    
                  </b-card>
                </b-col>
              </b-row>
              <b-row class="mt-4">
                <b-col>
                  <b-button variant="outline-danger" type="reset">Limpiar</b-button>
                </b-col>
                <b-col>
                  <b-button variant="outline-success" type="submit">Enviar</b-button>
                </b-col>
              </b-row>
            </form>
            </b-card>
          </div>
        </b-col>
    </b-row>
  </main>
</div></template>

<style scoped></style>
