<template>
  <section class="py-20 bg-gray-900">
    <div class="container mx-auto px-4">
      <div class="max-w-2xl mx-auto text-center mb-12" data-aos="fade-up">
        <h2 class="text-3xl md:text-4xl font-bold mb-4 font-poppins">Get in Touch</h2>
        <p class="text-xl text-gray-400">Have questions? We'd love to hear from you.</p>
      </div>

      <form @submit.prevent="handleSubmit" class="max-w-xl mx-auto" data-aos="fade-up" data-aos-delay="200">
        <div class="space-y-6">
          <!-- Name Input -->
          <div class="form-group">
            <input 
              type="text" 
              v-model="formData.name" 
              :class="{ 'has-value': formData.name }" 
              required
            />
            <label>Your Name</label>
            <div class="line"></div>
          </div>

          <!-- Email Input -->
          <div class="form-group">
            <input 
              type="email" 
              v-model="formData.email" 
              :class="{ 'has-value': formData.email, 'invalid': !isValidEmail && formData.email }" 
              required
            />
            <label>Email Address</label>
            <div class="line"></div>
            <span v-if="!isValidEmail && formData.email" class="error-message">Please enter a valid email address</span>
          </div>

          <!-- Message Input -->
          <div class="form-group">
            <textarea 
              v-model="formData.message" 
              :class="{ 'has-value': formData.message }" 
              rows="4" 
              required
            ></textarea>
            <label>Your Message</label>
            <div class="line"></div>
          </div>

          <!-- Submit Button -->
          <button 
            type="submit" 
            class="w-full py-4 px-6 bg-gradient-to-r from-blue-600 to-purple-600 text-white font-semibold rounded-lg transform transition-all duration-300 hover:scale-[1.02] hover:shadow-lg disabled:opacity-50 disabled:cursor-not-allowed flex items-center justify-center"
            :disabled="isSubmitting"
          >
            <span v-if="!isSubmitting">Submit Your Inquiry</span>
            <div v-else class="loading-spinner"></div>
          </button>
        </div>
      </form>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';

const formData = ref({
  name: '',
  email: '',
  message: ''
});

const isSubmitting = ref(false);

const isValidEmail = computed(() => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return !formData.value.email || emailRegex.test(formData.value.email);
});

const handleSubmit = async () => {
  if (!isValidEmail.value) return;
  
  isSubmitting.value = true;
  
  try {
    // Simulate API call
    await new Promise(resolve => setTimeout(resolve, 2000));
    
    // Reset form
    formData.value = {
      name: '',
      email: '',
      message: ''
    };
    
    // Show success message (you can implement your own notification system)
    alert('Message sent successfully!');
  } catch (error) {
    alert('An error occurred. Please try again.');
  } finally {
    isSubmitting.value = false;
  }
};
</script>

<style scoped>
.form-group {
  @apply relative;
}

.form-group input,
.form-group textarea {
  @apply w-full bg-gray-800 text-white px-4 pt-6 pb-2 rounded-lg outline-none transition-all duration-300;
}

.form-group label {
  @apply absolute left-4 top-4 text-gray-400 transition-all duration-300 pointer-events-none;
}

.form-group input:focus ~ label,
.form-group textarea:focus ~ label,
.form-group input.has-value ~ label,
.form-group textarea.has-value ~ label {
  @apply text-sm text-blue-500 -translate-y-3;
}

.form-group .line {
  @apply absolute bottom-0 left-0 w-full h-0.5 bg-gray-600 transform scale-x-0 transition-transform duration-300 origin-center;
}

.form-group input:focus ~ .line,
.form-group textarea:focus ~ .line {
  @apply scale-x-100 bg-blue-500;
}

.form-group input.invalid {
  @apply border-red-500;
}

.error-message {
  @apply text-sm text-red-500 mt-1;
}

.loading-spinner {
  @apply w-6 h-6 border-[3px] border-white border-t-transparent rounded-full animate-spin;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
</style>