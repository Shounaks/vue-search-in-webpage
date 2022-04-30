<script setup>
import { ref } from "@vue/reactivity";
import { watch } from "@vue/runtime-core";

  const searchText = ref('');
  const searchOutput = ref([]);
  const students = ref([
    {studentId: "1", firstName:"shounak", className:"science"},
    {studentId: "2", firstName:"adwait", className:"food"},
    {studentId: "3", firstName:"yash", className:"maths"},
    {studentId: "4", firstName:"pavan", className:"foreign affairs"},
    {studentId: "5", firstName:"ashish", className:"propoganda"}
  ]);

  watch(searchText,()=>{
    searchOutput.value = [];
    students.value.forEach((student=>{
      if((student.firstName.includes(searchText.value) 
        || student.className.includes(searchText.value) 
        || student.studentId.includes(searchText.value)
        ) && !searchOutput.value.includes(student)){
        searchOutput.value.push(student);
      }
    }));
    })
</script>

<template>
  <form class="searchBarForm" action="searchAction">
    <input class="inputBarForm" type="text" v-model="searchText">
    <button>🔎</button>
  </form>
  You searched for: {{searchText}}
<hr/>

<div>
  Here is a list of students:
  <p v-if="!searchOutput.length">Nothing Found</p>
  <ul v-if="searchOutput.length">
    <li v-for="student in (searchText.length == 0)?students:searchOutput" :key="student.studentId" style="list-style-type: none;border: 1px solid blue;padding: 10px; margin: 5px;">
      Student Name: {{student.firstName}} <br/>
      Student Class: {{student.className}}
    </li>
  </ul>
</div>
<hr>
</template>

<style>
.searchBarForm{
  display: flex;
  flex-direction: row;
  border: 1px solid grey;
  padding: 4px;
}

.inputBarForm{
  flex-grow: 2;
  border: none;
}
input:focus {
  outline: none;
}
</style>
