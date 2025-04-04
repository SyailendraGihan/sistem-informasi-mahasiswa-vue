<template>
  <div class="hello">
    <h2>{{ msg }}</h2>
    <p>
      <button @click="tampilkanMhs">Tampilkan Data Mahasiswa</button>
    </p>
    <div v-if="tampil">
      <table class="center">
        <caption>Daftar Mahasiswa Universitas Terbuka</caption>
        <thead>
          <tr>
            <th>NIM</th>
            <th>Nama</th>
            <th>Tanggal Lahir</th>
            <th>E-mail</th>
            <th>Program Studi</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="dataMhs in dataMhsList" :key="dataMhs.id">
            <td>{{ dataMhs.nim }}</td>
            <td>{{ dataMhs.nama }}</td>
            <td>{{ dataMhs.tglLahir }}</td>
            <td>{{ dataMhs.email }}</td>
            <td>{{ dataMhs.prodi }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HalamanAwal',
  data() {
    return {
      tampil: false,
      dataMhsList: []
    };
  },
  props: {
    msg: String
  },
  methods: {
    tampilkanMhs() {
      axios.get('http://localhost:4000/mhs') // ← diperbaiki
        .then(response => {
          this.dataMhsList = response.data;
          this.tampil = true;
        })
        .catch(error => {
          console.error("Gagal ambil data:", error.message);
        });
    }
  }
};
</script>

<style scoped>
.center {
  margin-left: auto;
  margin-right: auto;
}
</style>
