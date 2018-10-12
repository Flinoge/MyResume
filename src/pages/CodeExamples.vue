<template>
  <div>
    <div style="padding: 1em;">
      <q-carousel no-swipe arrows quick-nav>
        <q-carousel-slide>
          <q-card flat style="padding: 2em;">
            <q-card-title>Chat System</q-card-title>
            <q-card-separator/>
            <q-chat-message
              label='Thursday, October 11th, 2018'
            />
            <q-chat-message
              v-for="(message, index) in chat" :key="index"
              :name="message.user"
              :avatar="message.picture"
              :text="message.message"
              :stamp="message.time"
              :sent="message.user !== 'Trevor'"
            />
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide>
          <q-card flat style="padding: 1em;">
            <q-table
              title="Table of Data"
              :data="goods"
              :columns="admincolumns"
              selection="multiple"
              row-key="name"
              :selected.sync="selected"
            >
              <template slot="top-selection" slot-scope="props">
                <q-btn color="secondary" flat label="Do Something" class="q-mr-sm" @click="notifyImplement('Doing something')" />
                <q-btn color="secondary" flat label="Something Else" @click="notifyImplement('Doing something else')"/>
                <div class="col" />
                <q-btn color="negative" flat round delete icon="delete" @click="deleteRow(selected)" />
              </template>
              <q-tr slot="top-row" slot-scope="props">
                <q-td colspan="100%">
                  <div class="row">
                    <q-field
                      :error="rowNameError"
                      error-label="You need a name!"
                      class="col-5"
                    >
                      <q-input placeholder="New Row Name" v-model="newRowName"></q-input>
                    </q-field>
                    <q-field
                      :error="rowPriceError"
                      error-label="You need a Price!"
                      class="col-5"
                    >
                      <q-input placeholder="New Row Price" v-model="newRowPrice" type="number"></q-input>
                    </q-field>
                    <div class="col-2">
                      <q-btn size="sm" color="primary" round icon="add" @click="addRow">
                        <q-tooltip>Add New Row</q-tooltip>
                      </q-btn>
                    </div>
                  </div>
                </q-td>
              </q-tr>
              <q-tr slot="body" slot-scope="props" :props="props">
                <q-td auto-width>
                  <q-checkbox color="primary" v-model="props.selected" />
                </q-td>
                <q-td key="name" :props="props">
                  {{ props.row.name }}
                </q-td>
                <q-td key="price" :props="props">
                  {{ props.row.price }}
                </q-td>
              </q-tr>
            </q-table>
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide>
          <q-card flat style="padding: 2em;">
            <q-card-title>Loaders and Progress Bars</q-card-title>
            <q-card-separator/>
            <div class="row" style="margin-top: 1em;">
              <div class="col-6" style="margin-bottom: 1em;">
                <q-btn color="primary" @click="showLoading">Full Screen Load Random Value</q-btn>
              </div>
              <div class="col-6" style="margin-bottom: 1em;">
                <q-btn color="secondary" @click="showInnerLoading">Inner Load Random Value</q-btn>
              </div>
              <div class="col-6" style="margin-bottom: 1em;">
                <q-knob v-model="knobModel" :min="min" :max="max"></q-knob>
              </div>
              <div class="col-6" style="margin-bottom: 1em;">
                <q-slider v-model="knobModel" :min="min" :max="max" label></q-slider>
              </div>
              <div class="col-12">
                <q-input v-model="min" type="number" float-label="Want a different min value?" @input="checkMin"></q-input>
              </div>
              <div class="col-12">
                <q-input v-model="max" type="number" float-label="How about a max value?" @input="checkMax"></q-input>
              </div>
            </div>
            <q-inner-loading :visible="innerspinner">
              Calculating Random Value... Wait a minute? I mean generating!
              <q-spinner-gears size="50px" color="primary"></q-spinner-gears>
            </q-inner-loading>
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide>
          <q-card flat color="grey-1" text-color="primary">
            <q-card-title>Infinite Feed</q-card-title>
            <q-card-separator/>
            <q-scroll-area style="width: 100%; height: 500px; margin-left: auto; margin-right: auto; padding: 2em;">
              <q-infinite-scroll :handler="loadMore">
                <q-list striped no-border multiline separator>
                  <q-list-header>My Feed (Scroll Down to Load more)</q-list-header>
                  <q-item v-for="(item, index) in scrollitems" class="caption" :key="index">
                    <q-item-side>{{index + 1}}</q-item-side>
                    <q-item-main>
                      <q-item-tile>
                        {{item.message}}
                      </q-item-tile>
                    </q-item-main>
                  </q-item>
                </q-list>
                <q-spinner-gears slot="message" :size="40"></q-spinner-gears>
              </q-infinite-scroll>
            </q-scroll-area>
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide>
          <q-card flat>
            <q-card-title>Want to pick your own colors?</q-card-title>
            <q-card-main>
              <div class="row">
                <q-field
                  helper="Pick a Background Color!"
                  class="col-xl-6 col-lg-6 col-md-6 col-sm-6 col-xs-12"
                >
                  <q-color-picker v-model="pickBackgroundColor"></q-color-picker>
                </q-field>
                <q-field
                  helper="Pick a Text Color!"
                  class="col-xl-6 col-lg-6 col-md-6 col-sm-6 col-xs-12"
                >
                  <q-color-picker v-model="pickTextColor"></q-color-picker>
                </q-field>
                <q-card flat class="col-12">
                  <q-card-title :style="'color: ' + pickTextColor + ';'">Play with the colors a little!</q-card-title>
                </q-card>
              </div>
            </q-card-main>
            <q-card-actions>
              <q-btn :style="'color: ' + pickTextColor + '; background-color: ' + pickBackgroundColor + ';'">Button!</q-btn>
            </q-card-actions>
          </q-card>
        </q-carousel-slide>
        <q-carousel-slide>
          <q-card flat>
            <q-card-title>Want a custom example?</q-card-title>
            <q-card-main>
              <q-stepper ref="stepper">
                <q-step default title="First Step" subtitle="Here we go">
                  Decide what example it is you want to see.
                </q-step>
                <q-step title="Then you...">
                  Send an email to trevororgill80@gmail.com including what you would like to see.
                </q-step>
                <q-step title="Finally!">
                  Wait and I'll quickly update my website to include an example of what you would like!
                </q-step>
                <q-stepper-navigation>
                  <q-btn
                    flat
                    @click="$refs.stepper.previous()"
                    label="Back"
                  />
                  <q-btn
                    @click="$refs.stepper.next()"
                    label="Next"
                  />
                </q-stepper-navigation>
              </q-stepper>
            </q-card-main>
          </q-card>
        </q-carousel-slide>
      </q-carousel>
    </div>
  </div>
</template>

<script>
export default {
  name: 'code-examples',
  data () {
    return {
      pickBackgroundColor: '#FFF',
      pickTextColor: '#000',
      scrollitems: [{
        message: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam nec risus vehicula, condimentum neque vitae, aliquet turpis. Integer ipsum risus, sodales consequat mauris non, venenatis porta metus. Curabitur metus ex, posuere sollicitudin odio ac, consequat maximus lorem. Nulla facilisi. Quisque aliquet diam ut viverra sagittis. Pellentesque tincidunt porttitor orci et mollis. Praesent eget mi arcu. Aliquam egestas nisi eget dolor eleifend, at volutpat justo sollicitudin. Nunc mollis risus vitae egestas ullamcorper. Aenean sit amet justo nec erat euismod ultrices. Integer sed tellus sit amet quam interdum fermentum. Curabitur iaculis libero eget leo dignissim tincidunt.\n' +
        '\n' +
        'Quisque ut lorem lacinia, hendrerit augue nec, rutrum diam. Phasellus a feugiat urna, in facilisis nulla. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Quisque ornare convallis aliquet. Aliquam leo mauris, eleifend vitae massa vitae, sollicitudin laoreet magna. Ut convallis tortor est, a bibendum lorem ornare non. Aenean dignissim semper sapien vitae iaculis. Morbi at dictum lectus. In dignissim sem non finibus pulvinar. Vivamus quis lorem quis augue facilisis dictum. Mauris varius suscipit leo ut elementum.\n' +
        '\n'
      },
      {
        message: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam nec risus vehicula, condimentum neque vitae, aliquet turpis. Integer ipsum risus, sodales consequat mauris non, venenatis porta metus. Curabitur metus ex, posuere sollicitudin odio ac, consequat maximus lorem. Nulla facilisi. Quisque aliquet diam ut viverra sagittis. Pellentesque tincidunt porttitor orci et mollis. Praesent eget mi arcu. Aliquam egestas nisi eget dolor eleifend, at volutpat justo sollicitudin. Nunc mollis risus vitae egestas ullamcorper. Aenean sit amet justo nec erat euismod ultrices. Integer sed tellus sit amet quam interdum fermentum. Curabitur iaculis libero eget leo dignissim tincidunt.\n' +
        '\n' +
        'Quisque ut lorem lacinia, hendrerit augue nec, rutrum diam. Phasellus a feugiat urna, in facilisis nulla. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Quisque ornare convallis aliquet. Aliquam leo mauris, eleifend vitae massa vitae, sollicitudin laoreet magna. Ut convallis tortor est, a bibendum lorem ornare non. Aenean dignissim semper sapien vitae iaculis. Morbi at dictum lectus. In dignissim sem non finibus pulvinar. Vivamus quis lorem quis augue facilisis dictum. Mauris varius suscipit leo ut elementum.\n' +
        '\n'
      }],
      innerspinner: false,
      knobModel: 3,
      min: 0,
      max: 10,
      rowNameError: false,
      rowPriceError: false,
      newRowName: '',
      newRowPrice: 0,
      selected: [],
      admincolumns: [
        {
          name: 'name',
          required: true,
          label: 'Product Name',
          align: 'left',
          field: 'name',
          sortable: true
        },
        {
          name: 'price',
          required: true,
          label: 'Product Price (In Dollars)',
          align: 'left',
          field: 'price',
          sortable: true
        }
      ],
      goods: [
        {
          'name': 'Headphones',
          'price': 20,
          'id': 0
        },
        {
          'name': 'Pencil',
          'price': 1,
          'id': 1
        },
        {
          'name': 'Flatscreen TV',
          'price': 500,
          'id': 2
        }
      ],
      chat: [
        {
          'message': ['Hey There!'],
          'user': 'Trevor',
          'time': '10 Minutes Ago',
          'picture': '../statics/MyProfile.jpg'
        },
        {
          'message': ['Hey Man, I need your help.'],
          'user': 'Customer',
          'time': '5 Minutes Ago',
          'picture': '../statics/Profile.jpg'
        },
        {
          'message': ['What do you need?'],
          'user': 'Trevor',
          'time': '4 Minutes Ago',
          'picture': '../statics/MyProfile.jpg'
        },
        {
          'message': ['Thank goodness you are here!', 'A Chat System!'],
          'user': 'Customer',
          'time': '<1 Minute Ago',
          'picture': '../statics/Profile.jpg'
        },
        {
          'message': ['I have what you need!'],
          'user': 'Trevor',
          'time': 'Just Now',
          'picture': '../statics/MyProfile.jpg'
        }
      ]
    }
  },
  methods: {
    loadMore (index, done) {
      this.scrollitems.push({message: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam nec risus vehicula, condimentum neque vitae, aliquet turpis. Integer ipsum risus, sodales consequat mauris non, venenatis porta metus. Curabitur metus ex, posuere sollicitudin odio ac, consequat maximus lorem. Nulla facilisi. Quisque aliquet diam ut viverra sagittis. Pellentesque tincidunt porttitor orci et mollis. Praesent eget mi arcu. Aliquam egestas nisi eget dolor eleifend, at volutpat justo sollicitudin. Nunc mollis risus vitae egestas ullamcorper. Aenean sit amet justo nec erat euismod ultrices. Integer sed tellus sit amet quam interdum fermentum. Curabitur iaculis libero eget leo dignissim tincidunt.\n' +
        '\n' +
        'Quisque ut lorem lacinia, hendrerit augue nec, rutrum diam. Phasellus a feugiat urna, in facilisis nulla. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Quisque ornare convallis aliquet. Aliquam leo mauris, eleifend vitae massa vitae, sollicitudin laoreet magna. Ut convallis tortor est, a bibendum lorem ornare non. Aenean dignissim semper sapien vitae iaculis. Morbi at dictum lectus. In dignissim sem non finibus pulvinar. Vivamus quis lorem quis augue facilisis dictum. Mauris varius suscipit leo ut elementum.\n' +
        '\n'
      })
      setTimeout(() => {
        done()
      }, 2000)
    },
    showInnerLoading () {
      this.innerspinner = true
      setTimeout(() => {
        this.innerspinner = false
        this.knobModel = Math.floor(Math.random() * (this.max - this.min)) + this.min
      }, 2000)
    },
    showLoading () {
      this.$q.loading.show({
        message: 'Don\'t move! Changing number now!'
      })
      setTimeout(() => {
        this.$q.loading.hide()
        this.knobModel = Math.floor(Math.random() * (this.max - this.min)) + this.min
      }, 2000)
    },
    checkMin (newVal) {
      if (newVal > this.max) {
        this.$q.notify('Min needs to be less than max!')
        this.min = this.max
      }
      if (this.knobModel < newVal) {
        this.knobModel = this.min
      }
    },
    checkMax (newVal) {
      if (newVal < this.min) {
        this.$q.notify('Max needs to be more than min!')
        this.max = this.min
      }
      if (this.knobModel > newVal) {
        this.knobModel = this.max
      }
    },
    addRow () {
      this.rowNameError = false
      this.rowPriceError = false
      if (this.newRowName === '') {
        this.rowNameError = true
        return
      }
      if (this.newRowPrice === '') {
        this.rowPriceError = true
        return
      }
      let newID = 0
      for (let i = 0; i < this.goods.length; i++) {
        if (this.goods[i].id === newID) {
          break
        } else {
          newID = i + 1
        }
      }
      this.goods.push({'name': this.newRowName, 'price': this.newRowPrice, 'id': newID})
      this.newRowPrice = 0
      this.newRowName = ''
      this.$q.notify({
        message: 'Added new row!',
        color: 'positive'
      })
    },
    notifyImplement (msg) {
      this.$q.notify(msg)
    },
    deleteRow (props) {
      let indexToDelete = []
      for (let i = 0; i < this.goods.length; i++) {
        for (let j = 0; j < props.length; j++) {
          if (this.goods[i].id === props[j].id) {
            indexToDelete.push(i)
          }
        }
      }
      indexToDelete.reverse()
      for (let i = 0; i < indexToDelete.length; i++) {
        this.goods.splice(indexToDelete[i], 1)
      }
      this.selected = []
    }
  }
}
</script>

<style scoped>
</style>
