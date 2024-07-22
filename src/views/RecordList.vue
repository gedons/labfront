<template>
    <div class="bg-blue-900 text-white py-4 shadow-md">
        <div class="max-w-md mx-auto flex justify-between items-center">
          <router-link to="/dashboard/records" class="text-xl font-semibold">Lab Dashboard</router-link>
          <button @click="logout" class="bg-white text-gray-900 font-semibold py-2 px-4 rounded hover:bg-gray-200 focus:outline-none focus:shadow-outline">
            Logout
          </button>
        </div>
    </div>
    <div class="container bg-gray-100 mx-auto p-8">      
      <div class="flex items-center justify-between">
        <h2 class="text-2xl font-bold">Lab Records</h2>      
        <button @click="addRecord" class="mb-2 bg-blue-900 text-white px-6 py-2 rounded hover:bg-blue-800">Add New Record</button>
      </div>
      <ul class="space-y-4">
        <li v-for="record in records" :key="record._id" class="bg-white p-6 rounded-lg shadow-md">
          <h3 class="text-xl font-semibold mb-2">{{ record.title }}</h3>
          <p class="mb-2">{{ record.description }}</p>
          <div class="grid grid-cols-2 gap-4">
            <p><strong>Experiment Name:</strong> {{ record.experimentName }}</p>
            <p><strong>Experiment Type:</strong> {{ record.experimentType }}</p>
            <p><strong>Sample Name:</strong> {{ record.sampleName }}</p>
            <p><strong>Sample Source:</strong> {{ record.sampleSource }}</p>
            <p><strong>Equipment Name:</strong> {{ record.equipmentName }}</p>
            <p><strong>Procedure Step:</strong> {{ record.procedureStep }}</p>
            <p><strong>Observations:</strong> {{ record.observations }}</p>
            <p><strong>Date:</strong> {{ record.date }}</p>
          </div>
          <div class="mt-4">
            <button @click="editRecord(record)" class="bg-blue-900 text-white px-4 py-2 rounded hover:bg-blue-800 mr-2">Edit</button>
            <button @click="deleteRecord(record._id)" class="  text-red-500 px-4 py-2 rounded underline">Delete</button>
          </div>
        </li>
      </ul>      
      <RecordModal v-if="showModal" :record="selectedRecord" @recordUpdated="fetchRecords" @close="closeModal" />
    </div>
  </template>
  
  <script>
  import RecordModal from './RecordModal.vue';
  
  export default {
    data() {
      return {
        records: [],
        showModal: false,
        selectedRecord: null,
      };
    },
    methods: {
      getAuthHeaders() {
        const token = localStorage.getItem('token');
        return {
          'Content-Type': 'application/json',
          'Authorization': `Bearer ${token}`,
        };
      },
      async fetchRecords() {
        const res = await fetch('https://labfront-api.onrender.com/api/records', {
          headers: this.getAuthHeaders(),
        });
        this.records = await res.json();        
      },
      addRecord() {
        this.selectedRecord = {
          title: '',
          description: '',
          experimentName: '',
          experimentType: '',
          sampleName: '',
          sampleSource: '',
          equipmentName: '',
          procedureStep: '',
          observations: '',
        };
        this.showModal = true;
      },
      editRecord(record) {
        this.selectedRecord = { ...record };
        this.showModal = true;
      },
      async deleteRecord(id) {
        confirm("Are you sure you want to delete this record");
        await fetch(`https://labfront-api.onrender.com/api/records/${id}`, {
          method: 'DELETE',
          headers: this.getAuthHeaders(),
        });
        this.fetchRecords();
      },
      logout(){
        localStorage.removeItem('token');
        this.$router.push('/')
      },
      closeModal() {
        this.showModal = false;
        this.selectedRecord = null;
      },
    },
    created() {
      this.fetchRecords();
    },
    components: {
      RecordModal,
    },
  };
  </script>
  