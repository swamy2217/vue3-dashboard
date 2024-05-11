<script>
import axios from 'axios';
import DataTable from 'datatables.net-vue3';
import DataTablesCore from 'datatables.net-bs5';
import 'datatables.net-buttons';
import 'datatables.net-buttons/js/buttons.html5';
import jszip from 'jszip';

DataTable.use(DataTablesCore);
DataTablesCore.Buttons.jszip(jszip);

export default {
    components: {
        DataTable
    },
    data() {
        return {
            drawer: null,
            options: {
                dom: 'Bftip',
                select: true,
            },
            columns: [
                { title: 'Repository Location', data: 'title'},
                { title: 'Repository File name', data: 'brand'},
                { title: 'Market', data: 'category'},
                { title: 'File Size', data: 'price'},
                { title: "Aging (in Years)", data: 'rating'},
                { title: 'Over-retained', data: 'discountPercentage'}                
            ],
            recData:[]
        };
    },
    methods: {
        getData() {      
            axios.get('https://dummyjson.com/products').then(({data}) => {
                this.recData = data.products;
                console.log (data)
            });
        },
        downloadXlsx() {
            const element = document.getElementsByClassName('buttons-excel')[0];
            element.click();
        }
    }
 };

</script>

<template>
    <nav class="filter-section">
        <div class="badge bg-light text-secondary d-flex align-items-center">Provide Repository location or File Path</div>
        
        <div>
            <input type="text" class="form-control form-control-sm" id="exampleFormControlInput1" placeholder="Enter repository">
        </div>
        <div>
            <select class="form-select form-select-sm" aria-label=".form-select-sm example">
                <option selected>List of share belonging to Flier</option>
                <option value="1">One</option>
                <option value="2">Two</option>
                <option value="3">Three</option>
            </select>
        </div>
        <div>
            <div class="input-group input-group-sm">
                <input type="text" class="form-control" placeholder="market/country" aria-label="Text input with dropdown button" />
                <button class="btn btn-outline-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false"></button>
                <ul class="dropdown-menu dropdown-menu-end">
                    <li><a class="dropdown-item" href="#">Action</a></li>
                    <li><a class="dropdown-item" href="#">Another action</a></li>
                    <li><a class="dropdown-item" href="#">Something else here</a></li>
                    <li><hr class="dropdown-divider"></li>
                    <li><a class="dropdown-item" href="#">Separated link</a></li>
                </ul>   
            </div>
        </div>
        <div>
            <button type="button" class="btn-space btn btn-primary btn-sm" @click="getData()">Scan</button>
            <button type="button" class="btn btn-danger btn-sm" @click="getData()">PII Scan</button>
        </div>
    </nav>
    <div v-if="recData">
        <DataTable
      :columns="columns"
      :options="options"
      :data="recData"
      class="display table table-bordered mt-3"
      width="100%"
    >
      <thead>
        <tr>
          <th>Repository Location</th>
          <th>Repository File name</th>
          <th>Market</th>
          <th>File Size</th>
          <!-- <th>Aging (in Years)</th> -->
          <!-- <th>Over-retained</th> -->
        </tr>
      </thead>
    </DataTable>
    </div>
    <div class="clear-both">
        <button type="button" @click="downloadXlsx()" id="excelExport" class="btn btn-link">Download scan results</button>
    </div>
</template>

<style>
@import 'datatables.net-bs5';
.filter-section {
    display: flex;
    gap: 10px;
    margin-top: 1rem;
}
.dt-info {
    float: left;
    margin-top: 5px !important;
}
.dt-search, .dt-buttons{
    display: none;
}
.dt-paging.paging_full_numbers, .dt-search {
    float: right;
    margin-top: 5px !important;
}
.clear-both {
    clear: both;
}
.btn-space {
    margin-left: 3rem;
    margin-right: 1rem;
}
</style>
