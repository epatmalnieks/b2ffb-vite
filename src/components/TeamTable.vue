<template>
    <v-data-table 
      class="team-table"
      density="compact"
      :headers="headers" 
      :items-per-page="-1"
      :items="team.players" 
      >
      <template v-slot:item.position="{ item }">
        <span class="team-table-position">{{item.position}}</span>
      </template>
      <template v-slot:item.name="{ item }">
        <v-text-field 
          v-if="item.position === editedItem.position"
          class="team-table-name"
          clearable
          v-on:keyup.enter="save" 
          v-model="editedItem.name" 
          :hide-details="true"
          density="compact"
          single-line >
        </v-text-field>
        <span v-else>{{item.name}}</span>
      </template>
      <template v-slot:item.salary="{ item }">
        <v-text-field 
          type="number" 
          class="team-table-salary"
          min="0" 
          v-on:keyup.enter="save" 
          v-model="editedItem.salary" 
          :hide-details="true"
          density="compact" 
          single-line 
          v-if="item.position === editedItem.position">
        </v-text-field>
        <span v-else>{{item.salary}}</span>
      </template>
      <template v-slot:item.actions="{ item }">
        <div v-if="item.position === editedItem.position">
          <v-icon color="red" class="mr-3" @click="close">
            mdi-window-close
          </v-icon>
          <v-icon color="green" @click="save">
            mdi-content-save
          </v-icon>
        </div>
        <div v-else>
          <v-icon color="green" class="mr-3" @click="editItem(item)">
            mdi-pencil
          </v-icon>
        </div>
      </template>
      <template #bottom></template>
    </v-data-table>
</template>

<script>
export default {
  data: () => ({
    defaultItem: {
      id: 0,
      name: 'New Item',
      position: 0,
      salary: 0,
    },
    editedIndex: -1,
    editedItem: {
      name: '',
      position: 0,
      salary: 0,
    },
    headers: [
      {
        title: 'Position',
        value: 'position',
      },
      {
        title: 'Name',
        value: 'name',
      },
      {
        title: 'Salary',
        value: 'salary',
      },
      {
        title: 'Actions',
        value: 'actions',
        width: '100px',
      },
    ],
  }),
  methods: {
    close() {
      this.editedItem = { ...this.defaultItem };
      this.editedIndex = -1;
    },
    editItem(item) {
      this.editedIndex = this.team.players.indexOf(item);
      this.editedItem = { ...item };
    },
    save() {
      if (this.editedIndex > -1) {
        if (this.editedItem.salary === '') {
          this.editedItem.salary = 0;
        }
        Object.assign(this.team.players[this.editedIndex], this.editedItem);
      }
      window.localStorage.setItem(this.team.name, JSON.stringify(this.team.players));
      this.close();
    },
  },
  name: 'TeamTable',
  props: {
    team: {
      required: true,
      type: Object,
    },
  },
};
</script>

<style scoped>
.team-table {
  height: 100vh;
  width: 500px;
}

.team-table-position {
  min-width: 50px;
}

.team-table-name {
  min-width: 150px;
}
.team-table-salary {
  width: 90px;
}
</style>