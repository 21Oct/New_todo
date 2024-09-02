

<template>

<div id="block">

  <h1>My Todo App</h1><hr>

   <form @submit.prevent>
   <input type="text" placeholder="new_tasks" v-model="newTasks" class="form">
   <button :disabled="newTasks==0" @click="addTasks" class="form">+</button>
   </form>

<!-- Affiche un message lorsque l'utilisateur n'a rien insérer -->
   <div v-if="tasks==0">Insert a task 😢</div>

<!-- S'affiche lorsque l'utilisateur à commencer à écrire -->
   <div v-else>

     <ul>
     <!-- Barrer chaque tache dans la liste de tache et 
      mettre ceux qui sont terminées en bas de liste -->
       <li v-for="task in sortTasks()" :class="{completed: task.completed}" 
         id="myList">

         <!-- Est lié à chacune des taches coché grace à v-model  -->
         <input type="checkbox" v-model="task.completed" class="listTasks"> 

         <button @click="deleteTasks(task)" class="listTasks">Delete</button>
            {{ task.name }}  <!--  Affiche le nom de chaque tache -->
      
       </li>
     </ul>
  

  
  </div>





</div>

</template>



<script setup>

import { ref } from 'vue';

//stocker la liste des taches à faire
const tasks=ref([])

//stocker les taches en cours de saisies
const newTasks=ref('')

// Ajouter une nouvelle tache à la liste des choses à faire
const addTasks=()=>{
   tasks.value.push({
    name:newTasks.value,
    completed:false,
    date:Date.now()
   })
   newTasks.value=''
}

// Supprimer une tache
const deleteTasks=(task)=>{
  tasks.value=tasks.value.filter(n => n !==task)


}

const sortTasks=()=>{
 return tasks.value.toSorted((a,b)=> a.completed > b.completed ? 1 : -1)
}

</script>


<style scoped>
    
    .completed{
      opacity: 40%;
      text-decoration: line-through;
      
    }

    #myList{
      list-style-type: none;
      height: 50px;
    }

    .listTasks{
      border-radius: 5px; 
    }

    #block{
      background: #475;
      padding: 50px;
      margin: 150px;
      border: 3px solid #366;
      border-radius: 20px;
      text-align: justify;
      box-shadow:  0px 0px 20px black;
      font-family: 'Times New Roman', Times, serif,;
      
    }

    .form{
      height: 25px;
      border-radius: 5px;
    }
    

</style>