<template>
    <div class="user-form-container">
      <form @submit.prevent="submitForm">
        <div class="form-group">
          <label for="name">Nom:</label>
          <input type="text" id="name" required v-model="name" @blur="validateName" />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>
  
        <div class="form-group">
          <label for="email">Email:</label>
          <input type="email" id="email" required v-model="email" @blur="validateEmail" />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>
  
        <div class="form-group">
          <label for="phone">Numéro de téléphone:</label>
          <input type="text" id="phone" required v-model="phone" @blur="validatePhone" />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>
  
        <button type="submit">Soumettre</button>
      </form>
      <p v-if="submittedMessage" class="success-message">{{ submittedMessage }}</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'UserForm',
    data() {
      return {
        name: '',
        email: '',
        phone: '',
        errors: {},
        submittedMessage: ''
      };
    },
    methods: {
      validateName() {
        if (!this.name) {
          this.errors.name = 'Le nom est requis.';
        } else {
          delete this.errors.name;
        }
      },
      validateEmail() {
        const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
        if (!this.email) {
          this.errors.email = 'L\'email est requis.';
        } else if (!emailPattern.test(this.email)) {
          this.errors.email = 'L\'email n\'est pas valide.';
        } else {
          delete this.errors.email;
        }
      },
      validatePhone() {
        const phonePattern = /^\d{8}$/;
        if (!this.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis.';
        } else if (!phonePattern.test(this.phone)) {
          this.errors.phone = 'Le numéro de téléphone n\'est pas valide.';
        } else {
          delete this.errors.phone;
        }
      },
      submitForm() {
        this.validateName();
        this.validateEmail();
        this.validatePhone();
        if (Object.keys(this.errors).length === 0) {
          this.submittedMessage = 'Formulaire soumis avec succès!';
          // Réinitialiser le formulaire
          this.name = '';
          this.email = '';
          this.phone = '';
        } else {
          this.submittedMessage = '';
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .user-form-container {
    max-width: 500px;
    margin: 0 auto;
    padding: 20px;
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  }
  
  .form-group {
    margin-bottom: 15px;
  }
  
  label {
    display: block;
    margin-bottom: 5px;
  }
  
  input {
    width: 100%;
    padding: 8px;
    box-sizing: border-box;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
  
  button {
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  button:hover {
    background-color: #45a049;
  }
  
  .error {
    color: red;
    font-size: 0.875em;
  }
  
  .success-message {
    color: green;
    font-size: 1em;
    margin-top: 20px;
  }
  </style>
  