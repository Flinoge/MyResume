<template>
  <div>
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
        <div v-if="prop.node.description">
          <span class="text-weight-thin">{{ prop.node.description }}</span>
        </div>
        <span v-else class="text-weight-thin">No Description.</span>
      </div>
    </q-tree>
  </div>
</template>

<script>
export default {
  name: 'projects',
  data () {
    return {
      projects: [
        {
          label: 'Work Projects',
          header: 'generic',
          icon: 'settings',
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
            }
          ]
        },
        {
          label: 'Personal Projects',
          header: 'generic',
          icon: '',
          children: [
            {
              label: 'Discord Bot (Raffle Bot)',
              description: 'Has a bot key so I cannot share, but creates, sets up, and executes a raffle, as well as a store to spend points won from the raffle at, on discord.',
              body: 'generic'
            },
            {
              label: 'Good table presentation',
              body: 'generic'
            },
            {
              label: 'Pleasing decor',
              body: 'generic'
            }
          ]
        }
      ]
    }
  }
}
</script>

<style scoped>
</style>
