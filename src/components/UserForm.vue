<template>
    <div class="form-container">
      <h2 class="form-title">Formulaire de Saisie Utilisateur</h2>
      <form @submit.prevent="submitForm">
        <!-- Champ Nom -->
        <div class="form-group">
          <label for="name">Nom</label>
          <input
            type="text"
            id="name"
            v-model="form.name"
            @input="validateName"
            :class="{ 'is-invalid': errors.name }"
            placeholder="Entrez votre nom"
          />
          <small v-if="errors.name" class="error-text">{{ errors.name }}</small>
        </div>
  
        <!-- Champ Email -->
        <div class="form-group">
          <label for="email">Email</label>
          <input
            type="email"
            id="email"
            v-model="form.email"
            @input="validateEmail"
            :class="{ 'is-invalid': errors.email }"
            placeholder="Entrez votre email"
          />
          <small v-if="errors.email" class="error-text">{{ errors.email }}</small>
        </div>
  
        <!-- Champ Téléphone -->
        <div class="form-group">
          <label for="phone">Numéro de Téléphone</label>
          <input
            type="tel"
            id="phone"
            v-model="form.phone"
            @input="validatePhone"
            :class="{ 'is-invalid': errors.phone }"
            placeholder="Entrez votre numéro de téléphone"
          />
          <small v-if="errors.phone" class="error-text">{{ errors.phone }}</small>
        </div>
  
        <button
          type="submit"
          class="btn-submit"
          :disabled="hasErrors"
        >
          Soumettre
        </button>
  
        <p v-if="successMessage" class="success-message">{{ successMessage }}</p>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        form: {
          name: '',
          email: '',
          phone: '',
        },
        errors: {},
        successMessage: ''
      };
    },
    computed: {
      hasErrors() {
        return Object.keys(this.errors).length > 0;
      }
    },
    methods: {
      validateName() {
        if (!this.form.name) {
          this.errors.name = 'Le nom est requis.';
        } else if (this.form.name.length < 3) {
          this.errors.name = 'Le nom doit comporter au moins 3 caractères.';
        } else {
          delete this.errors.name;
        }
      },
      validateEmail() {
        const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!this.form.email) {
          this.errors.email = 'L\'email est requis.';
        } else if (!emailPattern.test(this.form.email)) {
          this.errors.email = 'Veuillez entrer une adresse email valide.';
        } else {
          delete this.errors.email;
        }
      },
      validatePhone() {
        const phonePattern = /^[0-9]{8}$/;
        if (!this.form.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis.';
        } else if (!phonePattern.test(this.form.phone)) {
          this.errors.phone = 'Veuillez entrer un numéro de téléphone valide (8 chiffres).';
        } else {
          delete this.errors.phone;
        }
      },
      submitForm() {
        this.validateName();
        this.validateEmail();
        this.validatePhone();
  
        if (!this.hasErrors) {
          this.successMessage = 'Le formulaire a été soumis avec succès !';
          this.form = { name: '', email: '', phone: '' }; // Réinitialiser le formulaire
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .form-container {
    max-width: 500px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f8f9fa;
    border: 1px solid #ced4da;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .form-title {
    font-size: 24px;
    color: #343a40;
    margin-bottom: 20px;
    text-align: center;
  }
  
  .form-group {
    margin-bottom: 20px;
  }
  
  .form-group label {
    display: flex;
    margin-bottom: 8px;
    font-weight: bold;
    color: #495057;
  }
  
  .form-group input {
    width: 100%;
    padding: 12px;
    border-radius: 5px;
    border: 1px solid #ced4da;
    box-sizing: border-box;
    font-size: 16px;
    transition: border-color 0.3s;
  }
  
  .form-group input:focus {
    border-color: #007bff;
    outline: none;
  }
  
  .is-invalid {
    border-color: #dc3545;
  }
  
  .error-text {
    color: #dc3545;
    font-size: 14px;
    margin-top: 5px;
  }
  
  .btn-submit {
    width: 100%;
    padding: 12px;
    font-size: 16px;
    color: #fff;
    background-color: #007bff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .btn-submit:disabled {
    background-color: #b0bec5;
    cursor: not-allowed;
  }
  
  .success-message {
    color: #28a745;
    font-size: 16px;
    margin-top: 15px;
  }
  </style>
  