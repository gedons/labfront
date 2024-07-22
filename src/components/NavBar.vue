<template>
  <nav class="bg-gray-200 shadow shadow-gray-300 w-100 px-8 md:px-auto">
    <div class="md:h-16 h-28 mx-auto md:px-4 container flex items-center justify-between flex-wrap md:flex-nowrap">
      <!-- Logo -->
      <div class="text-gray-900 md:order-1 flex">
        <!-- Heroicon - Chip Outline -->
       <svg fill="#000000" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 512 512" xml:space="preserve" class="h-10 w-10"><g id="SVGRepo_bgCarrier" stroke-width="0"></g><g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g><g id="SVGRepo_iconCarrier"> <g> <g> <path d="M106.661,298.651c-25.872,0-46.921,21.048-46.921,46.921c0,25.872,21.049,46.921,46.921,46.921 c25.872,0,46.921-21.049,46.921-46.921C153.582,319.699,132.533,298.651,106.661,298.651z M106.661,375.43 c-16.462,0-29.859-13.397-29.859-29.859c0-16.462,13.397-29.859,29.859-29.859c16.462,0,29.859,13.396,29.859,29.859 C136.519,362.034,123.123,375.43,106.661,375.43z"></path> </g> </g> <g> <g> <path d="M217.565,298.651c-25.872,0-46.921,21.048-46.921,46.921c0,25.872,21.049,46.921,46.921,46.921 c25.872,0,46.921-21.049,46.921-46.921C264.485,319.699,243.437,298.651,217.565,298.651z M217.565,375.43 c-16.462,0-29.859-13.397-29.859-29.859c0-16.462,13.397-29.859,29.859-29.859c16.462,0,29.859,13.396,29.859,29.859 C247.423,362.034,234.027,375.43,217.565,375.43z"></path> </g> </g> <g> <g> <path d="M413.779,298.651c-25.872,0-46.921,21.048-46.921,46.921c0,25.872,21.049,46.921,46.921,46.921 c25.872,0,46.921-21.049,46.921-46.921C460.7,319.699,439.651,298.651,413.779,298.651z M413.779,375.43 c-16.462,0-29.859-13.397-29.859-29.859c0-16.462,13.396-29.859,29.859-29.859c16.462,0,29.859,13.396,29.859,29.859 C443.637,362.034,430.241,375.43,413.779,375.43z"></path> </g> </g> <g> <g> <path d="M460.583,271.711c-2.92-17.533-12.084-58.295-34.008-58.295h-34.124c-4.711,0-7.542,3.744-7.542,8.455v51.186 c0,4.711,2.83,8.607,7.542,8.607h59.717c2.508,0,4.89-1.141,6.511-3.053C460.3,276.695,460.995,274.186,460.583,271.711z M401.972,264.603v-34.124h24.6c3.841,0,10.822,14.929,15.192,34.124H401.972z"></path> </g> </g> <g> <g> <rect x="316.651" y="170.758" width="17.062" height="127.966"></rect> </g> </g> <g> <g> <rect x="248.403" y="187.82" width="17.062" height="102.373"></rect> </g> </g> <g> <g> <rect x="180.155" y="196.351" width="17.062" height="76.78"></rect> </g> </g> <g> <g> <rect x="111.906" y="221.944" width="17.062" height="42.655"></rect> </g> </g> <g> <g> <rect x="282.527" y="349.91" width="68.248" height="17.062"></rect> </g> </g> <g> <g> <path d="M465.219,180.55c-1.354-0.845-2.92-1.258-4.52-1.258h-86.454V128.03c0-2.529-0.742-4.924-2.679-6.544 c-1.937-1.625-4.331-2.274-6.793-1.854L32.544,179.35c-3.599,0.65-6.339,3.516-6.881,7.131L0.094,357.102 c-0.371,2.458,0.362,4.991,1.982,6.87c1.62,1.883,3.995,3.003,6.477,3.003h26.583v-17.062H18.46L41.3,195.1l315.883-56.869v49.516 c0,4.711,4.576,8.607,9.287,8.607h91.705c51.449,34.124,35.332,127.966,29.88,153.559h-9.304v17.062h16.073 c3.866,0,7.248-2.618,8.244-6.35C504.526,355.152,537.979,226.025,465.219,180.55z"></path> </g> </g> </g></svg>
        <span class="mt-2 ml-2">FleetTrack</span>
      </div>
      <div class="text-gray-500 order-3 w-full md:w-auto md:order-2">
        <ul class="flex  justify-between">                
          <li class="md:px-2   text-gray-800 hover:text-gray-500"><router-link to="/">Home</router-link></li>
          <li class="md:px-2 text-gray-800 hover:text-gray-500"><router-link to="/track">Track Vehicle</router-link></li>
          <li v-if="loggedIn" class="md:px-2 text-gray-800 hover:text-gray-700"><router-link to="/dashboard/cars/add">Add Vehicle</router-link></li>
          <li v-if="loggedIn" class="md:px-2 text-gray-800 hover:text-gray-700"><router-link to="/dashboard/cars">Vehicle Lists</router-link></li>          
          <li v-if="loggedIn" class="md:px-2 text-gray-800 hover:text-gray-700"><router-link to="/dashboard/cars/simulate">Simulate Vehicle</router-link></li>          
          <!-- <li class="md:px-4 md:py-2 hover:text-gray-400"><router-link to="/register">Register</router-link></li> -->
         
        </ul> 
          
            
      </div>
      <div class="order-2 md:order-3">
        <button v-if="loggedIn" @click="logout"  class="px-4 py-2 bg-gray-800 hover:bg-gray-900 text-gray-50 rounded-xl flex items-center gap-2">
                  <!-- Heroicons - Login Solid -->
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M3 3a1 1 0 011 1v12a1 1 0 11-2 0V4a1 1 0 011-1zm7.707 3.293a1 1 0 010 1.414L9.414 9H17a1 1 0 110 2H9.414l1.293 1.293a1 1 0 01-1.414 1.414l-3-3a1 1 0 010-1.414l3-3a1 1 0 011.414 0z" clip-rule="evenodd" />
                  </svg>
                  <span>Log out</span>
          </button>

          <button v-else class="px-4 py-2 bg-gray-500 hover:bg-gray-600 text-gray-50 rounded-xl flex items-center gap-2">           
            <span><router-link to="/login">Get started</router-link></span>
        </button>
      </div>
    </div>
  </nav>
  </template>
  
  <script>
    import { ref, onMounted } from 'vue';
    import { useRouter } from 'vue-router';
    import { isLoggedIn, logout } from '../utils/auth';

    export default {
      name: 'Navbar',

      setup() {
        const router = useRouter();
        const loggedIn = ref(false);

        onMounted(() => {
          loggedIn.value = isLoggedIn();
        });

        const handleLogout = () => {
          logout();
          loggedIn.value = false;
          router.push('/login');
        };

        return {
          loggedIn,
          logout: handleLogout,
          router,
        };
      },
    };
  </script>
  