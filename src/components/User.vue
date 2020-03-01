<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: {{ name }}</p>
    <p>{{ getDateAndTime(createdAt) }}</p>
    <p>{{ helloToMixin }}</p>
    <hr>
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail 
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
        ></UserDetail>
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit 
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
          @child="parents"
        ></UserEdit>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import UserDetail from "./UserDetail.vue"
import UserEdit from "./UserEdit.vue"
import { dateFormat } from '../mixins/dateFormat'

export default {
  components: {
    UserDetail,
    UserEdit
  },

  data:() => ({
    name: 'YuJin',
    address: 'Suwon',
    phone: '010-8433-9772',
    hasDog: true,
    createdAt: null
  }),

  created() {
    this.createdAt = new Date()
  },

  computed: {
    helloToMixin() {
      return this.mixinData + ' 안녕 유진아'
    }
  },

  methods: {
    parents(user) {
      this.name = user.name
      this.address = user.address
      this.phone = user.phone
      this.hasDog = user.hasDog
    },

    // getDateAndTime(date) {
    //   if(date !== null) {
    //       let hour = date.getHours()
    //       let minutes = date.getMinutes()
    //       let fullDate = `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`
    //       return `${fullDate} ${hour}:${minutes}`
    //   } else {
    //       return null
    //   }
    // }
  },

  mixins: [dateFormat]
}
</script>