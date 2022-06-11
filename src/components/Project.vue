<template>
  <v-card
          class="mx-auto">
      <v-container>
      <v-row dense>
        <v-col cols="12">
          <v-card
            color="#1F7087"
            theme="dark"
          >
            <div class="d-flex flex-no-wrap justify-space-between">
              <div>
                <v-card-title class="text-h5">
                  {{projectName}}
                </v-card-title>

                <v-card-subtitle>{{projectAbout}}</v-card-subtitle>

                <v-card-text>
                    {{projectId}}
                </v-card-text>
              </div>

              <v-avatar
                class="ma-3"
                size="135"
                rounded="0"
              >
                <v-img src="https://picsum.photos/125/125"></v-img>
              </v-avatar>
            </div>
          </v-card>
        </v-col>
      </v-row>
      </v-container>
  </v-card>
</template>

<script>
export default {
    props: ['projectId', 'projectName', 'projectAbout'],
    setup() {
        
    },
    data() {
        return {
            projectDetail : null,
            language: 'PL'
        }
    },
    mounted() {
        fetch('https://localhost:7197/projects/' + this.language + '/' + this.id)
        .then(res => res.json())
        .then(data => this.projectDetail = data)
        .catch(err => console.log(err.message))
    }
}
</script>