<template>
  <div class="child-container">
    <h2>Child Component</h2>
    <p>
      Data from Grandchild: <span class="data">{{ dataFromGrandchild }}</span>
    </p>
    <img
      v-if="imageFromGrandchild"
      :src="imageFromGrandchild"
      alt="Uploaded Image"
      class="uploaded-image"
    />
    <GrandChildComponent
      @grandChildData="handleGrandChildData"
      @grandChildImage="handleGrandChildImage"
    />
    <slot :message="slotMessage"></slot>
  </div>
</template>

<script>
import GrandChildComponent from "./GrandChildComponent.vue";

export default {
  components: {
    GrandChildComponent,
  },
  data() {
    return {
      dataFromGrandchild: null,
      imageFromGrandchild: null,
      slotMessage: "Hello from Child Component!",
    };
  },
  methods: {
    handleGrandChildData(data) {
      this.dataFromGrandchild = data;
      this.$emit("childData", data);
    },
    handleGrandChildImage(image) {
      this.imageFromGrandchild = image;
      this.$emit("childImage", image);
    },
  },
};
</script>

<style scoped>
.child-container {
  padding: 30px;
  border: 2px solid #2196f3;
  border-radius: 15px;
  background: linear-gradient(135deg, #f1f8e9, #aed581);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  margin-top: 20px;
  text-align: center;
  transition: transform 0.3s, background 0.3s;
}
.child-container:hover {
  transform: scale(1.05);
  background: linear-gradient(135deg, #aed581, #7cb342);
}
.data {
  color: #ff9800;
  font-weight: bold;
  animation: bounce 1.5s infinite;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.2);
}
@keyframes bounce {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}
.uploaded-image {
  margin-top: 20px;
  max-width: 100%;
  height: auto;
  border: 2px solid #ff9800;
  border-radius: 15px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}
h2 {
  color: #2e7d32;
  font-family: "Arial", sans-serif;
}
p {
  font-size: 18px;
  font-family: "Arial", sans-serif;
}
</style>
