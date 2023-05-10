<template>
  <q-page class="row items-center justify-center bg-primary">

    <q-card class="q-page-outer bg-primary" :class="$q.screen.gt.xs ? ' q-px-xl' : ' q-px-lg'" flat square>

      <!-- Picture -->
      <q-card-section class="row items-center justify-center">
        <div style="width: 45%; aspect-ratio: 1; min-width: 250px;" v-if="!ai_active">
          <q-avatar style="width: 100%; height: 100%;" color="secondary">
            <img src="~assets/images/Portrait_silouette_small.png" />
            <!-- <img src="~assets/images/Portrait_circle_small.png"> -->
          </q-avatar>
        </div>
      </q-card-section>

      <!-- Title -->
      <q-card-section>
        <h1 :class="$q.screen.gt.sm ? 'text-h1 q-my-lg' : 'text-h2 q-my-md'" class="text-center text-secondary">
          Gabriel Torcat
        </h1>
        <div :class="$q.screen.gt.sm ? 'text-subtitle1 q-my-md' : 'text-subtitle2 q-my-sm'"
          class="text-center text-secondary" v-if="!ai_active">
          {{ subTitle }}
        </div>
      </q-card-section>

      <!-- Buttons -->
      <q-card-actions align="around">

        <!-- Mail -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" icon="mail"
          :href="'mailto:' + emailAddress">
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">Email</q-tooltip>
          <!-- :href="'mailto:' + emailAddress + '?subject=' + emailSubject" /> -->
        </q-btn>

        <!-- Resume -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" icon="description"
          type="application/pdf" :href="resumeUrl" target="_blank">
          <!-- type="application/pdf" href="assets/resume/Resume.pdf" target="_blank" download="Gabriel Torcat - Resume" /> -->
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">Resume</q-tooltip>
        </q-btn>

        <!-- LinkedIn -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" :href="linkedinUrl"
          target="_blank">
          <q-icon :size="$q.screen.gt.sm ? 'md' : 'sm'" name="fa-brands fa-linkedin-in" />
          <!-- <q-icon :size="$q.screen.gt.sm ? 'md' : 'sm'" name="fa-brands fa-linkedin-in fa-bounce" /> -->
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">LinkedIn</q-tooltip>
        </q-btn>

        <!-- AI -->
        <q-btn round :color="ai_active ? 'accent' : 'secondary'" text-color="primary"
          :size="$q.screen.gt.sm ? 'lg' : 'md'" @click="ai_active = !ai_active">
          <q-icon :size="$q.screen.gt.sm ? '42px' : '29px'" name="img:/icons/ai/ai_microchip.svg" />
          <q-badge color="accent" floating v-if="!ai_active">New</q-badge>
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">Artificial Intelligence</q-tooltip>
        </q-btn>

        <!-- AI Next -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" icon="navigate_next"
          @click="ai_getRandomImage" v-if="ai_active">
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">Next Image</q-tooltip>
        </q-btn>

        <!-- ????? -->
        <!-- <q-fab round color="secondary" text-color="primary" :padding="$q.screen.gt.sm ? '20px' : 'sm'"
          icon="img:/icons/ai/ai_microchip.svg" direction="up">
          <q-icon :size="$q.screen.gt.sm ? 'lg' : 'md'" name="img:/icons/ai/ai_microchip.svg" />
          <q-badge color="orange" floating>New</q-badge>
          <q-fab-action icon="alarm"></q-fab-action>
        </q-fab> -->

      </q-card-actions>

      <!-- Profile -->
      <q-card-section class="" v-if="!ai_active">
        <h2 :class="$q.screen.gt.sm ? 'text-h2 q-my-lg' : 'text-h3 q-my-md'" class="text-left text-secondary">
          Profile
        </h2>
        <div :class="$q.screen.gt.sm ? 'text-body1' : 'text-body2'" class="text-center text-justify text-secondary"
          style="text-indent: 30px">
          {{ profile }}
        </div>
      </q-card-section>

      <!-- AI -->
      <div class="" v-if="ai_active">

        <!-- Separator -->
        <div :class="$q.screen.gt.xs ? ' q-pa-xl' : ' q-pa-lg'">
          <q-separator class="" color="secondary" inset spaced />
        </div>

        <!-- Image -->
        <q-card-section class="row items-center justify-center">
          <div style="width: 45%; aspect-ratio: 1; min-width: 250px;">

            <q-img :src="ai_image.path">
              <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
                self="center middle">{{ ai_image }}</q-tooltip>
            </q-img>

            <!-- caption -->
            <div class="text-center text-secondary text-weight-thin text-caption">
              {{ ai_caption }}
            </div>

          </div>
        </q-card-section>

        <!-- Info -->
        <q-card-section class="">
          <h2 :class="$q.screen.gt.sm ? 'text-h2 q-my-lg' : 'text-h3 q-my-md'" class="text-left text-secondary">
            Info
          </h2>
          <div :class="$q.screen.gt.sm ? 'text-body1' : 'text-body2'" class="text-center text-justify text-secondary"
            style="text-indent: 30px">
            {{ ai_info }}
          </div>
        </q-card-section>

      </div>

    </q-card>

  </q-page>
</template>

<style lang="sass">

.q-page-outer
  max-width: map-get($sizes, "md")

// .text-h1

//   @media (max-width: map-get($sizes, "md"))
//     // $h6
//     @extend .text-h2

</style>

<script setup>

import { ref } from 'vue'
import resumeUrl from 'assets/resume/Resume.pdf?url'

// const aiImgs = import.meta.glob('assets/ai/*.png', { as: 'url', eager: true })
const aiImgs = import.meta.glob('assets/ai/*.png', { eager: true })
Object.values(aiImgs).forEach((v) => v())
// Object.keys(aiImgs).forEach((key) => aiImgs[key]());


// general

const subTitle = "INNOVATION / TECHNOLOGY / X06";
const emailAddress = "contact@gabrieltorcat.com";
// const emailSubject = "Contact Request";
const linkedinUrl = "https://www.linkedin.com/in/gabriel-torcat/";
const profile =
  `Firm promoter of Innovation and the Work Smarter and Not Harder Principle. I don't Believe in Problems, I Believe in Solutions. 
  A scientist at heart, I apply critical and strategic thinking to materialize solid and cutting-edge business solutions to improve performance, 
  drive innovation and achieve growth.`;

// ai

const ai_active = ref(false)
const ai_caption = "AI generated image."
const ai_info =
  `Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae neque ipsum accusamus minima quidem nostrum provident et vitae similique dolorum, corporis quam, rerum animi fuga maiores vero repellendus dicta dolorem.`;
const ai_images = {
  1: {
    "path": "assets/ai/2023-05-08T00:42:49.659567.png",
    "tooltip": "aaaaaaa"
  },
  2: {
    "path": "assets/ai/2023-05-08T15:54:20.724023.png",
    "tooltip": "aaaaaaa"
  },
  3: {
    "path": "assets/ai/2023-05-09T01:17:54.992698.png",
    "tooltip": "aaaaaaa"
  },
  4: {
    "path": "assets/ai/2023-05-09T02:49:53.530992.png",
    "tooltip": "aaaaaaa"
  },
  5: {
    "path": "assets/ai/2023-05-09T09:26:07.068974.png",
    "tooltip": "aaaaaaa"
  },
  6: {
    "path": "assets/ai/2023-05-09T11:28:30.095897.png",
    "tooltip": "aaaaaaa"
  },
  7: {
    "path": "assets/ai/2023-05-09T11:53:16.589587.png",
    "tooltip": "aaaaaaa"
  },
}
const ai_image = ref(ai_images[2])



function ai_getRandomImage() {

  // morphGroupVal.value = "ai"
  morphGroupVal.value = morphGroupVal.value === "ai" ? "regular" : "ai"

}

</script>
