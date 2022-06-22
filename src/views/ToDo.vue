<template>
  <div class="home">
     <v-text-field
     class="pa-2"
            outlined
            label="Add Task"
            append-icon="mdi-plus"
            hide-details
            clearable
            v-model="newTask"
            @keyup.enter="addTask(newTask)"
            @click:append="addTask(newTask)"
          ></v-text-field>
    <v-list flat class="pt-0">
      <div v-for="litem in list" :key="litem.id">
        <v-list-item
          @click="taskDone(litem)"
          :class="{ 'blue lighten-3': litem.done }"
        >
          <template>
            <v-list-item-action>
              <v-checkbox
                :input-value="litem.done"
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through':litem.done}">{{ litem.item }}</v-list-item-title>
            </v-list-item-content>
          </template>
            <v-list-item-action @click.stop="deleteTask(litem)">
            <v-btn icon>
              <v-icon color="red lighten-1">mdi-delete</v-icon>
            </v-btn>
          </v-list-item-action>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  name: "ToDo",
  data() {
    return {
      newTask:"",
      list: [
        {
          id: 1,
          item: "Wake Up",
          done: false,
        },
        {
          id: 2,
          item: "Do Push ups",
          done: false,
        },
        {
          id: 3,
          item: "Start the day",
          done: false,
        },
      ],
    };
  },
  methods: {
    taskDone(item) {
      console.log(item);
      item.done = !item.done;
    },
    deleteTask(item){
      this.list=this.list.filter(el=>el.id!==item.id);
    },
    addTask(newt){
      if(newt){
        let list=this.list
        console.log(list[list.length-1]);
        this.list.push({id:list[list.length-1].id+1,item:newt,done:false});
      }
      this.newTask=""
    }
  },
};
</script>
