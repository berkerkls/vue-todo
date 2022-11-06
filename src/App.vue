<template>
  <div class="container">
    <HeaderItem title="Shopping List" />
    <InputSection />
    <ListSection :itemList="shopList" />
  </div>
</template>

<script>
import InputSection from "./components/InputSection.vue"
import HeaderItem from "./components/HeaderItem.vue"
import ListSection from "./components/ListSection.vue"
import axios from "axios"
 export default {
  components: {
    InputSection,
    HeaderItem,
    ListSection
  },
  data() {
    return {
      shopList: []
    }
  
  },
  mounted() {
    axios.get("http://localhost:3000/items")
    .then(res => {
      this.shopList = res.data
      console.log(this.shopList)
    })
  },
  methods: {
    enterInput(e) {
      const newObject = {
        id: new Date().getTime(),
        title: e.target.value
      }
      axios.post("http://localhost:3000/items", newObject).then(res => this.shopList.push(res.data))
      
      e.target.value = ""
    },
    deleteItem(item) {
      axios.delete(`http://localhost:3000/items/${item.id}`)
      .then(res => {
        console.log(res)
        this.shopList = this.shopList.filter(el => el.id !== item.id)
      })
    }
  },
  provide() {
    return {
      enterInput: this.enterInput,
      itemList: this.shopList,
      deleteItem: this.deleteItem
    }
  }
 }

</script>