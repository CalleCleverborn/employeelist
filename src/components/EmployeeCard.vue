<template>
    <div class="employee-card">
      <img :src="employee.avatar" alt="Profile Picture" class="avatar">
      <div class="employee-details">
        <h2>{{ employee.first_name }} {{ employee.last_name }}</h2>
        <a :href="`mailto:${employee.email}`">{{ employee.email }}</a>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      employee: Object
    }
  }
  </script>
  
  <style scoped>
  .employee-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    border: 1px solid #e0e0e0;
    border-radius: 10px;
    background-color: white;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s;
  }
  
  .employee-card:hover {
    transform: scale(1.05);
  }
  
  .avatar {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin-bottom: 15px;
  }
  
  .employee-details {
    text-align: center;
  }
  
  .employee-details h2 {
    font-size: 18px;
    margin: 0 0 10px 0;
  }
  
  .employee-details a {
    font-size: 16px;
    color: #007bff;
    text-decoration: none;
  }
  
  .employee-details a:hover {
    text-decoration: underline;
  }
  
  @media (max-width: 768px) {
    .employee-card {
      padding: 15px;
    }
  
    .avatar {
      width: 80px;
      height: 80px;
    }
  
    .employee-details h2 {
      font-size: 16px;
    }
  
    .employee-details a {
      font-size: 14px;
    }
  }
  </style>
  