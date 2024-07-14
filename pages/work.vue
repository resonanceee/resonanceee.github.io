<template>
    <div class="container">
      <div class="bg"></div>
      <div class="fade-in-color" :style="{ opacity: fadeOpacity }"></div>
      <div class="fullscreen-container">
        <div class="heading-content">
          <div class="heading"><p class="heading-title">5</p></div>
          <div class="heading"><p class="heading-text">projects</p></div>
        </div>
        <div ref="scrollDownIndicator" class="scroll-down-indicator">
          <img src="/assets/icons/scroll-down-text.png" class="scroll-down-text" alt="">
          <img src="/assets/icons/arrow-down-solid.svg" class="arrow-down" alt="">
        </div>
      </div>
      <Projects />
    </div>
</template>
  
<script>
  export default {
    data() {
      return {
        initialStripeSize: 5,
        maxStripeSize: 190,
        fadeOpacity: 0,
      };
    },
    methods: {
      handleScroll() {
        const scrollPosition = window.scrollY;
        const windowHeight = document.documentElement.scrollHeight - window.innerHeight;
        const scrollPercentage = (scrollPosition / windowHeight) / 8; // final division is a hack to slow down scroll speed
        const newStripeSize = this.initialStripeSize + (scrollPercentage * (this.maxStripeSize - this.initialStripeSize));
        this.updateBackgroundGradient(newStripeSize);
        this.updateFadeInOpacity(scrollPercentage);
      },
      updateBackgroundGradient(stripeSize) {
        const bgElement = document.querySelector('.bg');
        if (bgElement) {
          const transparentSize = Math.max(90 - stripeSize, 0);
          bgElement.style.background = `repeating-linear-gradient(
            -45deg,
            #efa819,
            #efa819 ${stripeSize}px,
            black 1px,
            transparent 4px,
            transparent ${transparentSize}px
          )`;
        }
      },
      updateFadeInOpacity(scrollPercentage) {
        const fadeStart = 0;
        const fadeEnd = 0.1;
        if (scrollPercentage > fadeStart && scrollPercentage < fadeEnd) {
          const adjustedPercentage = (scrollPercentage - fadeStart) / (fadeEnd - fadeStart);
          this.fadeOpacity = Math.min(adjustedPercentage, 1);
        } else if (scrollPercentage >= fadeEnd) {
          this.fadeOpacity = 1;
        } else {
          this.fadeOpacity = 0;
        }
      }
    },
    mounted() {
      window.addEventListener('scroll', this.handleScroll);
    },
    beforeDestroy() {
      window.removeEventListener('scroll', this.handleScroll);
    },
  };
</script>

<style scoped>

.fade-in-color {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 200vh;
  background-color: #efa819;
  transition: opacity 0.5s ease;
  z-index: -1;
}

.container {
    display: flex;
    position: relative;
    align-items: flex-start;
    flex-direction: column;
}

.fullscreen-container {
    display: flex;
    color: #fff;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
    position: relative;
}

.bg {
    display: flex;
    height: 200vh;
    width: 100vw;
    background: repeating-linear-gradient(
        -45deg,
        #efa819,
        #efa819 5px,
        black 1px,
        transparent 4px,
        transparent 95px
    );
    position: absolute;
    transform: rotate(180deg);
    z-index: -10;
}

.bg::before {
    position: absolute;
    content: '';
    top: 0;
    left: 0;
    width: 0;
    height: 0;
    background: linear-gradient(to bottom right, #4d2282 50%, transparent 50%);
    animation: revealStripes 1.2s forwards;
}

@keyframes revealStripes {
    0% {
        width: 200%;
        height: 200%;
    }
    100% {
        width: 0;
        height: 0;
    }
}
  
.heading {
    display: flex;
    position: relative;
    justify-content: center;
    align-items: center;
    margin: 0;
}

.heading-title {
    font-size: 35rem;
    font-weight: 700;
    margin-right: auto;
    animation: fadeInUp 1s ease-out forwards;
    text-shadow: 4px 4px 8px rgba(0, 0, 0, 0.5);

}

@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(20px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.heading-text {
    font-size: 5rem;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);    
    animation: fadeInUp 1s ease-out forwards;
}

.scroll-down-indicator {
    transition: opacity 0.5s ease-out;
    position: absolute;
    top: 85%;
    left: 50%;
    transform: translate(-50%, -25%);
    opacity: 1;
}

.scroll-down-text {
    animation: spin-slow 3s linear infinite;
    width: 120px;
}

.arrow-down {
    width: 35px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

@keyframes spin-slow {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
}

@media (max-width: 768px) {
    .heading-title {
        margin: 0;
        padding: 0;
        line-height: 1;
    }

    .heading-title {
        font-size: 25rem;
    }

    .heading-text {
        font-size: 2rem;
    }

    .scroll-down-text {
        animation: spin-slow 3s linear infinite;
        width: 100px;
    }

    .arrow-down {
        width: 25px;
    }

}

@media (max-width: 425px) {
    .heading-title {
        font-size: 20rem;
    }

    .heading-text {
        font-size: 2rem;
    }
}
</style>