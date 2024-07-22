<template>
    <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
      <div class="bg-white p-8 rounded-lg shadow-lg w-3/4 max-w-4xl max-h-full overflow-y-auto">
        <span class="close cursor-pointer text-gray-500 float-right text-2xl" @click="close">&times;</span>
        <h2 class="text-2xl font-bold mb-4">{{ isEditing ? 'Edit' : 'Add' }} Record</h2>
        <form @submit.prevent="submitForm" class="grid grid-cols-1 md:grid-cols-2 gap-4">
          <div>
            <label class="block mb-1">Title</label>
            <input v-model="form.title" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div class="col-span-2">
            <label class="block mb-1">Description</label>
            <textarea v-model="form.description" required class="w-full p-2 border border-gray-300 rounded"></textarea>
          </div>
          <div>
            <label class="block mb-1">Experiment Name</label>
            <input v-model="form.experimentName" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div>
            <label class="block mb-1">Experiment Type</label>
            <input v-model="form.experimentType" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div>
            <label class="block mb-1">Sample Name</label>
            <input v-model="form.sampleName" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div>
            <label class="block mb-1">Sample Source</label>
            <input v-model="form.sampleSource" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div>
            <label class="block mb-1">Equipment Name</label>
            <input v-model="form.equipmentName" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div>
            <label class="block mb-1">Procedure Step</label>
            <input v-model="form.procedureStep" type="text" required class="w-full p-2 border border-gray-300 rounded" />
          </div>
          <div class="col-span-2">
            <label class="block mb-1">Observations</label>
            <textarea v-model="form.observations" required class="w-full p-2 border border-gray-300 rounded"></textarea>
          </div>
          <button type="submit" class="col-span-2 bg-blue-900 text-white px-4 py-2 rounded hover:bg-blue-800">{{ isEditing ? 'Update' : 'Add' }} Record</button>
        </form>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      record: {
        type: Object,
        default: () => ({
          title: '',
          description: '',
          experimentName: '',
          experimentType: '',
          sampleName: '',
          sampleSource: '',
          equipmentName: '',
          procedureStep: '',
          observations: '',
        }),
      },
    },
    data() {
      return {
        form: { ...this.record },
      };
    },
    computed: {
      isEditing() {
        return !!this.record._id;
      },
    },
    methods: {
      getAuthHeaders() {
        const token = localStorage.getItem('token');
        return {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${token}`,
        };
      },
      async submitForm() {
        const url = this.isEditing
          ? `https://labfront-api.onrender.com/records/${this.record._id}`
          : 'https://labfront-api.onrender.com/records';
        const method = this.isEditing ? 'PUT' : 'POST';
  
        await fetch(url, {
          method,
          headers: this.getAuthHeaders(),
          body: JSON.stringify(this.form),
        });
  
        this.$emit('recordUpdated');
        this.$emit('close');
      },
      close() {
        this.$emit('close');
      },
    },
  };
  </script>
  
  <style scoped>
  .modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.4);
  }
  
  .modal-content {
    background-color: #fff;
    margin: auto;
    padding: 20px;
    border: 1px solid #888;
    width: 80%;
  }
  
  .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
  }
  
  .close:hover,
  .close:focus {
    color: #000;
    text-decoration: none;
    cursor: pointer;
  }
  </style>
  