<template>
    <div class="bg-gray-900 text-white py-4 shadow-md">
        <div class="max-w-md mx-auto flex justify-between items-center">
          <router-link to="/dashboard" class="text-xl font-semibold">Remedial</router-link>
          <button @click="logout" class="bg-white text-gray-900 font-semibold py-2 px-4 rounded hover:bg-gray-200 focus:outline-none focus:shadow-outline">
            Logout
          </button>
        </div>
    </div>

      <div class="container mx-auto">
        <div class="flex justify-end mt-6">
            <router-link to="/dashboard/register-student" class="bg-gray-900 hover:bg-gray-800 text-sm text-white font-semibold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
              Add New
            </router-link>
        </div>
        <h1 class="text-2xl font-bold mb-4 mt-6">Student Results</h1>
        <div class="overflow-x-auto">
            <table class="min-w-full bg-white">
              <thead>
                <tr class="bg-gray-900 text-white">
                  <th class="py-2 px-4 border-b border-gray-800 text-left">SN</th>
                  <th class="py-2 px-4 border-b border-gray-800 text-left">Full Name</th>
                  <th class="py-2 px-4 border-b border-gray-800 text-left">Email</th>
                  <th class="py-2 px-4 border-b border-gray-800 text-left">Matric Number</th>
                  <th class="py-2 px-4 border-b border-gray-800 text-left">Actions</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(student, index) in students" :key="student._id" :class="index % 2 === 0 ? 'bg-gray-200' : 'bg-white'">
                  <td class="py-2 px-4 border-b border-gray-200 text-left text-sm font-semibold">{{ index + 1 }}</td>
                  <td class="py-2 px-4 border-b border-gray-200 text-left text-sm font-semibold">{{ student.fullName }}</td>
                  <td class="py-2 px-4 border-b border-gray-200 text-left text-sm font-semibold">{{ student.email }}</td>
                  <td class="py-2 px-4 border-b border-gray-200 text-left text-sm font-semibold">{{ student.matricNumber }}</td>
                  <td class="py-2 px-4 border-b border-gray-200 text-left">
                    <div class="inline-block">
                      <button @click="generatePDF(student.matricNumber)" class="bg-gray-900 hover:bg-gray-800 text-white text-sm font-semibold py-1 px-2 rounded">
                        Result PDF
                      </button>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
      </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      students: [],
    };
  },
  async created() {
    this.fetchStudents();
  },
  methods: {
    async fetchStudents() {
      try {
        const token = localStorage.getItem('token');
        const response = await axios.get('http://localhost:5000/api/remedial/students', {
          headers: {
            Authorization: `Bearer ${token}`,
          },
        });
        this.students = response.data;
      } catch (error) {
        console.error('Error fetching students:', error);
      }
    },
    async generatePDF(matricNumber) {
      try {
        const token = localStorage.getItem('token');
        const response = await axios.get(`http://localhost:5000/api/remedial/results/pdf?matricNumber=${matricNumber}`, {
          headers: {
            Authorization: `Bearer ${token}`,
          },
          responseType: 'blob',
        });

        // Create a link element
        const url = window.URL.createObjectURL(new Blob([response.data]));
        const link = document.createElement('a');
        link.href = url;
        link.setAttribute('download', `${matricNumber}_result.pdf`);
        document.body.appendChild(link);
        link.click();

        // Clean up
        document.body.removeChild(link);
        window.URL.revokeObjectURL(url);
      } catch (error) {
        console.error('Error generating PDF:', error);
      }
    },
    logout(){
        localStorage.removeItem('token');
        this.$router.push('/login')
    }
  },
};
</script>
