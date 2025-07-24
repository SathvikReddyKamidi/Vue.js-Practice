<template>
    <div class="bg-black text pt-3">
        <div class="container">
            <div class="row text-white p-2 mb-2">
                <div class="col-6">Owner Name: <input v-model="ownername"/></div>
                <div class="col-6 text-end">Lucky Number : <input v-model.number="maxNumber"></div>
            </div>
            <br/><br/>
            <AddContact @add-contact="onaddContact"></AddContact>
            <div class="col-12" v-for="contact in contactList" :key="contact.name">
                <contact 
                :name="contact.name" 
                :phone="contact.phone" 
                :ownername="contact.ownername" 
                :isFavourite="contact.isFavourite" 
                :email="contact.email"
                
                @update-favourite="contact.isFavourite = onUpdateFavourite($event)"
                ></contact>
            </div>
        </div>
    </div>
</template>
<script setup>
import { reactive, ref ,provide } from 'vue';
import ButtonCounter from './components/ButtonCounter.vue';
import AddContact from './components/addContact.vue';
import contact from './components/contact.vue';
const maxNumber = ref(100);
provide('maxLuckyNumber', maxNumber);
    
    const ownername=ref("Kamidi");
    const contactList = reactive([
        { name: "Sathvik", phone: 9132956622, ownername:ownername, isFavourite:false },
        { name: "Sathvik1", phone: 9132956623 ,ownername:ownername, isFavourite:true},
        { name: "Sathvik2", phone: 9132956624 ,ownername:ownername, isFavourite:false}
    ]);
    function onUpdateFavourite(isFavourite) {
        console.log("isFavourite", isFavourite);
        return !isFavourite.isFavourite;
    }
    function onaddContact(contact) {
        contact.isFavourite = false; // default value for new contact
        contact.ownername = ownername.value; // set owner name for new contact
        contactList.push(contact);
        console.log("contactList", contactList);
    }
</script>
<style>
</style>