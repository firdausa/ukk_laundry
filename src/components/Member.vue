<template>
    <div>
        <main>
            <div class="container-fluid px-4">
                <h1 class="mt-4">Data Member</h1>
                <div class="card mb-4">
                    <div class="card-body">
                        <a class="btn btn-success" v-b-modal.modal_member>Tambah Member</a>
                        <table class="table">
                            <tr>
                                <td>ID MEMBER</td>
                                <td>NAMA</td>
                                <td>JK</td>
                                <td>TLP</td>
                                <td>ALAMAT</td>
                                <td>AKSI</td>
                            </tr>
                            <tr v-for="mem in member" :key="mem">
                                <td>{{ mem.id_member }}</td>
                                <td>{{ mem.nama }}</td>
                                <td>{{ mem.jenis_kelamin }}</td>
                                <td>{{ mem.tlp }}</td>
                                <td>{{ mem.alamat }}</td>
                                <td>
                                    <a href="#" class="btn btn-info">Ubah</a>
                                    <a href="#" class="btn btn-danger">Hapus</a>
                                </td>
                            </tr>
                        </table>
                    </div>
                </div>
            </div>
        </main>

        <b-modal id="modal_member" ref="modal" title="Form Member" size="md" @ok="Save">
            <form>
                <div class="form-floating mb-3 mb-md-0">
                    <input v-model="nama" placeholder="Enter your first name" v-modal="nama" id="inputNama" class="form-control" type="text"/>
                    <label for="inputNama">Nama</label>
                </div>
                <div class="form-floating mb-3 mb-md-0">
                    <input v-model="tlp" placeholder="Enter your first name" v-modal="tlp" id="inputTlp" class="form-control" type="text"/>
                    <label for="inputTlp">Telepon</label>
                </div>
                <div class="form-floating mb-3 mb-md-0">
                    <input v-model="jk" placeholder="Enter your first name" v-modal="jk" id="inputJk" class="form-control" type="text"/>
                    <label for="inputJk">Jenis Kelamin</label>
                </div>
                <div class="form-floating mb-3 mb-md-0">
                    <input v-model="alamat" placeholder="Enter your first name" v-modal="alamat" id="inputAlamat" class="form-control" type="text"/>
                    <label for="inputAlamat">Alamat</label>
                </div>
            </form>
        </b-modal>
    </div>
</template>
<script>
module.exports =  {
    data: function(){
        return {
            nama: "",
            jk:"",
            tlp:"",
            alamat:"",
            member: [],
        }
    },
    methods: {
        getData: function(){
            let config = {
                headers : {
                "Authorization" : "Bearer " + this.$cookies.get('Authorization')
                }
            }

          axios.get(base_url + '/member', config)
          .then( response => {
              console.log(response);
            if(response.data.success == true){
                this.member = response.data.data.member;
            }
          })

        },
        Save: function(){
            let config = {
                headers : {
                "Authorization" : "Bearer " + this.$cookies.get('Authorization')
                }
            }

            let form = {
                "nama": this.nama,
                "alamat": this.alamat,
                "jenis_kelamin": this.jk,
                "tlp": this.tlp,
            }

            axios.post(base_url + '/member', form, config)
            .then( response => {
                console.log(response);
                alert(response.data.message);
                // if(response.data.success == true){
                    
                // }
            })
        }
    },
    mounted() {
        this.getData();
    },
}
</script>