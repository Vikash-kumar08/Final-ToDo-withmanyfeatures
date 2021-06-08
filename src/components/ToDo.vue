<template>
  <div align="center">
    <button @click="getSelectedRows">Get Selected Rows</button>
    <br /><br />
    <br /><br />
    <button @click="deleteSelectedRows">Delete selected Rows</button>
    <br /><br />
    <button @click="addRow">AddRow</button>
    <ag-grid-vue
      style="width: 500px; height: 500px"
      class="ag-theme-balham"
      :columnDefs="columnDefs"
      :rowData="rowData"
      rowSelection="multiple"
      @grid-ready="onGridReady"
      :floatingFilters="true"
    >
    </ag-grid-vue>
  </div>
</template>
<script>
import "ag-grid-community/dist/styles/ag-grid.css";
import "ag-grid-community/dist/styles/ag-theme-balham.css";
import { AgGridVue } from "ag-grid-vue";
export default {
  name: "ToDo",
  data() {
    return {
      columnDefs: null,
      rowData: null,
      gridApi: null,
      columnApi: null,
    };
  },
  components: {
    AgGridVue,
  },
  methods: {
    onGridReady(params) {
      this.gridApi = params.api;
      this.columnApi = params.columnApi;
    },
    addRow() {
      this.gridApi.applyTransaction({ add: [{}] });
    },
    getSelectedRows() {
      const selectedNodes = this.gridApi.getSelectedNodes();
      const selectedData = selectedNodes.map((node) => node.data);
      alert(JSON.stringify(selectedData));
      console.log({ data: JSON.parse(JSON.stringify(selectedData)) });
    },
    deleteSelectedRows() {
      const selectedNodes = this.gridApi.getSelectedNodes();
      const selectedData = selectedNodes.map((node) => node.data);
      this.gridApi.applyTransaction({ remove: selectedData });
    },
  },
  beforeMount() {
    this.columnDefs = [
      {
        field: "todo_name",
        editable: true,
        sortable: true,
        filter: true,
        checkboxSelection: true,
        floatingFilter: true,
      },
      {
        field: "todo_time",
        editable: true,
        sortable: true,
        filter: true,
        floatingFilter: true,
      },
    ];
    this.rowData = [
      { todo_name: "bathing", todo_time: "7:30" },
      { todo_name: "yoga", todo_time: "8:30" },
      { todo_name: "rest", todo_time: "9:00" },
      { todo_name: "breakfast", todo_time: "9:15" },
      { todo_name: "study", todo_time: "10:00" },
    ];
  },
};
</script>