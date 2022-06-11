<template>
    <div v-if="project !== null">
        <div v-if="project.details.length">
            <div v-for="detail in project.details" :key="detail.id">
                  <v-card
    class="mx-auto mt-2"
    max-width="800"
  >
    <v-img
      src="https://picsum.photos/600/500"
      cover
    ></v-img>

    <v-card-title>
      {{detail.name}}
    </v-card-title>

    <v-card-subtitle>
      {{detail.about}}
    </v-card-subtitle>

    <v-card-actions>
      <v-spacer></v-spacer>

      <v-btn
        :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show = !show"
      ></v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
         {{detail.description}}
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
            </div>
        </div>
    </div>
    <v-container v-else class="fill-height d-flex flex-column" justify="center" align="center">
    <v-row align="center">
        <v-col justify="center">
            <v-progress-circular
            :size="100"
            color="blue-darken-4"
            indeterminate
            ></v-progress-circular>
            <div>
                Wczytywanie danych
            </div>
        </v-col>
    </v-row>
</v-container>
</template>

<script>
export default {
    props: ['id', 'language'],
    setup() {
        
    },
    data() {
        return {
            project : null,
            show: false,
        }
    },
    created(){
        fetch('https://localhost:7197/projects/' + this.language + '/' + this.id)
        .then(res => res.json())
        .then(data => this.project = data)
        .then(data => console.log(data + this.id + this.language))
        .catch(err => console.log(err.message + this.id + this.language))
    }
}
</script>