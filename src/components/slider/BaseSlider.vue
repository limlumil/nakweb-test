<template>
  <!-- Base slider component start -->
  <div class="base-slider" @mouseover="handleMouseOverSlide" @mouseleave="handleMouseLeaveSlide">
    <!-- Handling transition animation for the slides -->
    <transition :name="slideDirection === 'next' ? 'slide-left' : 'slide-right'">
      <div class="content" :key="currentIndex">
        <!-- Slot for the current slide content -->
        <slot :currentIndex="currentIndex"></slot>
      </div>
    </transition>

    <!-- Display controls (prev/next) if 'control' prop is true -->
    <div v-if="control" class="controls-container">

      <!-- Previous button -->
      <div class="control-button prev-button" @click="prevSlide">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512" class="icon-chevron-left">
          <path
            d="M9.4 233.4c-12.5 12.5-12.5 32.8 0 45.3l192 192c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L77.3 256 246.6 86.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0l-192 192z" />
        </svg>
      </div>

      <!-- Pagination to display the current slide number -->
      <div class="pagination">{{ currentIndex + 1 }} / {{ totalSlides }}</div>

      <!-- Next button -->
      <div class="control-button next-button" @click="nextSlide">
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512" class="icon-chevron-right">
          <path
            d="M310.6 233.4c12.5 12.5 12.5 32.8 0 45.3l-192 192c-12.5 12.5-32.8 12.5-45.3 0s-12.5-32.8 0-45.3L242.7 256 73.4 86.6c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0l192 192z" />
        </svg>
      </div>
    </div>

    <!-- Display progress bar if 'autoPlay' prop is true -->
    <div v-if="autoPlay" class="progress-bar-container">
      <div class="progress-bar" :style="{ width: progressBarWidth + '%' }" @transitionend="handleTransitionEnd"></div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'BaseSlider',
  props: {
    // Total number of slides
    totalSlides: {
      type: Number,
      required: true
    },
    // Whether the slide should auto-play
    autoPlay: {
      type: Boolean,
      default: false
    },
    // Whether to display the controls
    control: {
      type: Boolean,
      default: true
    },
    // Duration of each slide in auto-play mode
    slideDuration: {
      type: Number,
      default: 8000
    }
  },
  data() {
    return {
      currentIndex: 0,
      progressBarWidth: 0,
      progressInterval: null,
      mouseOverSlide: false,
      slideDirection: 'next'
    }
  },
  watch: {
    // Resets and restarts the progress when the slide changes
    currentIndex() {
      this.resetProgress()
      this.startAutoPlay()
    }
  },
  methods: {
    // Go to the next slide
    nextSlide() {
      this.slideDirection = 'next';
      this.currentIndex = (this.currentIndex + 1) % this.totalSlides;
    },
    // Go to the previous slide
    prevSlide() {
      this.slideDirection = 'prev';
      this.currentIndex = (this.currentIndex - 1 + this.totalSlides) % this.totalSlides;
    },
    // Handle the end of the progress bar
    handleTransitionEnd() {
      if (this.progressBarWidth >= 100) {
        this.nextSlide()
      }
    },
    // Handle mouse hover over the slider
    handleMouseOverSlide() {
      if (this.control === false) return;
      this.mouseOverSlide = true
      this.resetProgress()
      clearInterval(this.progressInterval)
    },
    // Handle mouse leaving the slider
    handleMouseLeaveSlide() {
      if (this.control === false) return;
      this.mouseOverSlide = false
      this.startAutoPlay()
    },
    // Reset the progress bar
    resetProgress() {
      clearInterval(this.progressInterval)
      this.progressBarWidth = 0
    },
    // Begin auto-play
    startAutoPlay() {
      if (this.autoPlay && this.mouseOverSlide === false) {
        this.progressInterval = setInterval(() => {
          this.progressBarWidth += 1

          if (this.progressBarWidth >= 100) {
            clearInterval(this.progressInterval)
            this.nextSlide()
          }
        }, this.slideDuration / 100)
      }
    }
  },
  // When the component is mounted, start auto-play if needed
  mounted() {
    this.startAutoPlay();
  },
  // Before destroying the component, clear any intervals
  beforeDestroy() {
    clearInterval(this.progressInterval)
  }
}
</script>

<style lang="scss">
// Default basic slider style
.base-slider {
  position: relative;
  overflow: hidden;
  min-height: 390px;

  .content {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: inline-flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: flex-start;
  }

  .controls-container {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 0 30px 0;
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    z-index: 2;
    font-weight: 600;

    .control-button {
      margin: 0 10px;
      cursor: pointer;
    }

    .pagination {
      margin: 0 15px;
    }
  }

  .progress-bar-container {
    position: absolute;
    bottom: 0;
    width: 100%;
    background-color: #e0e0e0;
    height: 4px;

    .progress-bar {
      height: 100%;
      background-color: green;
      transition: width 0.03s linear;
    }
  }

  .slide-left-enter-active,
  .slide-left-leave-active,
  .slide-right-enter-active,
  .slide-right-leave-active {
    transition: transform .3s ease-in-out;
  }

  .slide-right-enter,
  .slide-left-leave-to {
    transform: translateX(-100%);
  }

  .slide-right-leave-to,
  .slide-left-enter {
    transform: translateX(100%);
  }

  .icon-chevron-right,
  .icon-chevron-left {
    width: 13px;
    height: 13px;
    fill: #333;
    cursor: pointer;
    opacity: 0.5;

    &:hover {
      opacity: 1;
    }
  }
}
</style>
