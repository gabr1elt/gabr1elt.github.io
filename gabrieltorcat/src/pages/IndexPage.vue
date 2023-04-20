<template>
  <q-page class="row items-center justify-center bg-primary">


    <q-card class="q-page-outer bg-primary" flat square>

      <q-card-section class="row items-center justify-center ">
        <q-avatar size="100%" color="secondary">
          <img src="~assets/images/Portrait_silouette_small.png">
          <!-- <img src="~assets/images/Portrait_circle_small.png"> -->
        </q-avatar>
      </q-card-section>

      <q-card-section>
        <h1 :class="$q.screen.gt.md ? 'text-h1' : 'text-h2'" class="text-center text-secondary">Gabriel Torcat</h1>
        <div :class="$q.screen.gt.md ? 'text-subtitle1' : 'text-subtitle2'" class=" text-center text-secondary">INNOVATION
          / TECHNOLOGY / X06</div>
      </q-card-section>

      <q-card-actions align="around">
        <q-btn round color="secondary" text-color="primary" size="lg" icon="mail" />
        <q-btn round color="secondary" text-color="primary" size="lg" icon="description" />
        <q-btn round color="secondary" text-color="primary" size="lg" icon="fa-brands fa-linkedin-in" />
      </q-card-actions>

      <q-card-section>
        <h2 :class="$q.screen.gt.md ? 'text-h2' : 'text-h3'" class=" text-left text-secondary">Profile</h2>
        <div :class="$q.screen.gt.md ? 'text-body1' : 'text-body2'" class=" text-center text-justify text-secondary">
          Firm promoter of Innovation and the Work Smarter and Not Harder Principle. I don't Believe in Problems, I
          Believe in Solutions. A scientist at heart, I apply critical and strategic thinking to materialize solid and
          cutting-edge business solutions to improve performance, drive innovation and achieve growth.
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
