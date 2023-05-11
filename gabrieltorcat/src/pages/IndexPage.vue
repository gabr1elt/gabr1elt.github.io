<template>
  <q-page class="row items-center justify-center bg-primary">

    <q-card class="q-page-outer bg-primary" :class="$q.screen.gt.xs ? ' q-px-xl' : ' q-px-lg'" flat square>

      <!-- Picture -->
      <q-card-section class="row items-center justify-center">
        <div v-if="!ai_active" style="width: 45%; aspect-ratio: 1; min-width: 250px;">
          <q-avatar style="width: 100%; height: 100%;" color="secondary">
            <img src="~assets/images/Portrait_silouette_small.png" />
          </q-avatar>
        </div>
      </q-card-section>

      <!-- Title -->
      <q-card-section>
        <h1 :class="$q.screen.gt.sm ? 'text-h1 q-my-lg' : 'text-h2 q-my-md'" class="text-center text-secondary">
          Gabriel Torcat
        </h1>
        <div v-if="!ai_active" :class="$q.screen.gt.sm ? 'text-subtitle1 q-my-md' : 'text-subtitle2 q-my-sm'"
          class="text-center text-secondary">
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
          <q-badge v-if="!ai_active" color="accent" floating>New</q-badge>
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">Artificial Intelligence</q-tooltip>
        </q-btn>

        <!-- AI Next -->
        <q-btn v-if="ai_active" round color="accent" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'"
          icon="navigate_next" @click="ai_getNextImage">
          <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500" anchor="bottom right"
            self="center middle">Next Image</q-tooltip>
        </q-btn>

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
      <div v-if="ai_active" class="">

        <!-- Separator -->
        <div :class="$q.screen.gt.xs ? ' q-pa-xl' : ' q-pa-lg'">
          <q-separator class="" color="secondary" inset spaced />
        </div>

        <!-- Image -->
        <q-card-section class="row items-center justify-center">
          <!-- <div style="width: 45%; aspect-ratio: 1; min-width: 250px;"> -->
          <div style="width: 70%; min-width: 250px;">

            <q-img :src="ai_image.url" style="border-radius: 25px;">
              <q-tooltip :class="$q.screen.lt.sm ? 'q-pa-xs' : ''" class="text-caption" :delay="500"
                anchor="center middle" self="center middle">{{ ai_image.info.tooltip }}</q-tooltip>
            </q-img>

            <!-- caption -->
            <div class="text-center text-secondary text-weight-thin text-caption"
              :class="$q.screen.gt.xs ? ' q-pt-md' : ' q-pt-sm'">
              {{ ai_caption }}
            </div>

          </div>
        </q-card-section>

        <!-- Info -->
        <q-card-section class="">
          <h2 :class="$q.screen.gt.sm ? 'text-h2 q-my-lg' : 'text-h3 q-my-md'" class="text-left text-secondary">
            Artificial Intelligence
          </h2>
          <div :class="$q.screen.gt.sm ? 'text-body1' : 'text-body2'" class="text-center text-justify text-secondary"
            style="text-indent: 30px">
            <p class="text-bold">
              Generative AI diffusion models finetunning and text-to-image generation with DreamBooth, Stable Diffusion
              and Hugging Face diffusers.
            </p>
            <p>
              Diffusion Models are a type of generative AI that transforms noise into a data sample of interest i.e.
              images, audio, and even 3d structures like molecules.
            </p>
            <p>
              In this particular example I fine-tune (re-train) with images of myself a general pre-trained image
              generation model 'Stable Diffusion'. So it esentially learns how to generate a new concept: Me.
            </p>
            <p>
              Check out my code at <a href="https://github.com/gabr1elt/diffusers/tree/dev/examples/dreambooth"
                target="_blank" rel="noopener noreferrer">Github</a> .
            </p>
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

import { ref, onMounted } from 'vue'
import resumeUrl from 'assets/resume/Resume.pdf?url'
import ai_imagesInfo from 'assets/ai/images.json'
const ai_imagesImport = import.meta.glob('assets/ai/*.png', { as: 'url', eager: true })

// general

const subTitle = "INNOVATION / TECHNOLOGY / X06";
const emailAddress = "hello@gabrieltorcat.com";
// const emailSubject = "Contact Request";
const linkedinUrl = "https://www.linkedin.com/in/gabriel-torcat/";
const profile =
  `Firm promoter of Innovation and the Work Smarter and Not Harder Principle. I don't Believe in Problems, I Believe in Solutions. 
  A scientist at heart, I apply critical and strategic thinking to materialize solid and cutting-edge business solutions to improve performance, 
  drive innovation and achieve growth.`;

// ai

const ai_active = ref(false)
const ai_caption = "AI generated image."
const ai_intro =
  `Generative AI diffusion models finetunning and text-to-image generation with DreamBooth, Stable Diffusion and Hugging Face diffusers.
  Diffusion Models are a type of generative AI that transforms noise into a data sample of interest i.e. images, audio, and even 3d structures like molecules.`;
const ai_info =
  `In this particular example I fine-tune (re-train) with images of myself a general pre-trained image generation model 'Stable Diffusion'. So it esentially learns how to generate a new concept: Me.
  You can check out the code used to generate this at https://github.com/gabr1elt/diffusers.`;
// shuffle images for better random effect
const ai_imagesOrder = Object.keys(ai_imagesInfo)
  .map(value => ({ value, sort: Math.random() }))
  .sort((a, b) => a.sort - b.sort)
  .map(({ value }) => value)

const ai_image = ref({})

// get next random image
function ai_getNextImage() {

  const firstImage = "2023-05-08T00:42:49.659567.png" // obama
  let nextIndex

  if (!Object.hasOwn(ai_image.value, 'orderIdx')) {

    // init to specific image
    nextIndex = ai_imagesOrder.findIndex(x => x === firstImage);

  } else {

    // get next random image
    nextIndex = (ai_image.value.orderIdx + 1) % ai_imagesOrder.length;

  }

  // update image values
  ai_image.value.orderIdx = nextIndex
  ai_image.value.url = Object.keys(ai_imagesImport).filter(k => k.includes(ai_imagesOrder[nextIndex])).map(k => ai_imagesImport[k])[0]
  ai_image.value.info = ai_imagesInfo[ai_imagesOrder[nextIndex]]

}

onMounted(() => {
  // init ai image
  ai_getNextImage()
})

</script>
