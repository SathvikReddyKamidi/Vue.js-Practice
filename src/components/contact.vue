<template>
    <div class="bg-info rounded p-1 pb-4 m-2">
        <div class="row">
            <div class="col-5">
                <h3>Name : {{ name }}</h3>
                <p>Email: {{ email }}</p>
                <p>Phone : {{ phone }}</p>
                
            </div>
            <div class="col-3">
                <button @click="toggleFavourite()" :class="[isFavourite? 'btn btn-warning form-control':'btn btn-success form-control']">
                    {{ isFavourite ? 'remove from' : 'Add to' }} Favourite
                </button>
            </div>
            <div class="col-4">
                <LuckyNumber></LuckyNumber>
            </div>
        </div>
        <span class="float-end small" v-if="ownername!=''">
                    *this contact belongs to {{ ownername }}
                </span>
    </div>
</template>
<script setup>
    import{ref,defineProps} from "vue";
import LuckyNumber from "./LuckyNumber.vue";    // const email=ref("hello@appatsery");
    // const props=defineProps(["name","phone","ownername"]);
        const props=defineProps(
            {
                name:{type:String, required:true},
                phone:Number,
                ownername:String,
                email:{type:String,required:false, default:"-n/a"},
                isFavourite:{type:Boolean,default:false},
                       
            });
            const emit=defineEmits(['update-favourite']);
    function toggleFavourite() {
        emit('update-favourite', {isFavourite:props.isFavourite});
    }
</script>