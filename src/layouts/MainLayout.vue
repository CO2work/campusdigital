<template>
  <q-layout view="lHr LpR ffr">
    <q-header class="col-auto bg-transparent" style="left: unset;">
      <q-toolbar class="col-auto bg-blue-5">
<!--        <q-toolbar-title>Campus Digital UMSNH</q-toolbar-title>-->
        <q-btn
          flat
          dense
          round
          icon="las la-bars"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="rightDrawerOpen"
      show-if-above

      :mini="miniState"

      :width="400"
      :breakpoint="600"

      side="right"
      behavior="desktop"
      bordered
      class="bg-grey-1 row"
    >
      <q-scroll-area class="fit">
        <q-list>
          <EssentialLink
            v-for="link in essentialLinks"
            :key="link.title"
            :obj="link.obj"
            :title="title"
            v-bind="link"
          />
        </q-list>

      </q-scroll-area>

      <div class="absolute" style="bottom: 15px; left: -17px">
        <q-btn
          dense
          round
          unelevated
          color="primary"
          icon="las la-angle-left"
          @click="miniState = !miniState"
        ></q-btn>
      </div>
    </q-drawer>

    <Dialog/>

    <q-page-container>
      <router-view />
    </q-page-container>

<!--    <q-footer reveal class="bg-transparent text-white">-->
<!--      <q-toolbar>-->
<!--        <q-avatar>-->
<!--          <img src="~assets/umsnh_escudo_svg_v1.svg" alt="Escudo UMSNH">-->
<!--        </q-avatar>-->
<!--        <p  class="text-overline text-white q-px-sm">-->
<!--          <span>-->
<!--            Universidad Michoacana de San nicolas de Hidalgo-->
<!--          </span>-->
<!--        </p>-->
<!--      </q-toolbar>-->
<!--    </q-footer>-->

  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink.vue'
import Dialog from 'components/Dialog.vue'

const linksList = [
  {
    title: 'Campus Digital',
    caption: 'UMSNH',
    icon: 'las la-university',
    link: './'
  },
  {
    title: 'Plataformas de Educación',
    caption: 'UMSNH',
    icon: 'las la-school',
    link: '',
    obj: {
      tipo: 'plataformas',
      title: 'Plataformas de Educación'
    }
  },
  {
    title: 'Servicios Digitales',
    caption: 'y de Información',
    icon: 'las la-comments',
    link: '',
    obj: {
      tipo: 'servicios',
      title: 'Servicios Digitales y de Información'
    }
  },
  {
    title: 'Publicaciones digitales',
    caption: 'Revistas, libros y blogs',
    icon: 'las la-atom',
    link: '',
    obj: {
      tipo: 'publicaciones',
      title: 'Publicaciones digitales y Revistas digitales',
      slides: ['https://cdn.quasar.dev/img/mountains.jpg', 'https://cdn.quasar.dev/img/parallax1.jpg']
    }
  },
  {
    title: 'Repositorios en línea',
    caption: 'Índices y repositorios',
    icon: 'las la-project-diagram',
    link: '',
    obj: {
      tipo: 'repositorios',
      title: 'Repositorios en línea',
      slidesNoAun: ['img1', 'img2']
    }
  },
  {
    title: 'Cultura Digital',
    caption: 'Cultura UMSNH',
    icon: 'las la-broadcast-tower',
    link: '',
    obj: {
      tipo: 'cultura',
      title: 'Cultura Digital'
    }
  },
  {
    title: 'ADINI - UMSNH',
    caption: 'Agenda Digital Nicolaita',
    icon: 'las la-vector-square',
    link: '',
    obj: {
      tipo: 'adini',
      title: 'ADINI - UMSNH'
    }
  }
]

import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
    Dialog
  },

  setup () {
    const rightDrawerOpen = ref(false)
    const miniState = ref(false)

    return {
      essentialLinks: linksList,
      rightDrawerOpen,
      toggleLeftDrawer () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      },

      drawer: ref(false),
      miniState: ref(true),

      drawerClick (e) {
        // if in "mini" state and user
        // click on drawer, we switch it to "normal" mode
        if (miniState.value) {
          miniState.value = false

          // notice we have registered an event with capture flag;
          // we need to stop further propagation as this click is
          // intended for switching drawer to "normal" mode only
          e.stopPropagation()
        }
      }
    }
  }
})
</script>
