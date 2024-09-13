<script setup>
// Define the prop for unreadCount
const props = defineProps({
  unreadCount: {
    type: Number,
    required: true,
  },
});

// Define the emit for the mark-read event
const emit = defineEmits(["mark-read"]);
</script>

<template>
  <div class="notifications-count-container">
    <div class="notifications-count-section">
      <h1>Notifications</h1>
      <h3>
        <span class="notifications-count">{{ unreadCount }}</span>
      </h3>
    </div>
    <p @click="$emit('mark-read')">Mark all as read</p>
  </div>
</template>

<style scoped>
.notifications-count-container {
  width: 95%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.notifications-count-container p:hover {
  cursor: pointer;
  color: var(--primary-color-blue);
}

.notifications-count-section {
  display: flex;
  align-items: center;
}

h1 {
  font-weight: 800;
  font-size: 28px;
}

.notifications-count {
  background-color: var(--primary-color-blue);
  color: var(--neutral-white);
  padding: 3px 12px;
  border-radius: 7px;
  margin-left: 10px;
}

.notifications-count-container p {
  color: var(--neutral-dark-grayish-blue);
}
</style>
