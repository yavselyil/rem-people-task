<template>
  <div class="table-view">
    <div class="navbar">
      <p class="header">Competitor Comparative Product Availability</p>
    </div>
    <Table :items="pageData" />
    <Pagination :totalPages="totalPageCount" @updatePage="updatePage" />
    <button class="log-out-btn" @click="logOut()">Log Out!</button>
  </div>
</template>

<script>
import Table from "../components/Table";
import Pagination from "../components/Pagination";
import jsonData from "../table.json";
export default {
  components: {
    Table,
    Pagination
  },
  data() {
    return {
      data: jsonData.data.rows,
      pageData: [],
      itemCountPerPage: 5,
      currentPage: 1
    };
  },
  beforeCreate: function() {
    document.body.className = "table";
  },
  computed: {
    totalPageCount() {
      return (
        Math.floor(this.data.length / this.itemCountPerPage) +
        (this.data.length % this.itemCountPerPage)
      );
    }
  },
  created() {
    this.data.map(x => {
      x.visitDateTime = new Date(x.visitDateTime).toLocaleDateString();
    });
    this.updatePage(this.currentPage);
  },
  methods: {
    updatePage(page) {
      this.currentPage = page;
      let startIndex = (page - 1) * this.itemCountPerPage;
      this.pageData = this.data.slice(
        startIndex,
        startIndex + this.itemCountPerPage
      );
    },
    logOut() {
      this.$router.push("/");
      this.$noty.success("Successfully logged out!");
    }
  }
};
</script>

<style>
.log-out-btn {
  position: absolute;
  top: 35px;
  font-size: 13px;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  border-radius: 6px;
  background-color: #e93890;
  border-color: #ff69b4;
  -webkit-box-shadow: 0px 0px 10px 3px rgba(255, 105, 180, 0.88);
  -moz-box-shadow: 0px 0px 10px 3px rgba(255, 105, 180, 0.88);
  box-shadow: 0px 0px 10px 3px rgba(255, 105, 180, 0.88);
}
.table-view .navbar {
  border: 2px solid rgba(60, 58, 58, 0.5);
  max-width: 100%;
  background: rgba(60, 58, 58, 0.5);
  text-align: left;
  padding-left: 50px;
}
.header {
  color: white;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  font-size: 24px;
}
</style>
