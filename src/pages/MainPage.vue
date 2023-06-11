<template>
  <div>
    <q-layout view="hHr LpR lFf" style="min-height: calc(100vh - 50px)" container>
      hello
      <q-btn color="primary" icon="check" label="OK" @click="onClick" />

      <q-dialog v-model="open_modal" persistent>
        <q-card>
          <q-card-section class="row items-center">
            <q-avatar icon="signal_wifi_off" color="primary" text-color="white" />
            <span class="q-ml-sm">You are currently not connected to any network.</span>
          </q-card-section>
          <q-card-section>
            <q-table title="UsersList" :rows="data" :columns="columns" row-key="id" />
          </q-card-section>
          <q-card-actions align="right">
            <q-btn flat label="Cancel" color="primary" v-close-popup />
            <q-btn flat label="Turn on Wifi" color="primary" v-close-popup />
          </q-card-actions>
        </q-card>
      </q-dialog>
    </q-layout>
  </div>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
import { QTable } from 'quasar';
import { api } from 'src/boot/axios';
/**===== Variables =========== */
const open_modal = ref<boolean>(false);
const columns: QTable['columns'] = [
  { name: 'id', label: '#', field: 'id' },
  { name: 'username', label: 'Username', field: 'username' },
  { name: 'name', label: 'Name', field: 'name' },
  { name: 'email', label: 'Email', field: 'email' },
];
const data: any = ref([])
/**===== Methods =========== */
const onClick = async () => {
  try {
    const resp = await api.get('/users')
    console.log(resp.data);
    data.value = resp.data
  } catch (e) {
    console.log('e:', e);

  }
  open_modal.value = true;
};
</script>
<style></style>
