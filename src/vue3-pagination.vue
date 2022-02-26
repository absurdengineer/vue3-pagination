<template>
  <ul
    :class="{
      'vue3-pagination-pagination-container': [undefined, null, ''].includes(
        paginationContainerClass
      ),
      [paginationContainerClass]: paginationContainerClass,
    }"
    v-if="totalPage"
  >
    <li
      :style="sizeStyle"
      :class="{
        'vue3-pagination-not-allowed': 1 >= currentPage,
        'vue3-pagination-pagination-item': [undefined, null, ''].includes(
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
          'vue3-pagination-not-allowed': 1 >= currentPage,
        }"
        ><img src="./assets/first.png" :style="sizeStyle" alt=""
      /></a>
    </li>
    <li
      :style="sizeStyle"
      :class="{
        'vue3-pagination-not-allowed': 1 >= currentPage,
        'vue3-pagination-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        [paginationItemClass]: paginationItemClass,
      }"
      @click="1 >= currentPage ? null : handlePageChange(currentPage - 1)"
    >
      <a
        :title="previousTitle"
        :class="{
          'vue3-pagination-not-allowed': 1 >= currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
      >
        <img src="./assets/previous.png" :style="sizeStyle" alt=""
      /></a>
    </li>
    <li
      v-for="i in range"
      :style="sizeStyle"
      @click="i === currentPage ? null : handlePageChange(i)"
      :class="{
        'vue3-pagination-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        'vue3-pagination-not-allowed': i === currentPage,
        'vue3-pagination-active':
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
          'vue3-pagination-not-allowed': i === currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
        >{{ i }}</a
      >
    </li>
    <li
      :style="sizeStyle"
      :class="{
        'vue3-pagination-not-allowed': totalPage <= currentPage,
        'vue3-pagination-pagination-item': [undefined, null, ''].includes(
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
          'vue3-pagination-not-allowed': totalPage <= currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
      >
        <img src="./assets/next.png" :style="sizeStyle" alt="" />
      </a>
    </li>
    <li
      :style="sizeStyle"
      :class="{
        'vue3-pagination-not-allowed': totalPage <= currentPage,
        'vue3-pagination-pagination-item': [undefined, null, ''].includes(
          paginationItemClass
        ),
        [paginationItemClass]: paginationItemClass,
      }"
      @click="totalPage <= currentPage ? null : handlePageChange(totalPage)"
    >
      <a
        :title="lastTitle"
        :class="{
          'vue3-pagination-not-allowed': totalPage <= currentPage,
          [paginationLinkClass]: paginationLinkClass,
        }"
        ><img src="./assets/last.png" :style="sizeStyle" alt=""
      /></a>
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
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Gideon+Roman&display=swap");
* {
  margin: 0;
  padding: 0;
}
.vue3-pagination-pagination-container {
  font-family: "Gideon Roman", cursive;
  display: flex;
}
.vue3-pagination-pagination-item {
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
.vue3-pagination-pagination-item a {
  color: black;
  text-decoration: none;
  display: flex;
  padding: auto;
}
.vue3-pagination-pagination-item a img {
  user-drag: none;
  -webkit-user-drag: none;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
}
.vue3-pagination-active {
  border-radius: 100%;
  background: #0f5298;
}
.vue3-pagination-active a {
  color: #fff;
  font-weight: bold;
}
.vue3-pagination-not-allowed {
  cursor: not-allowed;
}
</style>
