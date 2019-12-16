<template>
  <div class="pagination" :style="{ width: paginationWidth }">
    <div v-for="(page, index) in totalCount" :key="page">
      <p
        :class="['page-item', { active: currentPage == index + 1 }]"
        :style="{ width: paginationItemWidth }"
        @click="onPageClicked(index + 1)"
      >
        {{ index + 1 }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["totalPages"],
  data() {
    return {
      pageItemWidth: 30,
      totalCount: new Array(Number(this.totalPages)),
      currentPage: 1
    };
  },
  computed: {
    paginationItemWidth: function() {
      return this.pageItemWidth + "px";
    },
    paginationWidth: function() {
      return this.totalPages * this.pageItemWidth + "px";
    }
  },
  methods: {
    onPageClicked(page) {
      this.currentPage = page;
      this.$emit("updatePage", page);
    }
  }
};
</script>

<style scoped>
.pagination {
  display: block;
  margin: 0 auto;
  color: white;
  font-weight: bold;
}

.page-item {
  float: left;
  cursor: pointer;
}

.page-item:hover {
  color: #fff;
  font-weight: bold;
  text-shadow: rgba(255, 255, 255, 0.5) 0px 3px 3px;
}

.page-item.active {
  color: #fff;
  text-shadow: rgba(255, 255, 255, 0.5) 0px 3px 3px;
  font-weight: bold;
  text-decoration: underline;
}
</style>
