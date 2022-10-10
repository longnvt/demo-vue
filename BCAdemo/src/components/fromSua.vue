<template>
  <a-form
      :model="formState"
      v-bind="layout"
      name="nest-messages"
      :validate-messages="validateMessages"
      @finish="onFinish"
  >
    <a-form-item :name="['nguoidung', 'soTaiKhoan']" label="Số Tài Khoản" :rules="[{ required: true }]">
      <a-input v-model:value="formState.nguoidung.soTaiKhoan" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'tenTaiKhoan']" label="Tên Người Dùng" :rules="[{  }]">
      <a-input v-model:value="formState.nguoidung.tenTaiKhoan" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'ngayThangNamSinh']" label="Ngày Tháng Năm Sinh" :rules="[{ }]">
      <a-input v-model:value="formState.nguoidung.ngayThangNamSinh" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'email']" label="email">
      <a-input v-model:value="formState.nguoidung.email" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'soTienTrongTaiKhoan']" label="Số tiền trong tài khoản">
      <a-input v-model:value="formState.nguoidung.soTienTrongTaiKhoan" />
    </a-form-item>
    <a-form-item :wrapper-col="{ ...layout.wrapperCol, offset: 8 }">
      <a-button type="primary" html-type="submit">Sửa</a-button>
    </a-form-item>
  </a-form>
</template>
<script lang="ts">
import { defineComponent, reactive } from 'vue';
import axios from "axios";

export default defineComponent({
  setup() {
    const layout = {
      labelCol: { span: 8 },
      wrapperCol: { span: 16 },
    };

    const validateMessages = {
      // required: '${label} is required!',
      // types: {
      //   email: '${label} is not a valid email!',
      //   number: '${label} is not a valid number!',
      // },
      // number: {
      //   range: '${label} must be between ${min} and ${max}',
      // },
    };

    const formState = reactive({
      nguoidung: {
        soTaiKhoan: '',
        tenTaiKhoan: '',
        ngayThangNamSinh: '',
        email: '',
        soTienTrongTaiKhoan: '',
      },
    });
    const onFinish = () => {
      axios.put('http://localhost:8088/nguoidung', formState.nguoidung)
          .then(response => {
            console.log("res:",response);
          })
          .catch(error => {
            console.log(error);
          });
    };
    return {
      formState,
      onFinish,
      layout,
      validateMessages,
    }
  },
});
</script>