<script setup>
import { ref } from 'vue';
import projectsData from '../assets/datajobs.json';

const projects = ref(projectsData);
const selectedProjects = ref([]); 

function toggleSelection(index) {
  if (selectedProjects.value.includes(index)) {
  
    selectedProjects.value = selectedProjects.value.filter(i => i !== index);
  } else {
    selectedProjects.value.push(index);
  }
}
function getStatusClass(status) {
  switch (status) {
    case 'Completed':
      return 'status_completed';
    case 'In Progress':
      return 'status_inprogress';
    case 'Job Scheduled':
      return 'status_jobscheduled';
    default:
      return '';
  }
}

function isSelected(index) {
  return selectedProjects.value.includes(index);
}

</script>



<template>
  <div class="alignment">
    <div class="title"> <strong>Project Listings </strong></div>
    <div class="wrapper">
      <div class="project-table">

        <table>
          <thead>
            <tr class="selected">
              <th class="borderRadius1"> <input type="checkbox" disabled /></th>
              <th>Project Name</th>
              <th>Customer Name</th>
              <th>Referee Name</th>
              <th>Status</th>
              <th class="borderRadius2">Assigned To</th>
            </tr>
          </thead>
          <tbody>
            <!-- List  of Projects-->
            <template v-for="(project, index) in projects" :key="project.ProjectName">
              <tr @click="toggleSelection(index)" :class="{ selected: isSelected(index) }">

                <td class="borderRadius1">
                  <input type="checkbox" :id="'checkbox-' + index" :checked="isSelected(index)"
                     />
                </td>
                <td>{{ project.ProjectName }}</td>
                <td>{{ project.CustomerName }}</td>
                <td>{{ project.RefereeName }}</td>
                <td><span :class="getStatusClass(project.Status)">{{ project.Status }} </span></td>
                <td class="borderRadius2">{{ project.AssignedTo }}</td>

              </tr>
              <!--Details of the project-->
              <tr v-if="isSelected(index)">
                <td colspan="6" class="selected">
                  <div class="details">
                    <div class="details_alignment">
                      <p><strong>Address</strong></p>
                      <p> {{ project.Address }}</p>
                    </div>
                    <div class="details_alignment">
                      <p><strong>City</strong></p>
                      <p> {{ project.City }}</p>
                    </div>
                    <div class="details_alignment">
                      <p><strong>State</strong> </p>
                      <p>{{ project.State }}</p>
                    </div>
                    <div class="details_alignment">
                      <p><strong>Country</strong> </p>
                      <p> {{ project.Country }}</p>
                    </div>
                    <div class="details_alignment">
                      <p><strong>Pin Code </strong> </p>
                      <p> {{ project.PinCode }}</p>
                    </div>
                    <div class="details_alignment">
                      <p><strong>Property Type </strong> </p>
                      <p> {{ project.PropertyType }}</p>
                    </div>
                    <div class="details_alignment">
                      <p><strong>Created On </strong> </p>
                      <p>{{ project.CreatedOn }}</p>
                    </div>
                  </div>
                </td>
              </tr>
            </template>
          </tbody>
        </table>
      </div>
    </div>
    <div class="details"></div>
  </div>
</template>


<style scoped>
.project-table table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0px 2px;
}

.alignment {
  margin: 0px;
  background-color: #eae5e5d0;
}

.wrapper {
  background-color: white;
  margin: 10px 2vw;
  border-radius: 20px;

}

.borderRadius1 {
  border-radius: 8px 0px 0px 8px;
}

.borderRadius2 {
  border-radius: 0px 8px 8px 0px;
}


.project-table th,
.project-table td {

  text-align: center;
  height: 8vh;


}

.project-table {
  padding: 10px 2vw;
}

.details {

  display: flex;
  padding: 10px 20px;

}

.details_alignment {
  flex: 1 1 50px;
  padding: 10px
}

.title {
  font-size: 20px;
  text-align: left;
  padding: 20px;

}

.status_completed {
  background-color: rgb(93, 220, 93);
  opacity: 0.5;
  color: rgba(3, 122, 47, 0.962);
  border-radius: 5px;
  padding: 7px;
  font-weight: 700;

}

.status_inprogress {
  background-color: rgb(159, 159, 217);
  opacity: 0.5;

  color: rgba(20, 10, 150, 0.947);
  border-radius: 7px;
  padding: 5px;
  font-weight: 700;

}

.status_jobscheduled {
  background-color: rgb(224, 130, 130);
  opacity: 0.5;
  color: rgba(94, 7, 7, 0.853);
  border-radius: 7px;
  padding: 5px;
  font-weight: 700;

}


.selected {
  background-color: #eae5e5d0;
  border-radius: 10px;
}

input[type="checkbox"] {
  appearance: none;
  background-color: white;
  border: 2px solid #ccc;
  border-radius: 3px;
  margin-top: 8px;
  width: 13px;
  height: 13px;
  position: relative;
}


input[type="checkbox"]:checked {
  background-color: orange;
  border-color: orange;
}

input[type="checkbox"]:checked::after {
  content: "✓";
  position: absolute;
  color: white;
  top: -40%;



}
</style>

