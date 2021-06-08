<template>
    <div align="center">
        <button @click="getSelectedRows()">Get Selected Rows</button>
        <br><br>
        <button @click="console.log(rowData)">
            show in console
        </button>
        <br><br>
         <button @click="buttonClick">X</button>
         <br><br>
         <button @click="addrow">AddRow</button>
        <ag-grid-vue style="width: 500px; height: 500px;"
            class="ag-theme-alpine"
            :columnDefs="columnDefs"
            :rowData="rowData"
            rowSelection="multiple"
            @grid-ready="onGridReady">
        </ag-grid-vue>
    </div>
</template>



<script>
import "ag-grid-community/dist/styles/ag-grid.css";
// import "ag-grid-community/dist/styles/ag-theme-alpine.css";
import { AgGridVue } from "ag-grid-vue";
export default {
  name: "ToDo",

  data () {
    return {
         columnDefs: null,
         rowData: null,
         gridApi: null,
         columnApi: null
    }
  },
   components: {
            AgGridVue
        },

   methods: {
            onGridReady(params) {
                this.gridApi = params.api;
                this.columnApi = params.columnApi;
            },
            addrow(){
                this.gridApi.applyTransaction({add:[{}]})

            },
            getSelectedRows() {
                const selectedNodes = this.gridApi.getSelectedNodes();
                const selectedData = selectedNodes.map( node => node.data );
                const selectedDataStringPresentation = selectedData.map( node => `${node.make} ${node.model}`).join(', ');
                alert(`Selected nodes: ${selectedDataStringPresentation}`);
            },
            defaultColDef: {
    suppressKeyboardEvent: params => {
        if (!params.editing) {
            let isBackspaceKey = params.event.keyCode === 8;
            let isDeleteKey = params.event.keyCode === 46;
			
            if (isBackspaceKey) {
                // Delete all selected rows...
				return true
			}
			
			if(isDeleteKey){
                // Delete all selected cell ranges...
                return true
			}
        }
        return false;
    }
 },
buttonClick (e) {

        this.setState({
            visible:true
        })
        let deletedRow = this.props.node.data;
        e.gridApi.updateRowData({ remove: [deletedRow] })  // It will update the row
    }
    
   },
            

        
   beforeMount() {
            this.columnDefs = [
                { field: 'todo_name', editable:true, sortable: true, filter: true, checkboxSelection: true},
                { field: 'todo_time' , editable:true, sortable: true, filter: true,checkboxSelection: true}
            ];

            this.rowData = [
                {todo_name:'bathing',todo_time:'7:30'},
                {todo_name:'yoga',todo_time:'8:30'},
                {todo_name:'rest',todo_time:'9:00'},
                {todo_name:'breakfast',todo_time:'9:15'},
                {todo_name:'study',todo_time:'10:00'}
                
            ];
        }
    }    
  

</script>

