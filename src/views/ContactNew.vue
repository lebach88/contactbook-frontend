<template>
    <div class="page">
        <h4>Thêm mới Liên hệ</h4>
        <ContactForm :contact="contact" @submit:contact="createContact" @submit:delete="clearContact"/>
        <p>{{ message }}</p>
    </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default{
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {
                name: '',
                email: '',
                address: '',
                phone: '',
                favorite:''
            },
            message: "",
        };
    },
    methods:{
        async createContact(data) {
            try {
                if(data != null){
                    let response = await ContactService.create(data);
                    console.log(response.data)
                    this.message = "Liên hệ được thêm thành công.";
                }
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.createContact(this.data);
        this.message = "";
    },
}
</script>