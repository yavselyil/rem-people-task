<template>
  <div class="section1" style="text-align: center">
    <div class="responsive-table">
      <table class="rem-table">
        <thead class="colored-thead">
          <tr class="header-row">
            <th>SalesPoint Number</th>
            <th>City</th>
            <th>SalesPoint Name</th>
            <th>ResearchGroupName</th>
            <th>Product</th>
            <th>Availability</th>
          </tr>
        </thead>
        <tbody>
          <tr class="element-row" v-for="item in items" :key="item.auditId">
            <td style="min-width: 144px">{{ item.auditId }}</td>
            <td>{{ item.city }}</td>
            <td>{{ item.salesPointName }}</td>
            <td>{{ item.researchGroupName }}</td>
            <td>{{ item.visitDateTime }}</td>
            <td>{{ item.availability ? "Yes" : "No" }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: ["items"]
};
</script>

<style>
.section1 {
  display: flex;
  justify-content: center;
}

.responsive-table {
  width: 960px;
  border-radius: 10px;
  overflow: scroll;
}
@media only screen and (max-width: 760px),
  (min-device-width: 768px) and (max-device-width: 1024px) {
  table,
  thead,
  tbody,
  th,
  td,
  tr {
    display: block;
  }

  thead tr {
    position: absolute;
    top: -9999px;
    left: -9999px;
  }

  tr {
    margin: 0 0 1rem 0;
  }

  tr:nth-child(odd) {
    background: #ccc;
  }

  td {
    border: none;
    border-bottom: 1px solid #eee;
    position: relative;
    padding-left: 50%;
  }

  td:before {
    position: absolute;
    top: 0;
    left: 6px;
    width: 45%;
    padding-right: 10px;
    white-space: nowrap;
  }
}

.rem-table {
  max-width: 1000px;
  text-align: center;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

.colored-thead {
  color: #ffffff;
  background: rgba(232, 211, 186, 0.5);
}

td,
th {
  text-align: left;
  padding: 8px;
}
.element-row {
  background: white;
}

.element-row:hover {
  background-color: #f5f5f5;
}
</style>
