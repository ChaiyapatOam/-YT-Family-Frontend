<template>
  <div>
    <h2 class="text-primary">Youtube Premium and Netflix</h2>
    <h3>ประจำเดือน : {{Month}}</h3>
    <User :user="user" v-for="(user, index) in users" :key="index" />
  </div>
</template>

<script>
import moment from "moment";
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import User from "@/components/User.vue";
export default {
  name: "Home",
  components: {
    HelloWorld,
    User,
  },
  mounted() {
      this.Month = moment(Date()).locale('th').format("MMMM")
  },
  data() {
    return {
      showimg: true,
      Month: null,
      users: [
        {
          id: "manuel",
          name: "Maximus",
          phone: "1234",
          email: "123@mail",
          details: "Youtube Premium & Netflix",
          price : 120,
          purchased: false,
        },
        {
          id: "max",
          name: "Maximilian",
          phone: "1234",
          email: "56@mail",
          details: "Youtube Premium ",
          price : 50,
          purchased: true,
        },
      ],
    };
  },
};
</script>
