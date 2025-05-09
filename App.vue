<template>
  <div class="max-w-xl mx-auto p-6 bg-white shadow-md rounded">
    <h2 class="text-2xl font-bold mb-4">Registration Form</h2>

    <form @submit.prevent="register">
      <div class="mb-4">
        <label class="block mb-1">Name</label>
        <input type="text" v-model="form.name" class="w-full border rounded p-2"
               :class="{'border-red-500': errors.name}" placeholder="Enter your name" />
      </div>

      <div class="mb-4">
        <label class="block mb-1">Contact Number</label>
        <input type="text" v-model="form.contact" class="w-full border rounded p-2" />
      </div>

      <div class="mb-4">
        <label class="block mb-1">Email</label>
        <input type="email" v-model="form.email" class="w-full border rounded p-2"
               :class="{'border-red-500': errors.email}" @blur="validateEmail" />
        <p v-if="errors.email" class="text-red-500 text-sm">{{ errors.email }}</p>
      </div>

      <div class="mb-4">
        <label class="block mb-1">Gender</label>
        <div class="flex space-x-4">
          <label><input type="radio" value="Male" v-model="form.gender" /> Male</label>
          <label><input type="radio" value="Female" v-model="form.gender" /> Female</label>
          <label><input type="radio" value="Other" v-model="form.gender" /> Other</label>
        </div>
      </div>

      <div class="mb-4">
        <label class="block mb-1">Country</label>
        <select v-model="form.country" class="w-full border rounded p-2">
          <option disabled value="">Select Country</option>
          <option v-for="country in countries" :key="country">{{ country }}</option>
        </select>
      </div>

      <div class="mb-4">
        <label class="block mb-1">College</label>
        <select v-model="form.college" class="w-full border rounded p-2">
          <option disabled value="">Select College</option>
          <option v-for="college in colleges" :key="college">{{ college }}</option>
        </select>
      </div>

      <div class="mb-4">
        <label class="block mb-1">Year</label>
        <select v-model="form.year" class="w-full border rounded p-2">
          <option disabled value="">Select Year</option>
          <option>1st</option>
          <option>2nd</option>
          <option>3rd</option>
          <option>4th</option>
        </select>
      </div>

      <div class="mb-4">
        <label class="block mb-1">Domain / Department</label>
        <input type="text" v-model="form.domain" class="w-full border rounded p-2" />
      </div>

      <button type="submit" class="w-full bg-blue-600 text-white p-2 rounded hover:bg-blue-700">
        Register
      </button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        contact: '',
        email: '',
        gender: '',
        country: '',
        college: '',
        year: '',
        domain: '',
      },
      errors: {
        name: '',
        email: '',
      },
      countries: ['USA', 'India', 'UK', 'Germany', 'Australia'], // Add more as needed
      colleges: ['Harvard', 'MIT', 'IIT Delhi', 'Oxford', 'Stanford'], // Add more as needed
      existingEmails: ['test@example.com', 'user@example.com'], // Placeholder for existing email check
    };
  },
  methods: {
    validateEmail() {
      const email = this.form.email;
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailPattern.test(email)) {
        this.errors.email = 'Invalid email format';
      } else if (this.existingEmails.includes(email)) {
        this.errors.email = 'Email already registered';
      } else {
        this.errors.email = '';
      }
    },
    register() {
      const namePattern = /^[A-Za-z\s]+$/;
      this.errors.name = namePattern.test(this.form.name) ? '' : 'Name must only contain letters';

      this.validateEmail();

      if (!this.errors.name && !this.errors.email) {
        alert('Registration successful!');
        console.log(this.form);
      }
    },
  },
};
</script>
<style scoped>
input, select{
  outline: none;
}
</style>
