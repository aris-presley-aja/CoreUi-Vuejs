<template>
  <CRow>
    <CCol :xs="12">
      <DocsCallout name="Table" href="components/table.html" />
    </CCol>
    <CCol :xs="12">
      <CCard class="mb-4">
       <CCardHeader color="info">
         <center>  User</center>
          <!-- <strong>Vue Table</strong> <small>Basic example</small> -->
        </CCardHeader>
        <CCardBody>
          <!-- <p class="text-medium-emphasis small">
            Using the most basic table CoreUI, here&#39;s how
            <code>&lt;CTable&gt;</code>-based tables look in CoreUI.
          </p> -->
<form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
            <CTable>
              <CTableHead>
                <CTableRow>
                  <!-- <CTableHeaderCell scope="col">#</CTableHeaderCell>
                  <CTableHeaderCell scope="col">Class</CTableHeaderCell>
                  <CTableHeaderCell scope="col">Heading</CTableHeaderCell>
                  <CTableHeaderCell scope="col">Heading</CTableHeaderCell> -->
                  
                </CTableRow>
              </CTableHead>
                           <CTable hover>
                                  <CTableHead>
                                    <CTableRow>
                                      <CTableHeaderCell scope="col">#</CTableHeaderCell>
                                      <CTableHeaderCell scope="col">Username</CTableHeaderCell>
                                      <CTableHeaderCell scope="col">Email</CTableHeaderCell>
                                      <CTableHeaderCell scope="col">Password</CTableHeaderCell>
                                            <CTableHeaderCell scope="col"></CTableHeaderCell>
                                    </CTableRow>
                                  </CTableHead>
                              <CTableBody>
                                  <CTableRow>
                                      <CTableHeaderCell scope="row">1</CTableHeaderCell>
                                      <CTableDataCell>Mark Twain</CTableDataCell>
                                      <CTableDataCell>MT@Mark.net</CTableDataCell>
                                      <CTableDataCell>Marked</CTableDataCell>
                                      <CTableDataCell>
                                                      <CButton color="primary" @click="() => { visibleStaticBackdropDemo = true }">Edit</CButton>
                                                      <CModal size="lg" backdrop="static" :visible="visibleStaticBackdropDemo" @close="() => { visibleStaticBackdropDemo = false }">
                                                      <CModalHeader>
                                                        <CModalTitle>Edit User</CModalTitle>
                                                      </CModalHeader>
                                                      <CModalBody align="center">

                                                                                              <CTableHead>
                                    <CTableRow width="80%">


                                      <CTableHeaderCell scope="col">Username</CTableHeaderCell>
                                      <CTableHeaderCell scope="col">Email</CTableHeaderCell>
                                      <CTableHeaderCell scope="col">Password</CTableHeaderCell>

                                    </CTableRow>
                                  </CTableHead>
         <CTableRow width="80%">
            <CTableDataCell><input  md="2" type="text" v-model="form.name"></CTableDataCell>
            <CTableDataCell><input  md="2" type="text" v-model="form.email"></CTableDataCell>
            <CTableDataCell><input  md="2" type="text" v-model="form.password"></CTableDataCell>
            <!-- <input type="hidden" v-model="form.created_at">
            <input type="hidden" v-model="form.id"> -->
            <!-- <th><input  md="2" type="text" v-model="form.name"></th>
            <th><input  md="2" type="text" v-model="form.email"></th> -->
            <!-- <th><input  md="2" type="text" v-model="form.password"></th> -->
              <!-- <CRow md="2">
    <CFormInput v-model="form.name"/>
  </CRow>
              <CRow md="2">
    <CFormInput v-model="form.email"/>
  </CRow>
              <CRow md="2">
    <CFormInput v-model="form.password"/>
  </CRow> -->
            <!-- <input type="text" v-model="form.password"> -->
        </CTableRow>


                                                      </CModalBody>
                                                      <CModalFooter>
                                                        <CButton color="secondary" @click="() => { visibleStaticBackdropDemo = false }">
                                                          Close
                                                        </CButton>
                                                        <CButton color="primary">Save changes</CButton>
                                                      </CModalFooter>
                                                    </CModal>
                                                    || 
                                                    <CButton color="danger">Delete</CButton>
                                                  
                                    </CTableDataCell>
                                                    
                                                      
                                </CTableRow>

                              </CTableBody>
                           </CTable>
             </CTable>

        </CCardBody>
      </CCard>
    </CCol>
    <!-- tabel kue lapis -->

  </CRow>
</template>

<script>
import axios from 'axios'
export default {
  name: 'User',
data(

    ) 

    {
      return { 
         xlDemo: false,
        lgDemo: false,
        smDemo: false,
        
        visibleStaticBackdropDemo: false,
        form: {
          // id: '',
          // avatar: '',
          // name: '',
          // token: '',
          // email: '',
          // password: ''
        },
      users: '',  
headers: [
          {
            text: 'User database',
            align: 'start',
            sortable: false,
            value: 'users',
          },
          { text: 'name', value: 'name' },
          { text: 'email', value: 'email' },
          { text: 'password', value: 'password' },
          { text: 'id', value: 'id' },
       
        ],

        updateSubmit: false
                  
      }
    
          

  },
           mounted() {
    this.load()
  },
         methods: {
    load(){
        axios.get('https://6182648584c2020017d89e32.mockapi.io/api/v1/users').then(res => {
        this.users = res.data //respon dari rest api dimasukan ke users
      }).catch ((err) => {
        console.log(err);
      })
    },

     add(){
      axios.post('https://6182648584c2020017d89e32.mockapi.io/api/v1/users', this.form).then(res => {
          this.load()
          this.form.name = ''
            
          this.form.email = ''
            
          this.form.password = ''
  
                           
      })
      
              .catch ((add) => {
        console.log(add);
        
      })
      .catch ((err) => {
        console.log(err);
        
      })

    },

      edit(user){ 
        this.updateSubmit = true
        this.form.id = user.id 
        this.form.name = user.name
                this.form.email = user.email
                        this.form.password = user.password 
    },

    update(form){ 
       return axios.put('https://6182648584c2020017d89e32.mockapi.io/api/v1/users' + form.id , {name: this.form.name}).then(res => {
        this.load()
        this.form.id = ''
        this.form.name = ''
                this.form.email = ''
                        this.form.password = ''
        
        this.updateSubmit = false
      }).catch((err) => {
        console.log(err);
        
      })
    },

    del(user){
 axios.delete('https://6182648584c2020017d89e32.mockapi.io/api/v1/users' + user.id).then(res =>{
          this.load(id)
          let index = this.users.indexOf(form.name)
          this.users.splice(index,1)

      })
    },

         },

}

  

</script>
