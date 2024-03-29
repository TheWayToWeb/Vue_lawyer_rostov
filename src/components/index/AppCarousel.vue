<template>
  <VueSlickCarousel v-bind="settings">
    <div v-for="(i, index) in list" :class="[$style.slide]" :key="index">
      <div :class="[$style.slideContent]">
        <h3 :class="[$style.slideTitle]">{{ i.title }}</h3>
        <div :class="[$style.slideText]">
          {{ i.body }}
        </div>
      </div>
    </div>
  </VueSlickCarousel>
</template>

<script>
import axios from "axios";
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";

export default {
  name: "AppPresentationCarousel",
  props: {
    isDots: {
      type: Boolean,
      required: true
    },
    startSlide: {
      type: Number,
      default: 0
    }
  },
  components: {
    VueSlickCarousel,
  },
  data: function () {
    return {
      list: Array(25).fill({
        title: "",
        body: "",
      }),
      settings: {
        arrows: false,
        dots: this.isDots,
        infinite: true,
        initialSlide: this.startSlide,
        responsive: [
          {
            breakpoint: 360,
            arrows: true
          },
          {
            breakpoint: 375,
            arrows: true
          },
          {
            breakpoint: 390,
            arrows: true
          },
          {
            breakpoint: 768,
            arrows: true
          },
          {
            breakpoint: 820,
            arrows: true
          }
        ]
      },
    };
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/posts?_limit=26")
      .then((res) => {
        this.list = res.data;
      });
  },
};
</script>

<style module>
.slide {
  position: relative;
  display: flex !important;
  align-items: center;
  min-height: 900px;
  padding: 50px;
}

.slideContent {
  width: 100%;
  margin: 0 auto;
  padding: 0 32.5px;
}

.slideTitle {
  color: #fff;
  font-size: 54px;
  line-height: 1.1;
  margin-bottom: 13px;
  z-index: 10;
  max-width: 870px;
  white-space: break-spaces;
  overflow: hidden;
  text-overflow: ellipsis;
}

.slideText {
  color: #fff;
  font-size: 24px;
  line-height: 1.1;
  max-width: 870px;
  white-space: break-spaces;
  overflow: hidden;
  text-overflow: ellipsis;
}

@media all and (max-width: 360px) {
  .slideContent {
    padding: 0 19.5px;
    text-align: left;
    max-width: 360px;
  }

  .slideTitle {
    font-size: 34px;
    padding-left: 6.5px;
    padding-right: 6.5px;
  }

  .slideText {
    font-size: 16px;
    padding-left: 6.5px;
    padding-right: 6.5px;
  }
}

@media all and (max-width: 767px) {
  .slide {
    padding: 0;
  }

  .slideContent {
    margin: 0;
  }

  .slideText {
    max-width: 100%;
  }
}

@media all and (min-width: 768px) {
  .slideContent {
    max-width: 768px;
  }

  .slideTitle {
    font-size: 44px;
    padding-left: 26px;
    padding-right: 26px;
  }

  .slideText {
    padding-left: 26px;
    padding-right: 26px;
  }
}

@media all and (min-width: 1366px) {
  .slideContent {
    max-width: 1240px;
  }
}
</style>

<style>
@import "../../common/styles/slick.css";
</style>
