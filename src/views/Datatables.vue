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
                responsive: true
            },
            columns: [
                { title: 'Repository Location', data: 'title' },
                { title: 'Repository File name', data: 'brand' },
                { title: 'Market', data: 'category' },
                { title: 'File Size', data: 'price' },
                { title: "Aging (in Years)", data: 'rating' },
                { title: 'Over-retained', data: 'discountPercentage' }
            ],
            recData: [],
            seletedOption: '',
            seletedMarket: '',
            marketList: [],
            dropdownList: [
                { text: 'Type1', value: '1' },
                { text: 'Type2', value: '2' },
                { text: 'Type3', value: '3' },
            ],
        };
    },
    mounted() {
        this.getMarketList();
        this.bindDtClasses();
    },
    methods: {
        getMarketList() { // coutry/markets list will load
            axios.get('https://dummyjson.com/products').then(({ data }) => {
                this.marketList = [
                { text: 'USA', value: 'US' },
                { text: 'UK', value: 'UK' },
                { text: 'France', value: 'FR' },
                { text: 'Germany', value: 'DE' },
                { text: 'Finland', value: 'FI' },
                { text: 'Poland', value: 'PL' },
                { text: 'India', value: 'IN' },
                ];
                console.log('ovveriding market list', data.products);
            });
        },
        getData() {
            axios.get('https://dummyjson.com/products').then(({ data }) => {
                this.recData = data.products;
                console.log(data);
                console.log(this.recData.length, 'table length');
                this.bindDtClasses();
            });
        },
        bindDtClasses() {
            if (this.recData.length == 0) {
                this.addClassToElement(".datatable", "dt_empty_table");
            } else {
                this.removeClassFromElement(".datatable", "dt_empty_table");
            }
        },
        addClassToElement(prop, className) {
            const element = document.querySelector(prop);
            element && element.classList.add(className);
        },
        removeClassFromElement(prop, className) {
            const element = document.querySelector(prop);
            element && element.classList.remove(className);
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
        <div class="badge bg-light text-secondary d-flex align-items-center repo-hint">Provide Repository location or File Path
        </div>

        <div>
            <input type="text" class="form-control form-control-sm" id="exampleFormControlInput1"
                placeholder="Enter repository">
        </div>
        <div>
            <select class="form-select form-select-sm" v-model="seletedOption" aria-label=".form-select-sm example">
                <option value="">List of share belonging to Flier</option>
                <option v-for="option in dropdownList" :key= "option.value" :value="option.value">
                    {{ option.text }}
                </option>
            </select>
        </div>
        <div>
            <select class="form-select form-select-sm" v-model="seletedMarket" aria-label=".form-select-sm example">
                <option value="">market/country</option>
                <option v-for="option in marketList" :key= "option.value" :value="option.value">
                    {{ option.text }}
                </option>
            </select>
        </div>
        <div class="filter-buttons d-flex">
            <button type="button" class="btn-space btn btn-primary btn-sm" @click="getData()">Scan</button>
            <button type="button" class="btn btn-danger btn-sm" @click="getData()">PII Scan</button>
        </div>
    </nav>
    <DataTable :columns="columns" :options="options" :data="recData" class="display table table-bordered mt-3"
        width="100%">
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
    <div class="clear-both" v-if="recData.length > 0">
        <button type="button" @click="downloadXlsx()" id="excelExport" class="btn btn-link">Download scan
            results</button>
    </div>
</template>

<style>
@import 'datatables.net-bs5';

.filter-section {
    display: flex;
    gap: 10px;
    margin-top: 1rem;
    height: 50px;
    align-items: center;
}

.dt-info {
    float: left;
    margin-top: 5px !important;
}

.dt-search,
.dt-buttons {
    display: none;
}

.dt-paging.paging_full_numbers,
.dt-search {
    float: right;
    margin-top: 5px !important;
}

.clear-both {
    clear: both;
}

.btn-space {
    margin-right: 1rem;
}
.dt_empty_table .dt-info {
    display: none;
}
.dt_empty_table .dt-paging {
    display: none;
}
@media screen and (min-width: 1200px) {
    .filter-buttons {
        margin-left: auto;
    }
}
@media only screen and (min-width: 769px) and (max-width: 1199px) {
    .repo-hint {
        max-width: 200px;
        white-space: normal;
    }
}
@media screen and (max-width: 768px) {
    .filter-section {
        gap: 5px;
        height: auto;
        align-items: flex-start;
        flex-direction: column;
    }
    .repo-hint {
        width: auto;
    }
}
</style>
