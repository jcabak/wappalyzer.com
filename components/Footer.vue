<template>
  <div>
    <div width="100%" class="text-center">
      <v-divider />

      <v-container class="px-0">
        <v-row class="text-left justify-space-between">
          <template v-for="{ to, title, items: _items } in mainNav">
            <v-col :key="title" cols="12" sm="6" md="auto" lg="2">
              <v-list color="transparent" subheader>
                <v-subheader class="subtitle-2">
                  {{ title }}
                </v-subheader>

                <template v-if="_items">
                  <v-list-item
                    v-for="{ title: _title, to: _to } in _items"
                    :key="_to"
                    :href="_to.match(/^http/) ? _to : null"
                    :target="_to.match(/^http/) ? '_blank' : '_self'"
                    :to="_to.match(/^http/) ? null : _to"
                    :rel="_to.match(/^http/) ? `noopener noreferrer` : ''"
                    dense
                  >
                    <v-list-item-title class="font-weight-regular">
                      {{ _title }}
                    </v-list-item-title>
                  </v-list-item>
                </template>
                <v-list-item v-else :to="to" color="primary" dense>
                  <v-list-item-title class="font-weight-regular">
                    {{ title }}
                  </v-list-item-title>
                </v-list-item>
              </v-list>
            </v-col>
          </template>
        </v-row>
      </v-container>
    </div>

    <div class="footer">
      <v-divider />

      <v-container tag="footer">
        <v-row justify="space-between" align="center">
          <v-col cols="12" sm="auto" class="text-center">
            <Logo class="mx-auto d-inline-block d-sm-block" />
          </v-col>

          <v-spacer />

          <v-col cols="12" sm="auto" class="text-center"> <Status /> </v-col>

          <v-col cols="12" sm="auto" class="text-center">
            <v-btn
              v-for="{ title, to } in items"
              :key="title"
              :to="to"
              class="font-weight-regular"
              text
              small
              exact
            >
              {{ title }}
            </v-btn>
          </v-col>

          <v-col cols="12" sm="auto" class="text-center">
            <v-btn
              v-for="{ icon, href } in icons"
              :key="icon"
              :href="href"
              target="blank"
              rel="noopener noreferrer"
              icon
              small
            >
              <v-icon small>
                {{ mdi[icon] }}
              </v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </div>
  </div>
</template>

<script>
import {
  mdiGithub,
  mdiSlack,
  mdiTwitter,
  mdiFacebook,
  mdiInstagram,
  mdiLinkedin,
} from '@mdi/js'
import Logo from '~/components/Logo.vue'
import Status from '~/components/Status.vue'
import { icons, items } from '~/assets/json/nav/footer.json'

export default {
  components: {
    Logo,
    Status,
  },
  props: {
    mainNav: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      icons,
      items,
      mdi: {
        mdiSlack,
        mdiTwitter,
        mdiFacebook,
        mdiInstagram,
        mdiLinkedin,
        mdiGithub,
      },
    }
  },
}
</script>

<style>
.footer .logo {
  width: 150px;
}
</style>
