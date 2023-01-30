<script setup>


 const todos = ref([
    {
      id: 1,
      title: "todo 1",
      completed: false,
    },
    {
      id: 2,
      title: "todo 2",
      completed: false,
    },
    {
      id: 3,
      title: "todo 3",
      completed: false,
    },
 ])
const newTodo = ref("")
const errmsg=ref("")
 const addTodo = () => {
  if(newTodo.value.length<3){
errmsg.value="Todo must be less than 3 characters"
return ;
}
else{


    todos.value.push({
      id: todos.value.length + 1,
      title: newTodo.value,
      completed: false,
    })
    newTodo.value = ""
  
 }
  }

 const removecheckedTodos=() =>{
    todos.value = todos.value.filter((todo) => !checked.value.includes(todo.id))
    }

 /* const removeTodo=(id)=>{
    todos.value = todos.value.filter((todo) => todo.id !== id)
 }*/
 const checked = ref([])

 const selected = ref(false)

if(selected.value){
  checked.value = todos.value.map((todo) => todo.id)
  console.log(checked.value)
}
else{
  checked.value = []
  console.log(checked.value)
}







</script>
<template>
    <div class="h-screen min-w-max  flex  flex-col items-center justify-center ">
        <section >
           <form @submit.prevent="addTodo" class="border w-72 border-gray-800 rounded-md flex justify-between" >
            
               <input type="text" placeholder="Enter todo "  v-model="newTodo" class="w-64  h-8 border-none border-transparent bg-transparent "/>
                
               <button type="submit"  class="border-l w-11 h-8 border-gray-800  bg-gray-200  " >
            
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="5" stroke="white" class="w-6 h-6 ml-2 bg-gray-800 rounded-full ">
  <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
</svg>

</button>



           
</form>
<p v-if="errmsg" class="text-red-500">{{ errmsg }}</p>
        <div class="mt-2 border border-b-0 border-gray-800 ">
            <ul>
                <li  v-for="todo in todos" :key="todo.id" class="flex justify-between border-b border-gray-800 p-2">
             <span class="flex"> 

              <label for="checkbox" class="border-none"><input type="checkbox"  
                 :value="todo.id" v-model="checked">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="4" stroke="currentColor" :class="{'text-lime-700':checked==true}" class="w-4 h-4  ">
  <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
</svg>
</label>
                
               {{ todo.title }}</span>
                  <button v-if="checked" @click="removecheckedTodos(todo.id)" ><svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="#df2c14" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
</svg></button>
 </li>
                
            </ul>
        </div>
        </section>
        
    

    </div>
</template>

<style scoped>
/* changing checkbox style */ 
 
.hidden {
  display: none;
}

input:checked + label > span {
  background-color: gray;
}
</style>