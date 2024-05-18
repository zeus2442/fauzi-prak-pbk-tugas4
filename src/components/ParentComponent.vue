<template>
  <div class="parent-container">
    <h1>Parent Component</h1>
    <p>
      Data from Child: <span class="data">{{ dataFromChild }}</span>
    </p>
    <img
      v-if="imageFromChild"
      :src="imageFromChild"
      alt="Uploaded Image"
      class="uploaded-image"
    />
    <ChildComponent @childData="handleChildData" @childImage="handleChildImage">
      <template v-slot:default="{ message }">
        <div class="slot-content">
          <h2>Message from Slot:</h2>
          <p>{{ message }}</p>
        </div>
      </template>
    </ChildComponent>
  </div>
</template>

<script>
import ChildComponent from "./ChildComponent.vue";

export default {
  components: {
    ChildComponent,
  },
  data() {
    return {
      dataFromChild: null,
      imageFromChild: null,
    };
  },
  methods: {
    handleChildData(data) {
      this.dataFromChild = data;
    },
    handleChildImage(image) {
      this.imageFromChild = image;
    },
  },
};
</script>

<style scoped>
.parent-container {
  padding: 30px;
  border: 2px solid #4caf50;
  border-radius: 15px;
  background: linear-gradient(135deg, #e0f7fa, #80deea);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  text-align: center;
  transition: transform 0.3s, background 0.3s;
}
.parent-container:hover {
  transform: scale(1.05);
  background: linear-gradient(135deg, #80deea, #26c6da);
}
.data {
  color: #ff5722;
  font-weight: bold;
  animation: highlight 1.5s infinite;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}
@keyframes highlight {
  0% {
    color: #ff5722;
  }
  50% {
    color: #ffccbc;
  }
  100% {
    color: #ff5722;
  }
}
.slot-content {
  margin-top: 20px;
  padding: 20px;
  border: 2px dashed #2196f3;
  border-radius: 15px;
  background: linear-gradient(135deg, #e3f2fd, #bbdefb);
  animation: fadeIn 1s;
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.uploaded-image {
  margin-top: 20px;
  max-width: 100%;
  height: auto;
  border: 2px solid #2196f3;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
h1,
h2 {
  color: #2c3e50;
  font-family: "Arial", sans-serif;
}
p {
  font-size: 18px;
  font-family: "Arial", sans-serif;
}
</style>
