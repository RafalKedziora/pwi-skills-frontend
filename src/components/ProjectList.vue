<template>
    <v-list class="bg-blue-darken-4">
        <v-list-group>
        <template v-slot:activator="{ props }">
            <v-list-item v-bind="props" :title="lang" :value="lang"></v-list-item>
        </template>

        <v-list-item @click="UpdateData(language)"
            v-for="language in languages"
            :key="language.id"
            :value="language.code"
            :title="language.code"
            prepend-icon="mdi-translate"
        ></v-list-item>
        </v-list-group>
    </v-list>

    <div v-if="projects.length">
        <div v-for="project in projects" :key="project.id">
                <div v-if="project.details.length">
                    <div v-for="detail in project.details" :key="detail.id">
                        <v-card :to="{ name: 'ProjectDetail', params: { id: project.id, language: lang } }">
                            <Project :projectId="project.id" :projectName="detail.name" :projectAbout="detail.about"/>
                        </v-card>
                    </div>
                </div>
                <div v-else>
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
                  null
                </v-card-title>

                <v-card-subtitle>null</v-card-subtitle>

                <v-card-text>
                    {{project.id}}
                </v-card-text>
              </div>

              <v-avatar
                class="ma-3"
                size="135"
                rounded="0"
              >
                <v-img></v-img>
              </v-avatar>
            </div>
          </v-card>
        </v-col>
                        </v-row>
                        </v-container>
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
import Project  from '@/components/Project'
import Navbar from '@/components/Navbar'
export default {
    components: { Project, Navbar },
    setup() {
        
    },
    data() {
        return {
            projects: [],
            details: [],
            lang: 'PL',
            languages: []
        }
    },
    mounted() {
        fetch('https://localhost:7197/languages/')
        .then(res => res.json())
        .then(data => this.languages = data.languages)
        .catch(err => console.log(err.message))

        fetch('https://localhost:7197/projects/' + this.lang)
        .then(res => res.json())
        .then(data => this.projects = data.projects)
        .catch(err => console.log(err.message))
    },
    methods: {
        UpdateData(language) {
        this.lang = language.code

        fetch('https://localhost:7197/projects/' + this.lang)
        .then(res => res.json())
        .then(data => this.projects = data.projects)
        .then(data => console.log(data))
        .catch(err => console.log(err.message))
        }
    }
}
</script>