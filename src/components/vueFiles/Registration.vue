<script setup>
import { computed } from 'vue';
import { useStore } from 'vuex';
import { ref } from 'vue';
const store = useStore()
const username = ref()
const email = ref()
const password = ref()

const showRegistrationPopup = computed(() => store.getters["registration/showRegistrationPopup"])
const usernameIsValid = computed(() => store.getters["registration/usernameIsValid"])

const checkAvaliability = (lenght) =>{
    store.commit("registration/checkName",lenght)

}


const toggleModal = () => {
    store.commit("switchButtons/toggleInfoModal")
}


const registerUser = () =>{

    store.dispatch("registration/registerUser",{username:username.value,email:email.value,password:password.value,sigrdze: username.value.length})
        console.log(store.state.registration.userInfo) 
        username.value = ""
        email.value = ""
        password.value = ""
    
        toggleModal()
}

</script>

<template>
        <div v-if="showRegistrationPopup"  class="flex items-center absolute top-20 right-[10%] justify-center w-[20%] h-[40%] bg-gray-100">
            <div>
                <h1 class="text-center text-lg font-bold text-gray-500">Form Register</h1>
                <div class="space-y-4 mt-6">
                    <div class="w-full">
                        <input v-model="username" @change="()=>checkAvaliability(username.length)" type="text" placeholder="username" class="px-4 py-2 bg-gray-50" />
                        <p v-if="usernameIsValid == false" class="text-red-500 font-bold text-[15px]">Use more than 5 letters</p>
                    </div>
                    <div class="w-full">
                        <input v-model="email" type="text" placeholder="email" class="px-4 py-2 bg-gray-50" />

                    </div>
                    <div  class="w-full">
                        <input v-model="password"   type="password" placeholder="password" class="px-4 py-2 bg-gray-50" />
                    </div>
                </div>
                <button @click="registerUser" class="w-full mt-5 bg-indigo-600 text-white py-2 rounded-md font-semibold tracking-tight">Register</button>
            </div>
        </div>

</template>