<template>
  <div>
    <a-button style="float: right;background-color: royalblue;margin-right: 92px">
      <router-link to="/created">Thêm</router-link>
    </a-button>
  </div>

  <!--  cái bảng -->
  <a-table :columns="columns" :data-source="data">
    <template #bodyCell="{ column, record}">
      <template v-if="column.dataIndex === 'operation'">
        <a-button type="primary"><router-link to="/put">Edit</router-link></a-button>
        <a-button @click="xoaTaiKhoan(record.soTaiKhoan)" type="danger" style="margin-left: 5px">Delete</a-button>
      </template>
    </template>

  </a-table>
</template>

<script lang="ts">
import {defineComponent, onMounted, ref} from 'vue';
import axios from 'axios';
import giaoDien from './fromThemMoi.vue';

const columns = [
  {
    title: 'Số tài khoản',
    dataIndex: 'soTaiKhoan',
    key: 'soTaiKhoan',
  },
  {
    title: 'Tên tài khoản',
    dataIndex: 'tenTaiKhoan',
    key: 'tenTaiKhoan',
  },
  {
    title: 'Ngày tháng năm sinh',
    dataIndex: 'ngayThangNamSinh',
    key: 'ngayThangNamSinh',
  },
  {
    title: 'Email',
    dataIndex: 'email',
    key: 'email',
  },
  {
    title: 'Số tiền trong tài khoản',
    dataIndex: 'soTienTrongTaiKhoan',
    key: 'soTienTrongTaiKhoan',
  },
  {
    title: 'thao tác',
    dataIndex: 'operation',

  }
];

export default defineComponent({
  components: {
    giaoDien,
  },
  data() {

    return {
      data: [],
      nguoidung: {
        soTaiKhoan: '',
        tenTaiKhoan: '',
        ngayThangNamSinh: '',
        email: '',
        soTienTrongTaiKhoan: ''
      },
      columns,
    };
  },

  methods: {
     getTaiKhoan() {
      axios.get('http://localhost:8088/nguoidung').then((response) => {
        this.data = response.data.data;
        console.log(this.data);
        return;
      });
    },
     xoaTaiKhoan(soTaiKhoan : number) {
      axios.delete("http://localhost:8088/nguoidung/" + soTaiKhoan).then((response) => {
        console.log(response);
        this.getTaiKhoan();
      }).catch(error => {
        console.log(error);
      });
    },

  },
  mounted() {
    this.getTaiKhoan();
  },
});
</script>

