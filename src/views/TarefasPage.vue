<template>
    <ion-page>
        <ion-header>
            <ion-toolbar>
                <ion-title>TESTE</ion-title>
            </ion-toolbar>
        </ion-header>
        
        <ion-content :fullscreen="true">
            <ion-header collapse="condense">
                <ion-toolbar>
                    <ion-title size="large">oloko</ion-title>
                </ion-toolbar>
            </ion-header>

            <ion-input v-model="novaTarefa">Digite sua tarefa</ion-input>
            <div>tarefa nova: {{ novaTarefa }} </div>
            <ion-button @click="Adicionar">Adicionar</ion-button>

            <li v-for="(t, index) in (tare)" :key="index">
                {{ t }} <ion-button @click="Remover(index)">Remover</ion-button>
            </li>
            
            <div v-if="quantidade === 0 ">Sem bagulho cadastrado</div>

            <ion-button @click="DirecionarSite">Voltar</ion-button>
        </ion-content>
    </ion-page>



</template>

<script setup lang="ts">
import { IonPage, IonToolbar, IonHeader, IonTitle, IonContent, IonInput, IonButton } from '@ionic/vue';
import { ref } from 'vue';

const tare = ref<string[]>( [] )
const novaTarefa = ref('')
const quantidade = ref(0);

const Adicionar = () => {
    if(novaTarefa.value.trim() === ""){
        return
    }
    tare.value.push(novaTarefa.value);
    quantidade.value++;
}

const Remover = (index:number) =>{
    tare.value.splice(index,1)
    quantidade.value--;
}

import router from '@/router';


function DirecionarSite(){
  router.push('/Home')
}
</script>


<style scoped>

</style>