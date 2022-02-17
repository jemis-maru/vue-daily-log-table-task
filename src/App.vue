<template>
  <h2>Daily log sheet</h2>
  <div class="dropdownColor">
    <select v-model="selectedColor">
      <option value="" selected>Choose a color</option>
      <option v-for="color in colors" :key="color" :value="color">{{ color }}</option>
    </select>
  </div>
  <div class="table-container">
    <table :style="{backgroundColor: tableBackGroundColor}">
      <thead>
          <tr>
              <th>Date</th>
              <th>Day</th>
              <th>Section</th>
              <th>Git repo</th>
              <th>Progress</th>
              <th :colspan="findMaxLength">Topic covered</th>
          </tr>
      </thead>
      <tbody>
          <tr v-for="user in users" :key="user">
              <td>{{user.date}}</td>
              <td>{{user.day}}</td>
              <td>{{user.sections.toString()}}</td>
              <td>
                <a target="_blank" :href="user.repo">repo link</a>
              </td>
              <td>
                <div class="progressBar">
                  <div class="progressBarTxt">{{user.progress}}</div>
                  <div class="progressBarValue" :style="{width: user.progress}"></div>
                </div>
              </td>
              <td v-for="topic in user.topics" :key="topic">{{topic}}</td>
          </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
      return {
        selectedColor: '',
        colors: ['yellow', 'grey', 'pink'],
        users: [
            {
              date: '01/02/2022',
              day: 'Tuesday',
              sections: [1],
              repo: 'https://github.com/jemis-maru/vue-section1-tasks',
              progress: '20%',
              topics: ['Overview', 'Lifecycle', 'Directives'],
            },
            {
              date: '02/02/2022',
              day: 'Wednesday',
              sections: [2, 3],
              repo: 'https://github.com/jemis-maru/vue-section2-tasks',
              progress: '70%',
              topics: ['Methods', 'Computed', 'Watch', 'Events', 'Props'],
            },
        ],
      };
  },
  computed:{
    findMaxLength(){
      let maxLength = 0;
      this.users.forEach( obj => {
        if(obj.topics.length > maxLength){
          maxLength = obj.topics.length;
        }
      });
      return maxLength;
    },
    tableBackGroundColor(){
      if(this.selectedColor === 'yellow'){
        return '#e0e0a4';
      }
      else if(this.selectedColor === 'grey'){
        return '#c7c7c7';
      }
      else if(this.selectedColor === 'pink'){
        return '#fbc3ed';
      }
      else{
        return '#ffffff';
      }
    },
  },
}
</script>

<style>
h2, .dropdownColor {
  text-align: center;
}

.table-container{
  overflow-x: auto;
  margin-top: 30px;
}

table, th, td {
  margin: auto;
  border: 1px solid black;
  border-collapse: collapse;
}

th, td {
  padding: 5px;
}

.progressBar {
  width: 100%;
  height: 20px;
  border: 1px solid #000000;
  background: #959595;
  position: relative;
}

.progressBarTxt {
  position: absolute;
  top: 12%;
  right: 25%;
}

.progressBarValue {
  background-color: #00a876;
  height: 100%;
}
</style>
