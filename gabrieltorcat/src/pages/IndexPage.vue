<template>
  <q-page class="row items-center justify-center bg-primary">

    <q-card class="q-page-outer bg-primary" :class="$q.screen.gt.xs ? ' q-px-xl' : ' q-px-lg'" flat square>

      <!-- Picture -->
      <q-card-section class="row items-center justify-center">
        <div style="width: 45%; aspect-ratio: 1; min-width: 250px;">
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
          class="text-center text-secondary">
          {{ subTitle }}
        </div>
      </q-card-section>

      <!-- Buttons -->
      <q-card-actions align="around">

        <!-- Mail -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" icon="mail"
          :href="'mailto:' + emailAddress" />
        <!-- :href="'mailto:' + emailAddress + '?subject=' + emailSubject" /> -->

        <!-- Resume -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" icon="description"
          type="application/pdf" :href="resumeUrl" target="_blank" />
        <!-- type="application/pdf" href="assets/resume/Resume.pdf" target="_blank" download="Gabriel Torcat - Resume" /> -->

        <!-- LinkedIn -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'" :href="linkedinUrl"
          target="_blank">
          <q-icon :size="$q.screen.gt.sm ? 'md' : 'sm'" name="fa-brands fa-linkedin-in" />
          <!-- <q-icon :size="$q.screen.gt.sm ? 'md' : 'sm'" name="fa-brands fa-linkedin-in fa-bounce" /> -->
        </q-btn>

        <!-- AI -->
        <q-btn round color="secondary" text-color="primary" :size="$q.screen.gt.sm ? 'lg' : 'md'">
          <q-icon :size="$q.screen.gt.sm ? 'lg' : 'md'" name="img:/icons/ai/ai_microchip.svg" />
          <q-badge color="orange" floating>new</q-badge>
        </q-btn>

      </q-card-actions>

      <!-- Profile -->
      <q-card-section class="">
        <h2 :class="$q.screen.gt.sm ? 'text-h2 q-my-lg' : 'text-h3 q-my-md'" class="text-left text-secondary">
          Profile
        </h2>
        <div :class="$q.screen.gt.sm ? 'text-body1' : 'text-body2'" class="text-center text-justify text-secondary"
          style="text-indent: 30px">
          {{ profile }}
        </div>
      </q-card-section>

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

import resumeUrl from 'assets/resume/Resume.pdf?url'

const subTitle = "INNOVATION / TECHNOLOGY / X06";
const emailAddress = "contact@gabrieltorcat.com";
// const emailSubject = "Contact Request";
const linkedinUrl = "https://www.linkedin.com/in/gabriel-torcat/"
const profile =
  `Firm promoter of Innovation and the Work Smarter and Not Harder Principle. I don't Believe in Problems, I Believe in Solutions. 
  A scientist at heart, I apply critical and strategic thinking to materialize solid and cutting-edge business solutions to improve performance, 
  drive innovation and achieve growth.`;

</script>
