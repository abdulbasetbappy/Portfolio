<template>
    <!-- Section Subheading -->
    <div class="section-subheading animate-on-scroll">
        <!-- Title -->
        <h3 class="section-subheading-title mb-2  fw-bold text-uppercase">
            <span>{{props.title}}</span>
            <i v-if="props.faIcon" :class="props.faIcon" class="ms-2"/>
        </h3>

        <!-- Divider -->
        <hr class="solid-divider ms-1 me-1 mb-3 " :class="{'mb-sm-4': !props.description}">

        <!-- Description -->
        <p v-if="props.description" class="section-subheading-description lead text-muted ">{{props.description}}</p>
    </div>
</template>

<script setup>
/**
 * @property {String} title
 * @property {String} [description]
 * @property {String} [faIcon]
 */
const props = defineProps({
    title: String,
    description: String,
    faIcon: String
})
</script>

<style lang="scss" scoped>
.animate-on-scroll{
  animation: appear linear;
  animation-timeline: view();
  animation-range: entry 0% cover 20%;
}

@keyframes appear{
  from{
    opacity: 0;
    scale: 0.9;
  }
  to{
    opacity: 1;
    scale: 1;
  }
}
</style>