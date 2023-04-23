
<script>
import jsonData from './source.json';

export default {
    computed: {
    groupedAllData() {
   
   const grouped =  {};
    
       const filteredDataAssistant = jsonData.filter(item => item.assistant === true);
       const filteredDataStudent = jsonData.filter(item => item.assistant === false);
      
      
      //Assistant Group
      filteredDataAssistant.forEach(item => {
         const group = item.group;

         
               if (!grouped[group]) { 
                    grouped[group] = [];
                } 
        
        grouped[group].push(item);
      });

      //Student Group
       filteredDataStudent.forEach(item => {
        const groupStudent = item.group;

         if (!grouped[groupStudent]) { // Eğer grup daha önce tanımlanmamışsa, tanımlanıyor
                    grouped[groupStudent] = [];
                }

        grouped[groupStudent].push(item);
      });
      return grouped;
         
      }

      
    }   
}

</script>

<template>

  <div>
    <div v-for="(group, groupName) in groupedAllData" :key="groupName">   
      <h2>{{ groupName }}</h2> 
      <ul>
        <li v-for="item in group" :key="item.id">
        <span :style="{ fontSize: item.assistant ? '30px' : '12px' }">{{ item.name  }}</span>
         
        </li>
      </ul>
    </div>
   
  </div>
   
</template>

<style scoped>
 
</style>
