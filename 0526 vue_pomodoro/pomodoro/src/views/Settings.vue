<template>
  <div id="setting" class="container">
    <b-table :items='items' :fields="fields" >
      <template  v-slot:cell(preview)="data" >
        <audio controls :src="'./alarms/'+ data.item.file"></audio>
      </template>
      <template v-slot:cell(select)="data">
        <font-awesome-icon @click="change(data.index)" v-if="data.item.file == alarm" :icon="['fas','check']"></font-awesome-icon>
        <font-awesome-icon @click="change(data.index)" v-else :icon="['fas','times']"></font-awesome-icon>
      </template>
    </b-table>
  </div>
</template>
<script>
export default {
  data () {
    return {
      items: [
        {
          name: '鬧鈴',
          file: 'alarm1.mp3'
        },
        {
          name: '阿罵',
          file: 'ama.mp3'
        },
        {
          name: '感覺',
          file: 'nofeel.mp3'
        }
      ],
      fields: [
        {
          key: 'name',
          label: '名稱'
        },
        {
          key: 'preview',
          label: '預覽'
        },
        {
          key: 'select',
          label: '選擇'
        }
      ]
    }
  },
  computed: {
    alarm () {
      return this.$store.getters.alarm
    },
    methods: {
      selectAlarm (item) {
        this.$store.commit('selectAlarm', item.file)
      }

    }
  },
  methods: {
    change (index) {
      const song = this.items[index].file
      this.$store.commit('change', song)
    }
  }
}
</script>
