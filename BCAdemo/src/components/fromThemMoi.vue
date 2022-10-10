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
    <a-form-item :name="['nguoidung', 'tenTaiKhoan']" label="Tên Người Dùng" :rules="[{ type: 'email' }]">
      <a-input v-model:value="formState.nguoidung.tenTaiKhoan" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'ngayThangNamSinh']" label="Ngày Tháng Năm Sinh" :rules="[{ type : 'ngayThangNamSinh' }]">
      <a-input v-model:value="formState.nguoidung.tenTaiKhoan" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'email']" label="email">
      <a-input v-model:value="formState.nguoidung.email" />
    </a-form-item>
    <a-form-item :name="['nguoidung', 'soTienTrongTaiKhoan']" label="Số tiền trong tài khoản">
      <a-input v-model:value="formState.nguoidung.soTienTrongTaiKhoan" />
    </a-form-item>
    <a-form-item :wrapper-col="{ ...layout.wrapperCol, offset: 8 }">
      <a-button type="primary" html-type="submit">Thêm</a-button>
    </a-form-item>
  </a-form>
</template>
<script lang="ts">
import { defineComponent, reactive } from 'vue';

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
    const onFinish = (values: any) => {
      console.log('Success:', values);
    };
    return {
      formState,
      onFinish,
      layout,
      validateMessages,
    };
  },
});
</script>
