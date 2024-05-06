<template>
  <div id="vueapp" class="full-width-slider">
    <div class="slider-container"
         @mousedown="startDrag"
         @mouseup="stopDrag"
         @mouseleave="stopDrag"
         @mousemove="dragging"
         :style="{ 
           transform: `translateX(${translateX}px)`, 
           transition: isDragging ? 'none' : 'transform 0.3s ease',
           width: images.length * 100 + '%' 
         }">
      <div class="slider-item"
           v-for="(image, index) in images"
           :key="index"
           :style="{ 
             backgroundImage: 'url(' + image.url + ')',
             backgroundSize: 'cover',
             backgroundPosition: 'center'
           }">
      </div>
      <!-- <div style="position: fixed;height: 270px;background-color: antiquewhite;display: flex;flex-flow: column;align-items: start;">
        <span>Consectetur leo quis vitae viverra aenean ornare</span>
        <span>Ullamcorper id at dolor sed eu ornare orci sem </span>
        <span>Consequat egestas volutpat mattis suscipit. At semper urna tortor sed purus proin volutpat. Neque nisl quis nulla etiam. </span>
        <span>READ MORE</span>
      </div> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      startX: 0,
      currentX: 0,
      translateX: 0,
      isDragging: false,
      images: [
        { url: require('@/assets/banner1.jpg') },  // Use require if your setup supports it, or direct URL if not
        { url: require('@/assets/banner2.jpg') },
        { url: require('@/assets/banner3.jpg') }
      ]
    };
  },
  methods: {
    startDrag(e) {
      this.isDragging = true;
      this.startX = e.clientX;
      this.currentX = this.translateX;
    },
    dragging(e) {
      if (this.isDragging) {
        const dx = e.clientX - this.startX;
        this.translateX = this.currentX + dx;
      }
    },
    stopDrag() {
      this.isDragging = false;
      const slideWidth = window.innerWidth; // assuming each slide is full width
      const index = Math.round(-this.translateX / slideWidth);
      this.translateX = -index * slideWidth;
    }
  }
}
</script>

<style scoped>
.full-width-slider {
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.slider-container {
  display: flex;
  cursor: grab;
  height: 100%;
  transition: transform 0.3s ease;
}

.slider-item {
  flex: 0 0 100%;
  height: 100%;
}
</style>
