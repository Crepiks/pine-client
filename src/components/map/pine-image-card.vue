<template>
  <div class="card">
    <div class="card-close" @click="$emit('close-card')">
      <i class="bx bx-x card-close-icon"></i>
    </div>
    <div
      class="card-image"
      :style="{ backgroundImage: `url(${imagePath})` }"
    ></div>
    <div class="card-info">
      <span class="card-label">Дата снимка:</span>
      <span class="card-data">{{ createdAtParsed }}</span>
    </div>
    <div class="card-info">
      <span class="card-label">Город:</span>
      <span class="card-data">{{ city }}</span>
    </div>
    <div class="card-info" v-if="device">
      <span class="card-label">Устройство:</span>
      <span class="card-data">{{ device }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imagePath: {
      type: String,
      required: true,
    },
    createdAt: {
      type: String,
      required: true,
    },
    city: {
      type: String,
      required: true,
    },
    device: {
      type: String,
      required: false,
    },
  },

  watch: {
    createdAt() {
      if (this.createdAt) {
        const createdAt = new Date(Date.parse(this.createdAt));
        this.createdAtParsed =
          String(createdAt.getDate()) +
          "/" +
          String(createdAt.getMonth() + 1) +
          "/" +
          String(createdAt.getFullYear());
      }
    },
  },

  mounted() {
    if (this.createdAt) {
      const createdAt = new Date(Date.parse(this.createdAt));
      this.createdAtParsed =
        String(createdAt.getDate()) +
        "/" +
        String(createdAt.getMonth() + 1) +
        "/" +
        String(createdAt.getFullYear());
    }
  },

  data() {
    return {
      createdAtParsed: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/variables.scss";

.card {
  padding: 30px 25px;
  width: 300px;
  width: 350px;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  border-radius: 10px;
  background-color: $white;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.2);

  &-close {
    position: absolute;
    right: -10px;
    top: -10px;
    width: 40px;
    height: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 50%;
    background-color: $white;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    transition: 200ms ease-in-out;
    cursor: pointer;

    &:hover {
      transform: translateX(-3px) translateY(3px);
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
    }

    &-icon {
      font-size: 22px;
    }
  }

  &-image {
    margin-bottom: 25px;
    width: 100%;
    height: 150px;
    border-radius: 10px;
    background-size: cover;
    background-position: center center;
    background-repeat: no-repeat;
    box-shadow: 0 0 30px rgba(0, 0, 0, 0.1);
  }

  &-info {
    margin-bottom: 8px;
    width: 100%;
    display: flex;
    align-items: center;
    color: $main-dark;
    font-size: 18px;
  }

  &-label {
    margin-right: 5px;
    font-weight: bold;
  }
}
</style>
