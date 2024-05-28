<template>
    <div class="employee-list">
      <div class="employee-cards">
        <div v-for="employee in employees" :key="employee.id" class="employee-card-wrapper">
          <EmployeeCard :employee="employee" />
        </div>
      </div>
      <div class="pagination">
        <button @click="prevPage" :disabled="page === 1">Previous</button>
        <span>Page {{ page }} of {{ totalPages }}</span>
        <button @click="nextPage" :disabled="page === totalPages">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import EmployeeCard from './EmployeeCard.vue';
  
  export default {
    components: {
      EmployeeCard
    },
    data() {
      return {
        employees: [],
        page: 1,
        totalPages: 1
      };
    },
    methods: {
      fetchEmployees(page) {
        axios.get(`https://reqres.in/api/users?page=${page}`)
          .then(response => {
            this.employees = response.data.data;
            this.page = response.data.page;
            this.totalPages = response.data.total_pages;
          });
      },
      nextPage() {
        if (this.page < this.totalPages) {
          this.page++;
          this.fetchEmployees(this.page);
        }
      },
      prevPage() {
        if (this.page > 1) {
          this.page--;
          this.fetchEmployees(this.page);
        }
      }
    },
    created() {
      this.fetchEmployees(this.page);
    }
  }
  </script>
  
  <style scoped>
  .employee-list {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  
  .employee-cards {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
    margin-bottom: 20px;
  }
  
  .employee-card-wrapper {
    width: calc(33% - 20px);
    box-sizing: border-box;
  }
  
  .pagination {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .pagination button {
    padding: 10px 20px;
    font-size: 16px;
    border: none;
    background-color: #007bff;
    color: white;
    cursor: pointer;
    border-radius: 5px;
  }
  
  .pagination button:disabled {
    background-color: #cccccc;
  }
  
  .pagination span {
    font-size: 16px;
  }
  
  @media (max-width: 1024px) {
    .employee-card-wrapper {
      width: calc(50% - 20px);
    }
  }
  
  @media (max-width: 768px) {
    .employee-card-wrapper {
      width: calc(100% - 20px);
    }
  
    .pagination button {
      padding: 8px 16px;
      font-size: 14px;
    }
  
    .pagination span {
      font-size: 14px;
    }
  }
  </style>
  