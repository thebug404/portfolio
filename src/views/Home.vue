<template>
  <div class="home">
    <div class="container-fluid">
      <section v-animation class="py-3">
        <div class="row">
          <div class="col-12">
            <carousel v-bind:items="carouselItems" />
          </div>
        </div>
      </section>

      <section>
        <div class="row justify-content-center">
          <div
            v-animation
            data-effect="scale"
            :data-delay="i * 0.1"
            v-for="(item, i) in items"
            :key="i"
            class="col-12 col-sm-6 col-md-4 col-xl-3 p-3"
          >
            <item-card :item="item" />
          </div>
        </div>
      </section>

      <section class="py-4">
        <container-dynamic
          title="Technologies"
          subtitle="Some of the technologies to be used."
        >
          <div class="row">
            <div
              v-for="(item, i) in technologies"
              :key="i"
              class="col-12 col-sm-6 col-lg-4 p-3"
              v-animation
              data-effect="scale"
              :data-delay="i * 0.15"
            >
              <technology-card :technology="item" />
            </div>
          </div>
        </container-dynamic>
      </section>

      <section class="py-4">
        <container-dynamic
          title="Top Applications"
          subtitle="Take a look at the top apps"
          :pathName="'Apps'"
        >
          <slot>
            <div class="row">
              <div
                class="col-12 col-sm-6 col-lg-4 p-3"
                v-for="(app, i) in apps"
                :key="i"
                v-animation
                data-effect="scale"
                :data-delay="i * 0.2"
              >
                <app-card v-bind:app="app" />
              </div>
            </div>
          </slot>
        </container-dynamic>
      </section>

      <section>
        <container-dynamic
          title="Beautiful Packages"
          subtitle="All packages that help the community continue to grow"
          pathName="Packages"
        >
          <div class="row">
            <div
              v-for="(item, i) in packages"
              :key="i"
              class="col-12 col-sm-6 col-lg-4 p-3"
              v-animation
              data-effect="scale"
              :data-delay="i * 0.15"
            >
              <package-card :item="item" />
            </div>
          </div>
        </container-dynamic>
      </section>

      <section class="py-4">
        <container-dynamic
          title="Some Articles"
          subtitle="These are some of my articles."
          :pathName="'Articles'"
        >
          <div class="row">
            <div
              v-for="(item, i) in articles"
              :key="i"
              class="col-12 col-md-6 col-lg-4 p-3"
              v-animation
              data-effect="scale"
              :data-delay="i * 0.15"
            >
              <article-card :article="item" />
            </div>
          </div>
        </container-dynamic>
      </section>
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";

import { sortItems } from "@/utils/helpers";

import { apps, App } from "@/mock/apps.mock";
import { articles, Article } from "@/mock/articles.mock";
import { technologies, Technology } from "@/mock/technologies.mock";
import { packages, Package } from "@/mock/packages.mock";

import ContainerDynamic from "@/components/ContainerDynamic.vue";
import TechnologyCard from "@/components/TechnologyCard.vue";
import PackageCard from "@/components/PackageCard.vue";
import ArticleCard from "@/components/ArticleCard.vue";
import Carousel from "@/components/Carousel.vue";
import ItemCard from "@/components/ItemCard.vue";
import AppCard from "@/components/AppCard.vue";

@Options({
  components: {
    ContainerDynamic,
    Carousel,
    ItemCard,
    AppCard,
    ArticleCard,
    TechnologyCard,
    PackageCard,
  },
})
export default class Home extends Vue {
  carouselItems: Array<Record<string, string>> = [
    {
      title: "I'm Fullstack Developer",
      subtitle:
        "I can handle Backend, Frontend and interface design technologies. If solutions are what you want, that's my middle name.",
      picture: "https://res.cloudinary.com/dlkfpx8lb/image/upload/v1663095833/Portfolio/developer_njf6or.svg",
      color: "blue",
    },
  ];
  items = [
    {
      title: "Top apps",
      subtitle: `${apps.length} apps found.`,
      picture: "apps-icon.png",
      color: "ocean",
      route: "Apps",
    },
    {
      title: "My articles",
      subtitle: `${articles.length} apps found`,
      picture: "articles-icon.png",
      color: "yellow",
      route: "Articles",
    },
    {
      title: "My packages",
      subtitle: `${packages.length} packages found`,
      picture: "packages-icon.png",
      color: "brown",
      route: "Packages",
    },
  ];

  get apps(): App[] {
    return apps.slice(0, 3);
  }

  get articles(): Article[] {
    return sortItems(articles, "date", "DESC").slice(0, 3);
  }

  get technologies(): Technology[] {
    return technologies.slice(0, 6);
  }

  get packages(): Package[] {
    return packages.slice(0, 6);
  }
}
</script>
