<template>

<nav>    
  <v-app-bar
      color="grey darken-3"
      dense
      dark
      tile
      app class="indigo"
      height="30"
    >

      <v-btn icon right>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    
    </v-app-bar>
   

  <v-navigation-drawer 
        permanent 
        app class="indigo" 
        width="100" 
        color="grey darken-4"
  >
  </v-navigation-drawer>

  <!--<v-card
    id="chat-box"
    class="mx-auto overflow-hidden"
    height="330"
    width="300"
    color="white"
    style="position:fixed; right:10px; bottom:20%;"
  >
      <v-divider></v-divider>
        <v-text-field
          v-model='userName'
          color="white"
          border
          solo
          label="Search"
          append-icon="mdi-magnify"
      ></v-text-field>
    <v-card
      class="mx-auto"
      max-width="300"
      color="white"
      tile
    >
        <v-list flat>
          <v-list-item-group
            v-model="selectedItem"
            color="primary"
          >
            <v-list-item
              v-for="(item, i) in items"
              :key="i"
            >
              <v-list-item-icon>
                <v-icon v-text="item.icon"></v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title v-text="item.text"></v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-card>
    </v-card>
-->

 <v-card
    max-width="350"
    max-height="330"
    class="mx-auto"
    style="position:fixed; right:10px; bottom:10%;"
  >
    <v-toolbar
      color="cyan"
      dark
    >
      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    </v-toolbar>

    <v-list three-line>
      <template v-for="(item, index) in items">
        <v-subheader
          v-if="item.header"
          :key="item.header"
          v-text="item.header"
        ></v-subheader>

        <v-divider
          v-else-if="item.divider"
          :key="index"
          :inset="item.inset"
        ></v-divider>

        <v-list-item
          v-else
          :key="item.text"
        >
          <v-list-item-avatar>
            <v-img :src="item.image"></v-img>
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title v-html="item.text"></v-list-item-title>
            <v-list-item-subtitle v-html="item.tags"></v-list-item-subtitle>
              </v-list-item-action>
          </v-list-item-content>
            <v-list-item-action>
              <v-spacer></v-spacer>
                 <v-list-item-action-text v-text="item.publishDate"></v-list-item-action-text>
              </v-list-item-action>

        </v-list-item>
      </template>
    </v-list>

  </v-card>



  <v-row style="position:fixed; right:0; bottom:0;">
    
    <v-col id="btn-task" style="display: none;">
      <v-card-text>
      <h4>Task</h4>
            <v-fab-transition>
            
              <v-btn
                color="white"
                dark
                right 
                fab
                small
              >
                <v-icon color="blue">mdi-book</v-icon>
              </v-btn>
            </v-fab-transition>
      </v-card-text>
    </v-col>
    <v-col id="btn-inbox" style="display: none;">
      <v-card-text>
      <h4>Inbox</h4>

              <v-fab-transition>
                <v-btn
                  color="white"
                  dark
                  right 
                  fab
                  small
                >
                  <v-icon color="blue">mdi-message-text</v-icon>
                </v-btn>
              </v-fab-transition>

      </v-card-text>
    </v-col>
    <v-col id="btn-main">
      <v-card-text>
              <v-fab-transition>
                <v-btn
                  color="blue"
                  dark
                  right 
                  fab
                  small
                  @click="main"
                >
                  <v-icon>mdi-lightning-bolt</v-icon>
                </v-btn>
              </v-fab-transition>
      </v-card-text>
    </v-col>
  </v-row>
      
  </nav>
</template>


<script>
import "@nuxtjs/axios";
export default {
  data() {
    
    return {
      userName: '',
      items: {}
    }
  },

  methods: {
    main() {
      const btnInbox = document.getElementById("btn-inbox");
      btnInbox.style.display = "block";
      const btnTask = document.getElementById("btn-task");
      btnTask.style.display= "block";
     
    },
  },

  async mounted(){
    
    const items = await this.$axios.get(
      "/post",
      {
        "headers": {
          "app-id": "6370ce58b5927f161bd0d981"
        },
        params: {
          per_page: 5
        }
      }
    )
    debugger;
    this.items = items.data.data;
   
  }
}
</script>