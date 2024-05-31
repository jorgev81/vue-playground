<script>
import { ref } from 'vue';

const header = ref('My Shopping List App');
const items = ref([]);
const editing = ref(false);

/* const items = ref(
    {
        'item-1': { id: 'item-1', name: 'Milk' },
        'item-2': { id: 'item-2', name: 'Bread' },
        'item-3': { id: 'item-3', name: 'Cheese' }
    }
); */

const newItem = ref("");
/* const newItemHighPriority = ref("low"); */
const newItemPriority = ref(false);
const iceCreamFlavor = ref([]);
const saveItem = () => {
    items.value.push({ id: items.value.length + 1, name: newItem.value });
    newItem.value = "";
};
const doEdit = (val) => {
    editing.value = val;
    newItem.value = "";
};

export default {
    setup() {
        return { header, items, newItem, newItemPriority, iceCreamFlavor, saveItem, editing, doEdit };
    }
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
        <button 
        class="btn btn-primary"
        :disabled="newItem.length === 5"
        >Save item</button>
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
    <ul>
        <!--  <li v-for="item in items" :key="item.id">{{ item.name }}</li> -->
        <li v-for="({ id, name }, index) in items" :key="id">
            {{ index }}
            {{ name }}
        </li>
    </ul>
    <p v-if="!items.length">Nothing to see here</p>
</template>

<style></style>
