<template>
    <section>
        <b-field grouped group-multiline>
            <b-select v-model="perPage" :disabled="!isPaginated">
                <option value="5">5 per page</option>
                <option value="10">10 per page</option>
                <option value="15">15 per page</option>
                <option value="20">20 per page</option>
            </b-select>
            <div class="control is-flex">
                <b-switch v-model="isPaginated">Paginated</b-switch>
            </div>
            <div class="control is-flex">
                <b-switch v-model="isPaginationSimple" :disabled="!isPaginated">Simple pagination</b-switch>
            </div>
        </b-field>

        <b-table
            :data="data[1]"
            :paginated="isPaginated"
            :per-page="perPage"
            :current-page.sync="currentPage"
            :pagination-simple="isPaginationSimple"
            :pagination-position="paginationPosition"
            :default-sort-direction="defaultSortDirection"
            :sort-icon="sortIcon"
            :sort-icon-size="sortIconSize"
            aria-next-label="Next page"
            aria-previous-label="Previous page"
            aria-page-label="Page"
            aria-current-label="Current page">

           <template slot-scope="props">
                <b-table-column field="id" label="ID" width="40" sortable numeric>
                    {{ props.row.id }}
                </b-table-column>

                <b-table-column field="employee_name" label="Name" sortable>
                    {{ props.row.employee_name }}
                </b-table-column>

                <b-table-column field="employee_salary" label="Salary" sortable>
                    {{ props.row.employee_salary }}
                </b-table-column>
                <b-table-column field="employee_age" label="Age" sortable>
                    {{ props.row.employee_age }}
                </b-table-column>
                <!-- <b-table-column field="c_mobileno" label="Contact No" sortable>
                    {{ props.row.c_mobileno }}
                </b-table-column> -->
                <b-table-column  label="Actions">
                    <router-link
                                :to="'/edit/' + props.row.id"
                                style="cursor: pointer"><b-button type="is-success">Edit</b-button></router-link>
                    <router-link
                    :to="'/u/delete/' + props.row.id"
                    style="cursor: pointer"><b-button type="is-danger">Delete</b-button></router-link>
                    &nbsp;&nbsp;&nbsp;
                </b-table-column>   
            </template>
        </b-table>
    </section>
</template>

<script>
    export default {
        data() {
            return {
                data:[],
                //   columns: [
                //     {
                //         field: 'c_id',
                //         label: 'ID',
                //         numeric: true
                //     },
                //     {
                //         field: 'customer_name',
                //         label: 'Name',
                //     },
                //     {
                //         field: 'c_address',
                //         label: 'Address',
                //     },
                //     {
                //         field: 'c_email',
                //         label: 'Email',
                //         centered: true
                //     },
                //     {
                //         field: 'c_mobileno',
                //         label: 'Contact',
                //         centered: true
                //     },
                // ],
                isPaginated: true,
                isPaginationSimple: false,
                paginationPosition: 'bottom',
                defaultSortDirection: 'asc',
                sortIcon: 'arrow-up',
                sortIconSize: 'is-small',
                currentPage: 1,
                perPage: 5
            }
        },
        created(){
            this.showAll()
        },
        methods:{
            showAll() {
                this.$http.get('http://dummy.restapiexample.com/api/v1/employees')
                    .then(res => {
                        
                        return res.json()
                    })
                    .then(data => {
                        const usersArray = [];
                        // console.log(data.customers)
                        for(let key in data){
                            usersArray.push(data[key])
                        }
                        this.data = usersArray
                        // console.log(this.users)
                    })
                },
            }
    }
</script>


