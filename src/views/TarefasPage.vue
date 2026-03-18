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

            <ion-input
              label="Nome da tarefa"
              label-placement="floating"
              v-model="novaTarefa"
              :clear-input="true"
              placeholder="Ex: Estudar Vue.js"
              :error-text="erroTarefa"
              :class="{'ion-invalid ion-touched': erroTarefa}">
            </ion-input>

            <div>tarefa nova: {{ novaTarefa }} </div>

            <ion-button fill="solid" expand="block" color="primary" @click="Adicionar">
                <ion-icon slot="start" :icon="addOutline"></ion-icon>
                Adicionar
            </ion-button>

            <li v-for="(t, index) in (tare)" :key="index" :style="cor(index)">
                {{index + 1 }} - {{ t }}

                <ion-button fill="clear" color="danger" @click="Remover(index)">
                    <ion-icon :icon="trashOutline"></ion-icon>
                    Remover
                </ion-button> 
            </li>
            
            <div v-if="quantidade === 0 ">Sem bagulho cadastrado</div>

            <ion-button @click="RemoverTudo">Remover tudo</ion-button>
            <ion-button @click="DirecionarSite">Voltar</ion-button>
        </ion-content>
    </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonToolbar, IonHeader, IonTitle, IonContent, IonInput, IonButton, IonIcon } from '@ionic/vue';
import { addOutline, trashOutline } from 'ionicons/icons';
import { ref, computed } from 'vue';

const tare = ref<string[]>( [] )
const novaTarefa = ref('')
const quantidade = ref(0);

const erroTarefa = computed(() => !novaTarefa.value.trim() ? "Campo obrigatório" : "")

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

const RemoverTudo = () =>{
    tare.value.splice(0 , tare.value.length)
}

const cor = (index: number) => {
    return { color: index % 2 === 0 ? 'blue' : 'red' };
}

import router from '@/router';

function DirecionarSite(){
  router.push('/Home')
}
</script>

<style scoped>
</style>