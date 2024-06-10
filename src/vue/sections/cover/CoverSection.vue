<template>
  <SectionTemplate class="parent" :section-data="props.sectionData">
    <div class="resume animate-on-scroll">
      <!--Resume-->
      <a href="/public/Abdul-Baset-Bappy-Resume.pdf" download>
      <button class="resume-btn">
        Resume
        <span>
          <i class="fa-solid fa-cloud-arrow-down"></i>
        </span>
      </button>
    </a>
    </div>
    <!-- Title -->
    <h1 class="cover-title display-1 animate-on-scroll" v-html="coverTitle" />

    <!-- Divider -->
    <hr class="solid-divider ms-1 me-1 animate-on-scroll" />

    <!-- Info Items -->
    <InlineList
      class="info-list animate-on-scroll"
      :items="props.sectionData.content['items']['contactListItems']"
    />

    <!-- Description -->
    <p
      class="cover-description lead text-normal mb-4 mb-md-5 animate-on-scroll"
      v-html="props.sectionData.content['locales']['bio']"
    />

    <!-- Social Links -->
    <SocialLinks :items="props.sectionData.content['items']['socialCircles']" />
    <div id="scroll-down-animation">
  <span class="mouse">
    <span class="move"></span>
  </span>
  <h2>Scroll down</h2>
</div>
  </SectionTemplate>

</template>

<script setup>
import SectionTemplate from "../_templates/SectionTemplate.vue";
import { computed } from "vue";
import { useData } from "../../../composables/data.js";
import { useNavigation } from "../../../composables/navigation.js";
import InlineList from "../../widgets/InlineList.vue";
import SocialLinks from "../../widgets/SocialLinks.vue";

const data = useData();
const navigation = useNavigation();

/**
 * @property {Object} sectionData
 */
const props = defineProps({
  sectionData: Object,
});

/**
 * @type {ComputedRef<String>}
 */
const coverTitle = computed(() => {
  if (navigation.isAllAtOnceMode()) {
    return props.sectionData.content["locales"]["welcome"];
  } else {
    return props.sectionData.content["locales"]["welcomeShort"];
  }
});
</script>

<style lang="scss" scoped>
@import "/src/scss/_theming.scss";

.cover-title {
  margin-bottom: 1rem;
  text-transform: uppercase;
  font-weight: bold;
}

.solid-divider {
  @include media-breakpoint-up($navigation-sidebar-breakpoint) {
    display: none;
  }
}

.info-list {
  @include generate-dynamic-styles-with-hash(
    (
      xxxl: (
        margin-bottom: 2.5rem,
      ),
      lg: (
        margin-bottom: 2rem,
      ),
      md: (
        margin-bottom: 1.2rem,
      ),
    )
  );
}
.parent {
  position: relative;
}
.resume {
  position: absolute;
  top: 25px;
  right: 30px;
  @include generate-dynamic-styles-with-hash(
    (
      xxxl: (
        margin-bottom: 2.5rem,
      ),
      lg: (
        margin-bottom: 2rem,
      ),
      md: (
        margin-bottom: 1.2rem,
      ),
    )
  );
}
.resume-btn {
  border: none;
  background: $dark;
  padding: 8px 10px;
  border-radius: 8px;
    color: white;
    font-size: large;
  span {
    margin-left: 10px;
  }
  &:hover {
    background: $primary;
    transition: all 0.3s ease-in-out;
  }

}
.cover-description{
  color: gray !important;
}
#scroll-down-animation {
  position: absolute;
  bottom: -5%;
  left: 50%;
  transform: translate(-50%,-50%);
}
@media screen and (max-width: 992px) {
  #scroll-down-animation {
    display: none;
  }
  
}

h2 {
  color: #fff;
  font-family: 'Roboto', 'Arial', sans-serif;
  font-weight: 200;
  font-size: 16px;
}

.mouse {
  margin: 0 auto;
  display: block;
  border-radius: 50px;
  border: 2px solid #212529;
  height: 85px;
  width: 50px;
  position: relative;
}

.move {
  position: absolute;
  background-color: #0284C7;
  height: 16px;
  width: 8px;
  border-radius: 4px;
  left: 50%;
  transform: translateX(-50%);
  animation: move 3s linear infinite;
}

@keyframes move {
  0% {
    transform: translate(-50%,2px);
    opacity: 0;
  }
  40% {
    transform: translate(-50%, 25px);
    opacity: 1;
  }
  80% {
    transform: translate(-50%,35px);
    opacity: 0;
  }
  100% {
    transform: translate(-50%,35px);
    opacity: 0;
  }
}

.animate-on-scroll{
  animation: appear linear;
  animation-timeline: view();
  animation-range: entry 0% cover 10%;
}

@keyframes appear{
  from{
    opacity: 0;
    scale: 0.5;
  }
  to{
    opacity: 1;
    scale: 1;
  }
}
</style>
