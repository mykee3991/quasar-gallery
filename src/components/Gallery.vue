<template>
  <q-page>
    <div class="row q-col-gutter-md q-pa-md">
      <div
        class="col-xl-2 col-lg-4 col-md-6 col-sm-12 col-xs-12"
        v-for="(img, index) in state.images"
        :key="`img-${index}`"
      >
        <q-img
          class="cursor-pointer"
          :src="img"
          :ratio="1 / 1"
          spinner-color="primary"
          spinner-size="82px"
          @click="methods.showImage(index)"
        />
      </div>
    </div>

    <q-dialog
      ref="carouselDialog"
      v-model="state.show"
      @before-hide="methods.beforeImageDialogHide"
      @show="methods.addListener"
    >
      <q-card
        :style="
          $q.screen.sm || $q.screen.lt.md
            ? 'min-width: 100vw'
            : 'min-width: 60vw;'
        "
        @mouseenter="state.mouseHover = true"
        @mouseleave="state.mouseHover = false"
      >
        <q-carousel
          class="bg-black contain"
          control-color="grey"
          swipeable
          animated
          v-model="state.slide"
          infinite
          height="80vh"
          arrows
          ref="carousel"
          :fullscreen="$q.screen.lt.md || state.fullscreen"
        >
          <q-carousel-slide
            v-for="(image, i) in state.images"
            :key="`image-${i}`"
            :name="i"
            :img-src="image"
          >
          </q-carousel-slide>

          <template v-slot:control>
            <q-carousel-control position="top-right" :offset="[18, 18]">
              <div
                class="q-gutter-x-sm"
                v-show="state.mouseHover || $q.screen.lt.md"
              >
                <q-btn
                  style="background-color: rgba(0, 0, 0, 0.5)"
                  round
                  flat
                  dense
                  color="white"
                  text-color="white"
                  :icon="state.fullscreen ? 'fullscreen_exit' : 'fullscreen'"
                  @click="state.fullscreen = !state.fullscreen"
                  v-show="!$q.screen.lt.md"
                >
                  <q-tooltip> Fullscreen </q-tooltip>
                </q-btn>
                <q-btn
                  style="background-color: rgba(0, 0, 0, 0.5)"
                  round
                  flat
                  dense
                  text-color="white"
                  icon="close"
                  v-close-popup
                >
                  <q-tooltip> Close </q-tooltip>
                </q-btn>
              </div>
            </q-carousel-control>
          </template>
        </q-carousel>
      </q-card>
    </q-dialog>
  </q-page>
</template>
<script lang="ts">
import { defineComponent, ref, reactive } from "@vue/composition-api";
import { albums } from "./images";
import {State, Method} from "./models"

export default defineComponent({
  name: "Gallery",
  props: {
    category: {
      type: String,
      default: "",
    },
  },
  setup(props: any, context: any) {
    //initializa image data
    const refs = context.refs;
    const methods: Method = {};

    const data: State = {
      mouseHover: false,
      slide: 0,
      fullscreen: false,
      deleteDialog: false,
      show: false,
    };

    var tmp: Array<string> = [];
    for (let i = 0; i < albums.length; i++) {
      if (albums[i].category == props.category) {
        tmp = [...albums[i].images];
      } else if (props.category == "") {
        tmp = [...tmp, ...albums[i].images];
      }
    }
    data.images = tmp;

    methods.carouselKeyboardControl = (e: any) => {
      if (e.keyCode == 39) {
        refs.carousel.next();
      } else if (e.keyCode == 37) {
        refs.carousel.previous();
      }
    };

    const client: any = window;
    methods.beforeImageDialogHide = () => {
      data.mouseHover = false;
      data.fullscreen = false;
      client.removeEventListener("keydown", methods.carouselKeyboardControl);
    };

    methods.addListener = () => {
      
      client.addEventListener("keydown", methods.carouselKeyboardControl);
    };

    methods.showImage = (index:number) => {
      data.show = true;
      data.slide = index;
    }

    
    const state: State = reactive(data);
    return { state, methods };
  },
});
</script>