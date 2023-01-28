<template>
    <div class="font-bold text-4xl py-3">DATA NARAPIDANA</div>
    <div>
        <button class="px-4 py-2 border rounded bg-orange-500 text-white hover:bg-orange-400" @click="modelAdd = true">
            <i class="pi pi-user-plus px-1"></i>
            <span class="px-2">Add</span>
        </button>
    </div>
    <br>
    <div class="card">
            <DataTable :value="products2" editMode="row" dataKey="id" v-model:editingRows="editingRows" @row-edit-save="onRowEditSave" responsiveLayout="scroll">
                <Column field="id" header="No" style="width:20%">
                    <template #editor="{ data, field }">
                        <InputText v-model="data[field]" autofocus />
                    </template>
                </Column>
                <Column field="nama" header="Nama" style="width:20%">
                    <template #editor="{ data, field }">
                        <InputText v-model="data[field]" />
                    </template>
                </Column>
                <Column field="kasus" header="Kasus" style="width:20%">
                    <template #editor="{ data, field }">
                        <InputText v-model="data[field]" />
                    </template>
                </Column>
                <Column field="jenis_kelamin" header="Jenis Kelamin" style="width:20%">
                    <template #editor="{ data, field }">
                        <InputText v-model="data[field]" />
                    </template>
                </Column>
                <Column field="foto" header="Foto" style="width:20%">
                    <template #editor="{ data, field }">
                        <InputText v-model="data[field]" />
                    </template>
                </Column>
                <Column>
                    <button class="px-4 py-2 border rounded bg-orange-500 text-white hover:bg-orange-400" @click="edit(data.id)"><span class="pi pi-wrench"></span></button>
                    <button class="px-4 py-2 border rounded bg-red-500 text-white hover:bg-red-400" @click="destory(data.id)"><span class="pi pi-trash"></span></button>
                </Column>
            </DataTable>
        </div>

        <!-- Pop up modal add new -->
        <div class="flex w-full h-full justify-center item-center" v-show="modelAdd">
        <!-- Background -->
        <div class="w-screen h-full bg-gray-900 bg-opacity-80 top-0 fixed sticky-0 left-0" @click="(modelAdd = false)">
        </div>
        <!-- Form -->
        <div class="   flex justify-center items-center top-[30%] fixed sticky-0 left-[40%]">
          <div class=" md:w-auto  relative flex flex-col justify-center items-center bg-white  p-8">
            <div class="my-5">
              <h1 role="main" class="text-xl font-semibold text-center text-gray-800">Tambah Narapidana</h1>
            </div>
            <div class="mt-2 flex flex-col space-y-2">
                <InputText id="nama" type="text" v-model="data.nama" placeholder="Nama"/>
                <InputText id="kasus" type="text" v-model="data.kasus" placeholder="Kasus"/>
                <select id="jenis_kelamin" class="bg-white border border-gray-300 text-gray-900 text-l rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-4 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500">
                    <option selected>Pilih Jenis Kelamin</option>
                    <option value="L">Laki-Laki</option>
                    <option value="P">Perempuan</option>
                </select>
                <InputText id="foto" type="text" v-model="data.foto" placeholder="Salin Link Foto"/>
            </div>
            <button class="mt-2 px-4 py-2 border rounded bg-orange-500 text-white hover:bg-gray-400" @click="addnew"><span class="pi pi-save"></span></button>
          </div>
        </div>
      </div>
</template>

<script>
import { mapGetters } from 'vuex';
  export default {
    data() {
      return {
        modelAdd: false,
        modelUpdate: false,
        data: {
          id: "",
          nama: "",
          kasus: "",
          jenis_kelamin: "",
          foto: ""
        }
      }
    },
    computed: {
      ...mapGetters({
        posts: 'post/posts'
      })
    },
    methods: {
      addnew() {
        this.$store.dispatch('post/ADD_NEW', this.data).then(respone => {
          if (respone) {
            this.modelAdd = false;
            // reset data 
            this.data = {
                id: "",
                nama: "",
                kasus: "",
                jenis_kelamin: "",
                foto: ""
            }
          }
        })
      }
    }
}
</script>

<style>

</style>