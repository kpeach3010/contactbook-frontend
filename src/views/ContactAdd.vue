<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm
      :contact="{
        name: '',
        email: '',
        phone: '',
        address: '',
        favorite: false,
      }"
      @submit:contact="createContact"
    />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      console.log("Submit data:", data); // Debug: Xem dữ liệu từ form
      try {
        await ContactService.create(data);
        alert("Liên hệ được thêm thành công!");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.error("Lỗi API:", error);
      }
    },
  },
};
</script>

<style scoped>
@import "@/assets/form.css";
</style>
