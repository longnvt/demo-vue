<template>
  <div>
    <a-button style="float: right;background-color: royalblue;margin-right: 200px"><router-link to="/created">Thêm</router-link></a-button>
  </div>

<!--  cái bảng -->
  <a-table :columns="columns" :data-source="data">
    <template #bodyCell="{ column, text }">
      <template v-if="column.dataIndex === 'name'">
        <a>{{ text }}</a>
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
    async getTaiKhoan() {
      await axios.get('http://localhost:8088/nguoidung').then((response) => {
        // console.log(response.data.data);
        this.data = response.data.data;
        console.log(this.data);
        return;
      });
    },
  },
  mounted() {
    this.getTaiKhoan();
  },
});
</script>

