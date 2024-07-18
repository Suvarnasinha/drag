<template>
  <div class="container">
    <!-- Sidebar with draggable elements -->
    <div class="sidebar">
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'textarea', 'textarea1')">
        Textarea
      </div>
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'number', 'number1')">
        Number Input
      </div>
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'radio', 'radio1')">
        Radio Button
      </div>
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'select', 'select1')">
        DropDown
      </div>
    </div>

    <!-- Main area where elements are dropped -->
    <form class="main-area" @dragover.prevent @drop="drop($event)" @submit.prevent="handleSubmit">
      <draggable v-model="mainItems" group="main">
        <template #item="{ element }">
          <div :key="element.id" class="draggable-item">
            <label>
              <input type="checkbox" v-model="element.required" />
              Required
            </label>
            <template v-if="element.type === 'textarea'">
              <textarea :required="element.required" placeholder="Enter text here" v-bind:ref="setRefs(element.id)"></textarea>
            </template>
            <template v-else-if="element.type === 'number'">
              <input type="number" :required="element.required" placeholder="Enter number" v-bind:ref="setRefs(element.id)" />
            </template>
            <template v-else-if="element.type === 'radio'">
              <div>
                <input type="radio" :required="element.required" name="radio" v-bind:ref="setRefs(element.id)" /> Option 1
                <input type="radio" :required="element.required" name="radio" v-bind:ref="setRefs(element.id)" /> Option 2
              </div>
            </template>
            <template v-else-if="element.type === 'select'">
              <select :required="element.required" v-bind:ref="setRefs(element.id)">
                <option value="">Select an option</option>
                <option value="volvo">Volvo</option>
                <option value="saab">Saab</option>
                <option value="fiat">Fiat</option>
                <option value="audi">Audi</option>
              </select>
            </template>
          </div>
        </template>
      </draggable>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import draggable from 'vuedraggable';

const mainItems = ref([]);
const formRefs = ref({});

const setRefs = (id) => {
  return (el) => {
    if (el) {
      formRefs.value[id] = el;
    }
  };
};

const dragStart = (event, type, id) => {
  event.dataTransfer.dropEffect = 'move';
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('type', type);
  event.dataTransfer.setData('id', id);
  event.dataTransfer.setData('source', 'sidebar');
};

const drop = (event) => {
  const source = event.dataTransfer.getData('source');
  if (source === 'sidebar') {
    const type = event.dataTransfer.getData('type');
    const id = event.dataTransfer.getData('id');
    mainItems.value.push({ type, id, required: false });
  }
};

const handleSubmit = () => {
  const requiredFields = mainItems.value.filter(item => item.required);
  const unfilledFields = requiredFields.filter(item => {
    const el = formRefs.value[item.id];
    return !el.value && (el.type !== 'radio' && el.type !== 'select-one' && el.type !== 'textarea');
  });

  console.log('Required fields:', requiredFields);
  console.log('Unfilled required fields:', unfilledFields);

  if (unfilledFields.length > 0) {
    alert('Please fill in all required fields.');
  } else {
    alert('Form submitted successfully!');
  }
};
</script>

<style>
.container {
  display: flex;
  width: 100%;
  height: 100vh;
}

.sidebar {
  width: 25%;
  padding: 20px;
  background-color: #f0f0f0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.main-area {
  width: 75%;
  padding: 20px;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.draggable-item {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  background-color: #f9f9f9;
  border-radius: 4px;
  width: 300px;
}

textarea, input[type="number"], select {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-top: 5px;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
]]]]]]]]]]]]]]]]]]]
































<template>
  <div class="container">
    <!-- Sidebar with draggable elements -->
    <div class="sidebar">
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'textarea')">
        Textarea
      </div>
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'number')">
        Number Input
      </div>
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'radio')">
        Radio Button
      </div>
      <div class="draggable-item" draggable="true" @dragstart="dragStart($event, 'select')">
        DropDown
      </div>
    </div>

    <!-- Main area where elements are dropped -->
    <form class="main-area" @dragover.prevent @drop="drop($event)" @submit.prevent="handleSubmit">
      <draggable v-model="mainItems" group="main">
        <template #item="{ element }">
          <div :key="element.id" class="draggable-item">
            <label>
              <input type="checkbox" v-model="element.required" />
              Required
            </label>
            <template v-if="element.type === 'textarea'">
              <textarea :required="element.required" placeholder="Enter text here"></textarea>
            </template>
            <template v-else-if="element.type === 'number'">
              <input type="number" :required="element.required" placeholder="Enter number"/>
            </template>
            <template v-else-if="element.type === 'radio'">
              <div>
                <input type="radio" :required="element.required" name="radio" /> Option 1
                <input type="radio" :required="element.required" name="radio" /> Option 2
              </div>
            </template>
            <template v-else-if="element.type === 'select'">
              <select :required="element.required">
                <option value="">Select an option</option>
                <option value="volvo">Volvo</option>
                <option value="saab">Saab</option>
                <option value="fiat">Fiat</option>
                <option value="audi">Audi</option>
              </select>
            </template>
          </div>
        </template>
      </draggable>
      <button type="submit">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import draggable from 'vuedraggable';

const mainItems = ref([]);

const dragStart = (event, type) => {
  event.dataTransfer.dropEffect = 'move';
  event.dataTransfer.effectAllowed = 'move';
  event.dataTransfer.setData('type', type);
  event.dataTransfer.setData('source', 'sidebar');
};

const drop = (event) => {
  const source = event.dataTransfer.getData('source');
  if (source === 'sidebar') {
    const type = event.dataTransfer.getData('type');
    mainItems.value.push({ type, id: Date.now(), required: false });
  }
};

const handleSubmit = () => {
  alert('Form submitted successfully!');
};
</script>

<style>
.container {
  display: flex;
  width: 100%;
  height: 100vh;
}

.sidebar {
  width: 25%;
  padding: 20px;
  background-color: #f0f0f0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.main-area {
  width: 75%;
  padding: 20px;
  background-color: #ffffff;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.draggable-item {
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  background-color: #f9f9f9;
  border-radius: 4px;
  width: 300px;
}

textarea, input[type="number"], select {
  width: 100%;
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-top: 5px;
}

button {
  margin-top: 20px;
  padding: 10px 20px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
