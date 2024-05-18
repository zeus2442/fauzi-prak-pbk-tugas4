<template>
  <div class="grandchild-container">
    <h3>Grandchild Component</h3>
    <input
      v-model="inputData"
      placeholder="Enter data to send"
      class="text-input"
    />
    <input type="file" @change="previewImage" class="file-input" />
    <button @click="sendData" class="send-button">Send Data to Parent</button>
    <img
      v-if="imageUrl"
      :src="imageUrl"
      alt="Preview Image"
      class="preview-image"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputData: "",
      imageUrl: null,
    };
  },
  methods: {
    sendData() {
      if (this.inputData.trim()) {
        this.$emit("grandChildData", this.inputData);
        this.$emit("grandChildImage", this.imageUrl);
        this.inputData = "";
        this.imageUrl = null;
      } else {
        alert("Please enter some data.");
      }
    },
    previewImage(event) {
      const file = event.target.files[0];
      if (file) {
        this.imageUrl = URL.createObjectURL(file);
      }
    },
  },
};
</script>

<style scoped>
.grandchild-container {
  padding: 30px;
  border: 2px solid #ff9800;
  border-radius: 15px;
  background: linear-gradient(135deg, #fff3e0, #ffe0b2);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  margin-top: 20px;
  text-align: center;
  transition: transform 0.3s, background 0.3s;
}
.grandchild-container:hover {
  transform: scale(1.05);
  background: linear-gradient(135deg, #ffe0b2, #ffcc80);
}
.text-input {
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid #ccc;
  border-radius: 5px;
  width: 80%;
  font-size: 16px;
  box-sizing: border-box;
}
.file-input {
  margin-top: 10px;
  padding: 5px;
}
.send-button {
  padding: 10px 20px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s, transform 0.3s;
}
.send-button:hover {
  background-color: #388e3c;
  transform: translateY(-2px);
}
.preview-image {
  margin-top: 20px;
  max-width: 100%;
  height: auto;
  border: 2px solid #ff9800;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
h3 {
  color: #d32f2f;
  font-family: "Comic Sans MS", cursive, sans-serif;
}
</style>
