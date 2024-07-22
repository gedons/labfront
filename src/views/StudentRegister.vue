<template>
    <div class="bg-gray-900 text-white py-4 shadow-md">
        <div class="max-w-md mx-auto flex justify-between items-center">
            <router-link to="/dashboard" class="text-xl font-semibold">Remedial</router-link>
          <button @click="logout" class="bg-white text-gray-900 font-semibold py-2 px-4 rounded hover:bg-gray-200 focus:outline-none focus:shadow-outline">
            Logout
          </button>
        </div>
      </div>
    <div class="max-w-4xl mx-auto my-8 bg-white rounded-lg shadow-md p-6">
      <div>    
        <h2 class="mb-3">Upload Scanned Document</h2>
        <form @submit.prevent="uploadDocument">
          <input type="file" @change="handleFileUpload" required />
          <button class="py-3 px-3 bg-gray-900 hover:bg-gray-600 rounded-lg text-white" type="submit">Upload</button>
        </form>        

        <!-- Uploaded Content Display -->
        <div v-if="uploadedContent" class="mt-4 bg-gray-900 p-4 rounded-lg shadow-md">
          <h3 class="text-lg font-semibold mb-2 text-white">Uploaded Content:</h3>
          <pre class="bg-white p-4 rounded-lg border border-gray-300 overflow-auto">{{ uploadedContent }}</pre>
        </div>
      </div>
      <form @submit.prevent="registerStudent">
        <div class="mb-4 mt-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="fullName">
            Student Full Name
          </label>
          <input v-model="student.fullName" id="fullName" name="fullName" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="email">
            Email Address
          </label>
          <input v-model="student.email" id="email" name="email" type="email" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="courseOfStudy">
            Course of Study
          </label>
          <input v-model="student.courseOfStudy" id="courseOfStudy" name="courseOfStudy" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="department">
            Department
          </label>
          <input v-model="student.department" id="department" name="department" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="academicSession">
            Academic Session
          </label>
          <input v-model="student.academicSession" id="academicSession" name="academicSession" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="matricNumber">
            Matric Number
          </label>
          <input v-model="student.matricNumber" id="matricNumber" name="matricNumber" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="mobileNumber">
            Mobile Number
          </label>
          <input v-model="student.mobileNumber" id="mobileNumber" name="mobileNumber" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
  
        <!-- Courses -->
        <div v-for="(course, index) in student.courses" :key="index" class="border rounded p-4 mb-4">
          <h3 class="text-lg font-bold mb-2">Course {{ index + 1 }}</h3>
          <div class="grid grid-cols-2 gap-4">
            <div class="mb-2">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="courseCode">
                Course Code
              </label>
              <input v-model="course.courseCode" id="courseCode" name="courseCode" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>
            <div class="mb-2">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="courseTitle">
                Course Title
              </label>
              <input v-model="course.courseTitle" id="courseTitle" name="courseTitle" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>
            <div class="mb-2">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="courseCreditUnit">
                Credit Unit
              </label>
              <input v-model="course.courseCreditUnit" id="courseCreditUnit" name="courseCreditUnit" type="number" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>
            <div class="mb-2">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="courseLecturer">
                Course Lecturer
              </label>
              <input v-model="course.courseLecturer" id="courseLecturer" name="courseLecturer" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>
            <div class="mb-2">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="yearOfExam">
                Year of Exam
              </label>
              <input v-model="course.yearOfExam" id="yearOfExam" name="yearOfExam" type="number" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>
            <div class="mb-2">
              <label class="block text-gray-700 text-sm font-bold mb-2" for="grade">
                Grade
              </label>
              <input v-model="course.grade" id="grade" name="grade" type="text" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>
          </div>
          <button type="button" @click="removeCourse(index)" class="text-red-500 hover:text-red-700 font-semibold">
            Remove Course
          </button>
        </div>
  
        <!-- Button to add new course -->
        <button type="button" @click="addCourse" class="text-blue-500 underline font-semibold py-2 px-4 rounded focus:outline-none focus:shadow-outline mb-4">
          + Add Course 
        </button>
  
        <!-- Total courses failed -->
        <div class="mb-4">
          <label class="block text-gray-700 text-sm font-bold mb-2" for="totalCoursesFailed">
            Total Number of Courses Failed
          </label>
          <input v-model.number="student.totalCoursesFailed" id="totalCoursesFailed" name="totalCoursesFailed" type="number" required class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
        </div>
  
        <button type="submit" class="bg-gray-900 hover:bg-gray-800 text-white font-semibold py-2 px-4 rounded focus:outline-none focus:shadow-outline">
          Register Student
        </button>
      </form>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  export default {
    data() {
      return {
        file: null,
        uploadedContent: null,
        student: { 
          fullName: '',
          email: '',
          courseOfStudy: '',
          department: '',
          academicSession: '',
          matricNumber: '',
          mobileNumber: '',
          courses: [
            {
              courseCode: '',
              courseTitle: '',
              courseCreditUnit: '',
              courseLecturer: '',
              yearOfExam: '',
              grade: '',
            },
          ],
          totalCoursesFailed: '',
        },
      };
    },
    methods: {
      handleFileUpload(event) {
        this.file = event.target.files[0];
      },
      async uploadDocument() {
        try {
          const formData = new FormData();
          formData.append('file', this.file);

          const response = await axios.post('http://localhost:5000/api/remedial/upload', formData, {
            headers: {
              'Content-Type': 'multipart/form-data',
              Authorization: `Bearer ${localStorage.getItem('token')}`,
            },
          });
          alert('Uploaded Successfully!!');
          this.uploadedContent = response.data.content;
        } catch (error) {
          alert('Error uploading document');
          console.error(error);
        }
      },
      addCourse() {
        this.student.courses.push({
          courseCode: '',
          courseTitle: '',
          courseCreditUnit: '',
          courseLecturer: '',
          yearOfExam: '',
          grade: '',
        });
      },
      removeCourse(index) {
        this.student.courses.splice(index, 1);
      },
      async registerStudent() {
        try {
            const token = localStorage.getItem('token');  
            if (!token) {
            throw new Error('No token available');
            }

            console.log(token);

            // Construct headers with bearer token
            const headers = {
            'Authorization': `Bearer ${token}`,
            'Content-Type': 'application/json',
            };

          
          const response = await axios.post('http://localhost:5000/api/remedial/register', this.student, {headers});
          alert('Student registered successfully');
          this.$router.push('/dashboard')
          this.student = {
            fullName: '',
            email: '',
            courseOfStudy: '',
            department: '',
            academicSession: '',
            matricNumber: '',
            mobileNumber: '',
            courses: [
              {
                courseCode: '',
                courseTitle: '',
                courseCreditUnit: '',
                courseLecturer: '',
                yearOfExam: '',
                grade: '',
              },
            ],
            totalCoursesFailed: '',
          };
        } catch (error) {
          alert('Error registering student');
          console.error(error);
        }
      },
      logout(){
        localStorage.removeItem('token');
        this.$router.push('/login')
    }
    },
  };
  </script>
  
  <style>
  /* Tailwind CSS classes can be used directly in your components */
  </style>
  