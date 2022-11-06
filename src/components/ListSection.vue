<template>
    <ul v-if="itemList.length > 0">
        <li v-for="item in itemList" :key="item.id" class="list-item">
            <p>{{ item.title }}</p>
            <button @click="deleteItem(item)" class="delete">Delete</button>
        </li>
        <small>{{`There is ${itemList.length} product to buy`}}</small>
    </ul>
    <p v-else>There is no item to buy today.</p>
</template>

<script>
export default {
    inject: ["deleteItem"],
    props: ["itemList"]
}
</script>