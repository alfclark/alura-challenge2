<template>
  <div class="notification-container" :class="show ? 'show' : ''">
    <p>You have already entered this letter</p>
  </div>
</template>

<script>
export default {
  props: { show: { type: Boolean, default: false } },
};
</script>

<style scoped>
.notification-container {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.3);
  color: var(--green);
  padding: 15px 20px;
  transition: opacity 0.3s ease-in-out;
  position: fixed;
  bottom: 10%;
  opacity: 0;
  width: 100%;
}

.notification-container p {
  margin: 0;
}

.notification-container.show {
  opacity: 1;
}
</style>
