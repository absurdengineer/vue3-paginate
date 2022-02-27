<template>
  <ul
    :class="{
      'vue3-paginate-pagination-container': [undefined, null, ''].includes(
        paginationContainerClass
      ),
      [paginationContainerClass]: paginationContainerClass,
    }"
    v-if="totalPage"
  >
    <li
      :style="sizeStyle"
      :class="{
        'vue3-paginate-not-allowed': 1 >= currentPage,
        'vue3-paginate-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        [paginationItemClass]: paginationItemClass,
      }"
      @click="1 >= currentPage ? null : handlePageChange(1)"
    >
      <a
        :title="firstTitle"
        :class="{
          [paginationLinkClass]: paginationLinkClass,
          'vue3-paginate-not-allowed': 1 >= currentPage,
        }"
      >
        <svg
          :style="iconSizeStyle"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 320 512"
        >
          <!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
          <path
            d="M31.1 64.03c-17.67 0-31.1 14.33-31.1 32v319.9c0 17.67 14.33 32 32 32C49.67 447.1 64 433.6 64 415.1V96.03C64 78.36 49.67 64.03 31.1 64.03zM267.5 71.41l-192 159.1C67.82 237.8 64 246.9 64 256c0 9.094 3.82 18.18 11.44 24.62l192 159.1c20.63 17.12 52.51 2.75 52.51-24.62v-319.9C319.1 68.66 288.1 54.28 267.5 71.41z"
          /></svg
      ></a>
    </li>
    <li
      :style="sizeStyle"
      :class="{
        'vue3-paginate-not-allowed': 1 >= currentPage,
        'vue3-paginate-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        [paginationItemClass]: paginationItemClass,
      }"
      @click="1 >= currentPage ? null : handlePageChange(currentPage - 1)"
    >
      <a
        :title="previousTitle"
        :class="{
          'vue3-paginate-not-allowed': 1 >= currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
      >
        <svg
          :style="iconSizeStyle"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 448 512"
        >
          <!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
          <path
            d="M77.25 256l137.4-137.4c12.5-12.5 12.5-32.75 0-45.25s-32.75-12.5-45.25 0l-160 160c-12.5 12.5-12.5 32.75 0 45.25l160 160C175.6 444.9 183.8 448 192 448s16.38-3.125 22.62-9.375c12.5-12.5 12.5-32.75 0-45.25L77.25 256zM269.3 256l137.4-137.4c12.5-12.5 12.5-32.75 0-45.25s-32.75-12.5-45.25 0l-160 160c-12.5 12.5-12.5 32.75 0 45.25l160 160C367.6 444.9 375.8 448 384 448s16.38-3.125 22.62-9.375c12.5-12.5 12.5-32.75 0-45.25L269.3 256z"
          /></svg
      ></a>
    </li>
    <li
      v-for="i in range"
      :style="sizeStyle"
      @click="i === currentPage ? null : handlePageChange(i)"
      :class="{
        'vue3-paginate-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        'vue3-paginate-not-allowed': i === currentPage,
        'vue3-paginate-active':
          [undefined, null, ''].includes(paginationItemClass) &&
          i === currentPage,
        [paginationItemActiveClass]:
          paginationItemActiveClass && i === currentPage,
        [paginationItemClass]: paginationItemClass,
      }"
      :key="i"
    >
      <a
        :class="{
          'vue3-paginate-not-allowed': i === currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
        >{{ i }}</a
      >
    </li>
    <li
      :style="sizeStyle"
      :class="{
        'vue3-paginate-not-allowed': totalPage <= currentPage,
        'vue3-paginate-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        [paginationItemClass]: paginationItemClass,
      }"
      @click="
        totalPage <= currentPage ? null : handlePageChange(currentPage + 1)
      "
    >
      <a
        :title="nextTitle"
        :class="{
          'vue3-paginate-not-allowed': totalPage <= currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
      >
        <svg
          :style="iconSizeStyle"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 448 512"
        >
          <!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
          <path
            d="M246.6 233.4l-160-160c-12.5-12.5-32.75-12.5-45.25 0s-12.5 32.75 0 45.25L178.8 256l-137.4 137.4c-12.5 12.5-12.5 32.75 0 45.25C47.63 444.9 55.81 448 64 448s16.38-3.125 22.62-9.375l160-160C259.1 266.1 259.1 245.9 246.6 233.4zM438.6 233.4l-160-160c-12.5-12.5-32.75-12.5-45.25 0s-12.5 32.75 0 45.25L370.8 256l-137.4 137.4c-12.5 12.5-12.5 32.75 0 45.25C239.6 444.9 247.8 448 256 448s16.38-3.125 22.62-9.375l160-160C451.1 266.1 451.1 245.9 438.6 233.4z"
          />
        </svg>
      </a>
    </li>
    <li
      :style="sizeStyle"
      :class="{
        'vue3-paginate-not-allowed': totalPage <= currentPage,
        'vue3-paginate-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        [paginationItemClass]: paginationItemClass,
      }"
      @click="totalPage <= currentPage ? null : handlePageChange(totalPage)"
    >
      <a
        :title="lastTitle"
        :class="{
          'vue3-paginate-not-allowed': totalPage <= currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
        ><svg
          :style="iconSizeStyle"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 320 512"
        >
          <!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
          <path
            d="M287.1 447.1c17.67 0 31.1-14.33 31.1-32V96.03c0-17.67-14.33-32-32-32c-17.67 0-31.1 14.33-31.1 31.1v319.9C255.1 433.6 270.3 447.1 287.1 447.1zM52.51 440.6l192-159.1c7.625-6.436 11.43-15.53 11.43-24.62c0-9.094-3.809-18.18-11.43-24.62l-192-159.1C31.88 54.28 0 68.66 0 96.03v319.9C0 443.3 31.88 457.7 52.51 440.6z"
          /></svg
      ></a>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    currentPage: {
      type: Number,
      default: 1,
    },
    pageCount: {
      type: Number,
      default: 5,
    },
    totalPage: {
      type: Number,
      default: 1,
    },
    paginationItemClass: {
      type: String,
    },
    paginationLinkClass: {
      type: String,
    },
    paginationContainerClass: {
      type: String,
    },
    paginationItemActiveClass: {
      type: String,
    },
    height: {
      type: [String, Number],
      default: "35px",
    },
    width: {
      type: [String, Number],
      default: "35px",
    },
    firstTitle: {
      type: String,
      default: "First",
    },
    previousTitle: {
      type: String,
      default: "Previous",
    },
    nextTitle: {
      type: String,
      default: "Next",
    },
    lastTitle: {
      type: String,
      default: "Last",
    },
  },
  emits: ["pageChange"],
  methods: {
    handlePageChange(page) {
      this.$emit("pageChange", page);
    },
  },
  computed: {
    start() {
      return this.currentPage >
        this.totalPage - Math.floor((this.pageCount - 1) / 2)
        ? this.totalPage - (this.pageCount - 1)
        : this.currentPage - Math.floor((this.pageCount - 1) / 2);
    },
    end() {
      return this.currentPage <= Math.floor(this.pageCount / 2)
        ? this.pageCount
        : this.currentPage + Math.floor(this.pageCount / 2);
    },
    range() {
      const pages = [];
      for (let i = this.start; i <= this.end; i++) {
        if (i > 0 && i <= this.totalPage) {
          pages.push(i);
        }
      }
      return pages;
    },
    sizeStyle() {
      return { height: this.height, width: this.width };
    },
    iconSizeStyle() {
      const height = parseInt(this.height.replace("px", "") - 10);
      const width = parseInt(this.width.replace("px", "") - 10);
      return { height, width };
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Gideon+Roman&display=swap");
* {
  margin: 0;
  padding: 0;
}
.vue3-paginate-pagination-container {
  font-family: "Gideon Roman", cursive;
  display: flex;
}
.vue3-paginate-pagination-item {
  cursor: pointer;
  color: white;
  background: whitesmoke;
  border: 1px solid #dee2e6;
  margin: 2px;
  padding: 4px;
  font-size: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.vue3-paginate-pagination-item a {
  color: black;
  text-decoration: none;
  display: flex;
  padding: auto;
}
.vue3-paginate-pagination-item a img {
  user-drag: none;
  -webkit-user-drag: none;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
.vue3-paginate-active {
  border-radius: 100%;
  background: #0f5298;
}
.vue3-paginate-active a {
  color: #fff;
  font-weight: bold;
}
.vue3-paginate-not-allowed {
  cursor: not-allowed;
}
</style>
