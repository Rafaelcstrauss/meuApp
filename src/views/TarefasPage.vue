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

            <ion-list>
                <ion-item v-for="(t, i) in tare" :key="i">
                    <ion-icon slot="start" :icon="checkmarkCircleOutline" />
                    <ion-label>{{ t }}</ion-label>
                    <ion-button slot="end" fill="clear" color="danger" @click="Remover(i)">
                        <ion-icon :icon="trashOutline" />
                    </ion-button>
                </ion-item>
            </ion-list>

            <p v-if="!tare.length" class="ion-text-center ion-padding">
                Nenhuma tarefa cadastrada.
            </p>

            <ion-button @click="RemoverTudo">Remover tudo</ion-button>
            <ion-button @click="DirecionarSite">Voltar</ion-button>
        </ion-content>
    </ion-page>
</template>

<script setup lang="ts">
import { IonPage, IonToolbar, IonHeader, IonTitle, IonContent, IonInput, IonButton, IonIcon, IonList, IonItem, IonLabel } from '@ionic/vue';
import { addOutline, trashOutline, checkmarkCircleOutline } from 'ionicons/icons';
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





import router from '@/router';

function DirecionarSite(){
  router.push('/Home')
}
</script>

<style scoped>
</style>