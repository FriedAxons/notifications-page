<script setup>
import { ref, computed } from "vue";
import NotificationsCount from "./NotificationsCount.vue";

// Hardcoded notifications data
const notifications = ref([
  {
    id: 1,
    name: "Mark Webber",
    action: "reacted to your recent post",
    postTitle: "My first tournament today!",
    time: "1m ago",
    unread: true,
  },
  {
    id: 2,
    name: "Angela Gray",
    action: "followed you",
    time: "5m ago",
    unread: true,
  },
  {
    id: 3,
    name: "Jacob Thompson",
    action: "has joined your group",
    group: "Chess Club",
    time: "1 day ago",
    unread: true,
  },
  {
    id: 4,
    name: "Rizky Hasanuddin",
    action: "has sent you a private message",
    message:
      "Hello, thanks for setting up the Chess Club. I've been a member for a few weeks now and I'm already having lots of fun and improving my game.",
    time: "5 days ago",
    unread: false,
  },
  {
    id: 5,
    name: "Kimberly Smith",
    action: "commented on your picture",
    time: "1 week ago",
    unread: false,
    reactedToImage: "/public/images/avatar-image-chess.webp",
  },
  {
    id: 6,
    name: "Nathan Peterson",
    action: "reacted to your recent post",
    postTitle: "5 end-game strategies to increase your win rate",
    time: "2 weeks ago",
    unread: false,
  },
  {
    id: 7,
    name: "Anna Kim",
    action: "left the group",
    group: "Chess Club",
    time: "2 weeks ago",
    unread: false,
  },
]);

// Computed property for unread notifications count
const unreadNotificationsCount = computed(() => {
  return notifications.value.filter((notification) => notification.unread)
    .length;
});

// Mark all notifications as read
const markAllAsRead = () => {
  notifications.value.forEach((notification) => (notification.unread = false));
};
</script>

<template>
  <div class="notification-posts">
    <NotificationsCount
      :unreadCount="unreadNotificationsCount"
      @mark-read="markAllAsRead"
    />
    <div
      v-for="notification in notifications"
      :key="notification.id"
      class="post"
      :class="{ 'unread-post': notification.unread }"
    >
      <div class="image-text">
        <img
          :src="`images/avatar-${notification.name
            .toLowerCase()
            .replace(' ', '-')}.webp`"
          alt="Profile picture"
        />
        <div class="text-container">
          <p>
            <b class="name">{{ notification.name }}</b>
            {{ notification.action }}
            <span v-if="notification.postTitle" class="post-text-span"
              ><b>{{ notification.postTitle }}</b></span
            >
            <span v-if="notification.group" class="group-text-span"
              ><b>{{ notification.group }}</b></span
            >
            <span v-if="notification.unread" class="dot"></span>
          </p>
          <span class="time-spent-span">{{ notification.time }}</span>
          <p v-if="notification.message" class="message">
            {{ notification.message }}
          </p>
        </div>
        <img
          v-if="notification.reactedToImage"
          :src="notification.reactedToImage"
          alt="Reacted post image"
          class="repliedToImage"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.notification-posts {
  width: 35%;
  box-shadow: 0px 4px 20px hsla(219, 14%, 63%, 0.2);
}

.post {
  margin-top: 40px;
  margin-left: 10px;
  padding: 0 0 15px 12px;
}

.image-text {
  display: flex;
  align-items: flex-start; /* Align items to the top of the profile picture */
  gap: 15px;
}

.image-text img {
  width: 50px;
  border-radius: 50%; /* Optional: to make the profile picture round */
}

.image-text .repliedToImage {
  cursor: pointer;
  border-radius: 0;
  object-fit: cover;
  margin-left: auto;
  margin-right: 50px;
}

.name:hover {
  cursor: pointer;
  color: var(--primary-color-blue);
}

.text-container {
  display: flex;
  flex-direction: column;
}

.text-container p {
  margin: 0; /* Remove margin from the paragraph */
}

.message {
  border: 1px solid var(--neutral-light-grayish-blue-two);
  width: 89%;
  padding: 18px;
}

.message:hover {
  cursor: pointer;
  background-color: var(--neutral-light-grayish-blue-two);
}

.post-text-span:hover {
  cursor: pointer;
  color: var(--primary-color-blue);
}

.time-spent-span {
  margin: 5px 0 8px; /* Adds spacing between notification text and time */
}

.dot {
  display: inline-block;
  vertical-align: middle;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  margin-left: 5px;
  background-color: var(--primary-color-red);
}

/* Color Styles */
.notification-posts {
  background-color: var(--neutral-white);
}

.name {
  color: var(--neutral-very-dark-blue);
}

.post p {
  color: var(--neutral-dark-grayish-blue);
}

.post-text-span {
  color: var(--neutral-dark-grayish-blue);
}

.group-text-span {
  color: var(--primary-color-blue);
  cursor: pointer;
}

.time-spent-span {
  color: var(--neutral-grayish-blue);
}
</style>
