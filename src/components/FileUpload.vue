<template>
  <div>
    <div>
      <label>姓名</label>
      <input type="text" @change="handleText">
    </div>
    <input type="file" @change="handleFileUpload">
    <div style="display: flex;justify-content: center;">
      <div style="margin-top: 50px;border: 1px solid black;width: 600px; height: 300px;">
        <img v-if="imageUrl" :src="imageUrl" alt="Preview Image" style="width: 600px; height: 300px;">
        <div v-else>No preview available</div>
      </div>
    </div>
    
    <!-- Add the button here -->
    <button @click="sendHttpRequest">Send HTTP Request</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      name: null,
      imageUrl: null,
    };
  },
  methods: {
    handleText(event) {
      this.name = event.target.value;
    },
    handleFileUpload(event) {
      const file = event.target.files[0];

      if (file) {
        const reader = new FileReader();

        reader.onload = () => {
          this.imageUrl = reader.result;
        };

        reader.readAsDataURL(file);
      } else {
        this.imageUrl = null;
      }
    },
    sendHttpRequest() {
      // Add your Axios HTTP request logic here
      // Example: sending a POST request to a hypothetical API endpoint
      axios.post('https://example.com/api/upload', { name: this.name, image: this.imageUrl })
        .then(response => {
          // Handle the response as needed
          console.log(response.data);
        })
        .catch(error => {
          // Handle errors
          console.error(error);
        });
    }
  }
};
</script>
