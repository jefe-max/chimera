<template>
  <div class="home">
    <div class="btn-container">
      <button @click="shuffleJobs('title')">Order by title</button>
      <button @click="shuffleJobs('location')">Order by location</button>
      <button @click="shuffleJobs('salary')">Order by salary</button>
    </div>
    <JobList :jobs="jobs" :shuffle="shuffle" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";
import Job from "@/types/Job";
import orderTerm from "@/types/OrderTerm";
import JobList from "@/components/JobsList.vue";

export default defineComponent({
  name: "HomeView",
  components: { JobList },
  setup() {
    const jobs = ref<Job[]>([
      {
        id: "1",
        title: "Farm worker",
        location: "Ifite Awka Ranch",
        salary: 27000,
      },
      {
        id: "2",
        title: "Security gaurd",
        location: "GTB Onitsha",
        salary: 35000,
      },
      {
        id: "3",
        title: "Data Analyst Intern",
        location: "Lagos mainland ",
        salary: 50000,
      },
      {
        id: "4",
        title: "Tech Tutor",
        location: "Genesys Enugu",
        salary: 150000,
      },
    ]);

    let shuffle = ref<orderTerm>("title");
    const shuffleJobs = (order: orderTerm) => {
      shuffle.value = order;
    };
    return { jobs, shuffleJobs, shuffle };
  },
});
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
body{
  background: linear-gradient(
    360deg,
    rgba(41, 114, 124, 0.4),
    rgba(41, 114, 124, 0.1)
  );
}
.btn-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
  gap: 10px;
}
button {
  padding: 0.5rem;
  border-radius: 10px;
  background-color: rgba(41, 114, 124);
  color: #fff;
  font-weight: bold;
  border-color: rgba(41, 114, 124);
  cursor: pointer;
  margin: 0 0.5rem;
}
</style>
