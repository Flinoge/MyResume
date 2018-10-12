<template>
  <q-layout view="hHh Lpr lFf">
    <q-layout-header>
      <q-toolbar inverted>
        <q-toolbar-title class="text-black">
          <q-btn
            class="lt-lg"
            flat round dense
            @click="leftSide = !leftSide"
            icon="menu"
          />
          <span class="gt-md">Freelance/Full Time Programmer</span>
        </q-toolbar-title>
        <q-tabs align="right" inverted>
          <q-route-tab
            icon="developer_mode"
            label="Code Examples"
            class="gt-md"
            to="/"
            exact
            slot="title"
          />
          <q-route-tab
            icon="assignment"
            label="Resume"
            class="gt-md"
            to="/resume"
            exact
            slot="title"
          />
          <q-route-tab
            icon="build"
            label="My Projects"
            class="gt-md"
            to="/projects"
            exact
            slot="title"
          />
          <q-route-tab
            icon="developer_mode"
            class="lt-lg"
            to="/"
            exact
            slot="title"
          />
          <q-route-tab
            icon="assignment"
            class="lt-lg"
            to="/resume"
            exact
            slot="title"
          />
          <q-route-tab
            icon="build"
            class="lt-lg"
            to="/projects"
            exact
            slot="title"
          />
        </q-tabs>
      </q-toolbar>
    </q-layout-header>
    <q-layout-drawer side="left" v-model="leftSide">
      <q-card flat>
        <q-card-media>
          <img src="../statics/MyProfile.jpg">
        </q-card-media>
        <q-card-title>
          Trevor Orgill
        </q-card-title>
        <q-card-main>
          <q-list no-border>
            <q-item>
              Full Stack Developer
            </q-item>
            <q-item>
              Graphics Designer
            </q-item>
          </q-list>
        </q-card-main>
      </q-card>
    </q-layout-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
    <q-page-sticky position="bottom-right" :offset="[18, 18]">
      <q-btn
        round
        class="text-white"
        style="background-color: #3B5998;"
        icon="fab fa-facebook-f"
        @click="openURL('https://www.facebook.com/CodersU/')"
      ><q-tooltip>Facebook</q-tooltip></q-btn>
      <q-btn
        round
        class="text-white"
        style="background-color: #0077B5; margin: 1em;"
        icon="fab fa-linkedin-in"
        @click="openURL('https://www.linkedin.com/in/trevor-orgill-3b476a146/')"
      ><q-tooltip>LinkedIn</q-tooltip></q-btn>
      <q-btn
        round
        class="text-white"
        style="background-color: #212529; margin-right: 1em;"
        icon="fab fa-github"
        @click="openURL('https://github.com/Flinoge')"
      ><q-tooltip>Github</q-tooltip></q-btn>
    </q-page-sticky>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'

export default {
  name: 'MyLayout',
  data () {
    return {
      leftSide: true,
      leftDrawerOpen: this.$q.platform.is.desktop
    }
  },
  methods: {
    openURL
  }
}
</script>

<style>
</style>
