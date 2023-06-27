<template>
  <div class="job-list">
    <h3>Ordered by {{ shuffle }}</h3>
    <transition-group name="list" tag="ul">
      <li v-for="job in orderedJobs" :key="job.id">
        <h2>{{ job.title }} in {{ job.location }}</h2>

        <div class="salary">
          <img src="@/assets/naira.png" alt="naira" />
          <p>{{ job.salary }}</p>
        </div>

        <div class="description">
          <p>
            Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eligendi
            ad, reiciendis impedit unde pariatur amet sapiente aliquam, numquam,
            veritatis repellat dolore voluptatem vero reprehenderit velit atque
            eos doloribus. Officiis, ipsam?
          </p>
        </div>
      </li>
    </transition-group>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";
import job from "@/types/Job";
import orderTerm from "@/types/OrderTerm";

export default defineComponent({
  props: {
    jobs: {
      required: true,
      type: Array as PropType<job[]>,
    },
    shuffle: {
      required: true,
      type: String as PropType<orderTerm>,
    },
  },

  setup(props) {
    const orderedJobs = computed(() => {
      return [...props.jobs].sort((a: job, b: job) => {
        return a[props.shuffle] > b[props.shuffle] ? 1 : -1;
      });
    });

    return { orderedJobs };
  },
});
</script>

<style scoped>
.job-list ul {
  display: flex;
  flex-direction: column;
  gap: 20px;
  justify-content: center;
  align-items: center;
  margin: 30px 1rem;
}
li {
  border: 1px solid grey;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 0 10px 0 grey;
  list-style: none;
  max-width: 35rem;
  background-color: #fff;
  color: rgb(48, 47, 47);
}
li .salary {
  margin: 10px 0;
  color: rgb(6, 185, 21);
  font-weight: 900;
  font-weight: bold;
  display: flex;
  align-items: center;
  gap: 5px;
}
li .salary img {
  width: 25px;
  height: 25px;
}
li .description {
  color: rgb(14, 0, 0);
  font-weight: bold;
}
h3 {
  text-align: center;
  margin-top: 20px;
}
h2 {
  font-size: 1.8rem;
  color: rgba(41, 114, 124);
}
.list-move {
  transition: all 1s;
}
</style>
