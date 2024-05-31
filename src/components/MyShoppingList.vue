<script setup>

import { ref, computed } from 'vue';

const header = ref('My Shopping List App');
const items = ref([]);
const reverseItems = computed(() => [...items.value].reverse());
const editing = ref(false);
const newItem = ref("");
const newItemPriority = ref(false);

const characters = computed(() => newItem.value.length);
/* const items = ref(
    {
        'item-1': { id: 'item-1', name: 'Milk', purchased: false, highPriority: true },
        'item-2': { id: 'item-2', name: 'Bread', purchased: true, highPriority: false },
        'item-3': { id: 'item-3', name: 'Cheese', purchased: false, highPriority: true }
    }
); */
/* const iceCreamFlavor = ref([]); */

const saveItem = () => {
    items.value.push({
        id: items.value.length + 1,
        name: newItem.value,
        highPriority: newItemPriority.value
    });
    newItem.value = "";
};
const doEdit = (val) => {
    editing.value = val;
    newItem.value = "";
    newItemPriority.value = false;
};

const togglePurchased = (item) => {
    item.purchased = !item.purchased;
};
</script>

<template>
    <div class="header">
        <h1>{{ header }}</h1>
        <button class="btn" v-if="editing" @click="doEdit(false)">Cancel</button>
        <button class="btn btn-primary" v-else @click="doEdit(true)">Add item</button>
    </div>
    <form v-if="editing" class="add-item-form" @submit.prevent="saveItem">
        <input type="text" placeholder="Add an item" v-model.trim="newItem" />
        Priority:
        <label>
            <input type="checkbox" v-model="newItemPriority" />
            High Priority
        </label>
        <button class="btn btn-primary" :disabled="newItem.length === 5">Save item</button>
        <!--<select v-model="newItemPriority">
            <option value="low">Low</option>
            <option value="high">High</option>
        </select> -->
        <!--<label>
            <input type="radio" v-model="newItemPriority" value="low" />
            Low
        </label>
        <label>
            <input type="radio" v-model="newItemPriority" value="high" />
            High
        </label> -->

        <!--<label>
            <input type="checkbox" v-model="iceCreamFlavor" value="vanilla"/>
            Vanilla
        </label>
        <label>
            <input type="checkbox" v-model="iceCreamFlavor" value="chocolate"/>
            Chocolate
        </label>
        <label>
            <input type="checkbox" v-model="iceCreamFlavor" value="strawberry"/>
            Strawberry
        </label>
        {{ iceCreamFlavor }} -->
    </form>
    <p v-if="editing" class="counter">{{ characters }}/200</p>
    <ul>
        <li @click="togglePurchased(item)" v-for="(item) in reverseItems" :key="item.id"
            :class="{ strikeout: item.purchased, priority: item.highPriority }" class="static-class">
            {{ item.name }}
        </li>
        <!--  <li v-for="item in items" :key="item.id">{{ item.name }}</li> -->
        <!--         <li v-for="item in items" :key="item.id" :class="[item.purchased ? 'strikeout text-gray' : 'underlined',
            'other-class',
        { priority: item.highPriority }]">
            {{ item.name }}
        </li> -->
    </ul>
    <p v-if="!items.length && !editing">Nothing to see here</p>
</template>

<style></style>
