<template>
  <div class="slider-container" ref="sliderContainer" >
    <p class="header-text">Opinion Articles</p>
    <div class="my-slider"
         @mousedown="startDrag"
         @mouseup="stopDrag"
         @mouseleave="stopDrag"
         @mousemove="dragging"
         @touchstart="startDrag"
         @touchend="stopDrag"
         @touchmove="dragging"
         @touchcancel="stopDrag">
      <div v-for="(item, index) in sliders" :key="index" class="slider-item"
           :style="{ transform: `translateX(${translateX}px)`}">
        <div class="card">
          <img :src="item.imgUrl" :alt="item.title" class="card-img">
          <div class="title-wrapper">
            {{ item.title }}
            <div class="author-name">
              <img :src="item.img" :alt="item.name" class="author-img">
              {{ item.name }}
              <div class="author-details">
                <div class="article-tag"><label>Opinion Article</label></div>
                <span class="publish-date">{{ item.date }}</span>
              </div>
            </div>
          </div>
          <div class="author-info">
            <!-- Additional author information could be placed here -->
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    sliders: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      startX: 0,
      currentX: 0,
      translateX: 0,
      isDragging: false
    };
  },
  methods: {
    startDrag(e) {
      e = e.type.includes('touch') ? e.touches[0] : e;
      this.startX = e.clientX;
      this.isDragging = true;
      this.currentX = this.translateX;
    },
    dragging(e) {
      if (this.isDragging) {
        e = e.type.includes('touch') ? e.touches[0] : e;
        const dx = e.clientX - this.startX;
        this.translateX = this.currentX + dx;
      }
    },
    stopDrag() {
      this.isDragging = false;
      this.snapToClosest();
    },
    snapToClosest() {
      const itemWidth = this.$el.querySelector('.slider-item').offsetWidth + 50; // Assume margin of 25px on each side
      const shift = this.translateX % itemWidth;
      if (Math.abs(shift) > itemWidth / 2) {
        this.translateX -= (itemWidth - Math.abs(shift)) * Math.sign(shift);
      } else {
        this.translateX -= shift;
      }
      const maxTranslateX = 0;
      const minTranslateX = -(itemWidth * this.sliders.length - this.$el.clientWidth);
      this.translateX = Math.max(minTranslateX, Math.min(maxTranslateX, this.translateX));
    }
  }
}
</script>

<style scoped>
body {
  background: #333;
  color: white;
}

.slider-container {
  max-width: 100%;
  overflow: hidden;
}

.my-slider {
  display: flex;
  min-width: 100%;
  transition: transform 0.2s ease-in-out;
}

.slider-item {
  flex: 0 0 auto;
  width: calc(33.3333% - 50px);
  display: flex;
  justify-content: center;
  margin: 0 25px;
}

.card {
  text-align: left;
  background: white;
  color: #333;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.3);
  width: 100%;
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

.title-wrapper {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  width: calc(100% - 109px);
  padding: 10px;
  box-sizing: border-box;
  font-size: 20px;
  font-weight: 400;
}

.card-img {
  max-width: 107px;
  height: auto;
}

.author-img {
  width: 24px;
}

.author-details {
  display: flex;
  align-items: center;
  font-size: 12px;
  align-items: center;
  font-size: 12px;
  margin-top: 16px;
}

.article-tag {
  border-radius: 12px;
  display: flex;
  height: 20px;
  align-items:center;
  padding: 12px 9px;
  border: 1px solid;
}

.publish-date {
  margin-left: 12px;
}

.header-text {
  font-size: 35px;
  font-weight: 400;
  font-family: 'Ubuntu';
  text-align: justify;
  color: #171C35;
  margin-left: 25px;
}
@media (max-width: 768px) {
  .title-wrapper {
    width: 100%;
  }
  .slider-item{
    width: 88%;
  }
  .author-details{
    flex-flow: column;
  }
}
</style>
