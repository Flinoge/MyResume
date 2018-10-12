<template>
  <div>
    <q-card flat>
      <q-card-title>There are more Projects on Github</q-card-title>
      <q-card-separator/>
      <q-tree
        :nodes="projects"
        node-key="label"
        default-expand-all
      >
        <div slot="header-generic" slot-scope="prop" class="row items-center">
          <q-icon :name="prop.node.icon" color="orange" size="28px" class="q-mr-sm" />
          <div class="text-weight-bold text-primary">{{ prop.node.label }}</div>
        </div>
        <div slot="body-generic" slot-scope="prop">
          <div v-if="prop.node.address">
            <q-btn flat class="text-weight-thin cursor-pointer" @click="openURL(prop.node.address)">Visit It Here</q-btn>
          </div>
          <div v-if="prop.node.description">
            <span class="text-weight-thin">{{ prop.node.description }}</span>
          </div>
          <span v-else class="text-weight-thin">No Description.</span>
        </div>
      </q-tree>
    </q-card>
  </div>
</template>

<script>
import { openURL } from 'quasar'

export default {
  name: 'projects',
  data () {
    return {
      projects: [
        {
          label: 'Work Projects',
          header: 'generic',
          icon: 'work',
          children: [
            {
              label: 'Garrison Transportation',
              address: 'https://www.garrisontrans.com',
              description: 'Ground Transportation Services Personal Website',
              body: 'generic'
            },
            {
              label: 'Xzam',
              address: 'https://www.xzam.net',
              description: 'Secure Web Testing Software for Universities',
              body: 'generic'
            },
            {
              label: 'Seed Science',
              description: 'Science behind different seeds mobile/web app (Not currently published)',
              body: 'generic'
            }
          ]
        },
        {
          label: 'Personal Projects',
          header: 'generic',
          icon: 'person',
          children: [
            {
              label: 'Discord Bot (Raffle Bot)',
              description: 'Has a bot key so I cannot share, but creates, sets up, and executes a raffle, as well as a store to spend points won from the raffle at, on discord.',
              body: 'generic'
            },
            {
              label: 'Raffle',
              address: 'https://flinoge.github.io/Raffle/',
              description: 'A Website Originally Used as the Raffle-Bot (Key no longer valid)',
              body: 'generic'
            },
            {
              label: 'Misc Games on Unreal Engine',
              description: 'Done tutorials and experimented with my own games on unreal engine.',
              body: 'generic'
            }
          ]
        }
      ]
    }
  },
  methods: {
    openURL
  }
}
</script>

<style scoped>
</style>
