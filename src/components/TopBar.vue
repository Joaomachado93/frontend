<template>
  <div id="vueapp">
    <div class="top-bar">
      <button class="hamburger" @click="toggleMenu" v-if="isMobile">&#9776;</button>
      <div v-show="menuVisible || !isMobile">
        <ul class="menu-level-1">
          <li v-for="(item, index) in menuItems" :key="index" @click="toggleSubMenu(index)" :class="{ 'active': activeSubMenuIndex === index }">
            {{ item.title }}
          </li>
        </ul>
        <div class="related-content" v-if="activeSubMenuIndex !== -1">
          <div class="container-submenu">
            <ul class="submenu">
              <li class="submenu-element" v-for="(subItem, subIndex) in menuItems[activeSubMenuIndex].submenu" :key="subIndex" @click="handleSubmenuClick(subItem)">
                {{ subItem }}
              </li>
            </ul>
            <div class="content-wrapper">
              <div class="detail-section">
                <img src="../assets/image.jpg" alt="" class="detail-image">
                <div class="detail-text">
                  GI products such as figs, pepper and olive oil grow under cooperation between the EU and Africa
                  <div class="case-study-label"><label>Case Study</label></div>
                </div>
              </div>
              <div class="info-section">
                <div class="info-box"> 
                  <div>LEADERS LEAGUE 2023</div>
                  <div style="text-align:left;display: flex;width: 100%;">The Legal 500: Intellectual Property Comparative Guide - Portugal</div>
                  <div class="case-study-label"><label>Press Release</label></div>
                </div>
                <div class="info-box-second">
                  <div style="line-height: 51px;align-content:center;">
                    <div style="font-size:50px;color: #3346AA;">12</div>
                    <div style="font-size:50px;color: #3346AA;">JUL</div>
                  </div>
                  <div style="margin-left: 16px;">
                    <div style="font-size: 16px;text-align: left;">58th Edition FACIM – Maputo’s International Trade Fair</div>
                    <div class="name"><img src="@/assets/person3.jpg" style="width: 24px; border-radius: 12px; margin-right: 4px;" alt="">Rute Franco</div>
                    <div style="font-size:12px;text-align:left;line-height: 24px;"> 
                      <img src="@/assets/location.png" style="width:16px;border-radius:12px;margin-right:4px;">
                      Póvoa de Santa Iria <img src="@/assets/clock.png" style="width:16px;border-radius:12px;margin-right: 0px;margin-left: 12px;">
                      12 a 13 julho
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      menuItems: [
        { title: 'Expertise', submenu: [] },
        { title: 'Jurisdictions', submenu: [] },
        { title: 'Team', submenu: [] },
        { title: 'IP News & Insights', submenu: [
          'Opinion Articles',
          'Announcements',
          'Press Releases',
          'Case Studies',
          'Events',
          'Insights'
        ]},
        { title: 'About Us', submenu: [] },
        { title: 'Contacts', submenu: [] }
      ],
      activeSubMenuIndex: -1,
      menuVisible: false,
      isMobile: false
    };
  },
  mounted() {
    this.checkMobile();
    window.addEventListener('resize', this.checkMobile);
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.checkMobile);
  },
  methods: {
    toggleMenu() {
      this.menuVisible = !this.menuVisible;
    },
    toggleSubMenu(index) {
      this.activeSubMenuIndex = this.activeSubMenuIndex === index ? -1 : index;
  if (this.menuItems[index].submenu.includes('Opinion Articles')) {
    this.$emit('opinionArticlesClicked');
  }
    },
    checkMobile() {
      this.isMobile = window.innerWidth < 768;
    },  handleSubmenuClick(subItemName) {
    if (subItemName === 'Opinion Articles') {
      this.$emit('opinionArticlesClicked');
    }
  }
    
  }
}
</script>

<style scoped>
.top-bar {
  display: flex;
  justify-content: end;
  flex-flow: wrap;
  background-color: #FFFFFF;
  width: 100%;
  align-items: center;
  flex-flow: row-reverse;
  flex-flow: wrap;
}
.name {
  font-size: 12px;
  text-align: left;
}
.container-submenu {
  display: flex;
}
.menu-level-1 {
  display: flex;
  list-style-type: none;
  margin: 0;
  padding: 0;
  justify-content: end;
  flex-wrap: wrap;
  width: 100%;
}
.submenu {
  list-style-type: none;
  padding: 0;
  margin-top: -9px;
  text-align: left;
  margin-bottom: -40px;
}
.related-content {
  display: flex;
  width: 100%;
  align-items: flex-start;
  background-color: #F2F2F2;
  height: 436px;
  align-items: center;
  position: absolute;
  z-index: 999;
  left: 0;
}
.active {
  border-bottom: 8px solid #3346AA;
}
.content-wrapper {
  display: flex;
  margin-left: 20%;
  align-items: center;
  width: 67%;
}
.detail-section {
  display: flex;
  background: white;
  color: #333;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.3);
  border-radius: 17px;
  margin-right: 24px;
  height: 100%;
}
.detail-image {
  width: 150px;
  border-radius: 16px 0px 0px 16px;
}
.detail-text {
  width: 70%;
  font-size: 20px;
  padding: 30px;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
  text-align: left;
}
.case-study-label {
  border-radius: 12px;
  display: flex;
  align-items: center;
  padding: 0px 8px;
  border: 1px solid;
  font-size: 12px;
  margin-top: 16px;
}
.info-section {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.info-box {
  background: white;
  color: #333;
  width: 100%;
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
  margin-bottom: 16px;
  height: 100%;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.3);
  border-radius: 17px;
  margin-right: 24px;
  height: 100%;
}
.info-box-second {
  background: white;
  color: #333;
  box-shadow: 2px 2px 2px rgba(0, 0, 0, 0.3);
  width: 100%;
  display: flex;
  flex-flow: nowrap;
  padding: 1rem;
  margin-bottom: 0px;
  border-radius: 17px;
  margin-right: 24px;
  height: 100%;
}
li {
  padding: 10px;
  cursor: pointer;
  font-family: 'Ubuntu', sans-serif;
  font-size: 20px;
}
.hamburger {
  display: none;
  background: black;
  border: none;
  font-size: 30px;
  color: white;
}
/*podia ter ficado melhor mas por norma o design que recebo ja tem mobile*/
@media (max-width: 768px) {
  .hamburger {
    display: block;
  }
  .menu-level-1[v-show="menuVisible"] {
    flex-direction: column;
    align-items: center;
    width: 100%;
  }
  .title-wrapper {
    width: 100%;
  }
  .related-content {
    height: 100%;
  }
  .content-wrapper {
    flex-wrap: wrap;
    height: fit-content;
    margin-top: 8%;
    width: 89%;
    display: flex;
    align-self: self-end;
    margin-left: 0;
  }
  .detail-image {
    height: 120px;
  }
  .detail-text {
    font-size: 15px;
    padding: 9px;
  }
  .info-box {
    font-size: 12px;
    padding: 0.5rem;
    width: 95%;
  }
  .container-submenu {
    flex-wrap: wrap;
    flex-direction: column;
  }
  .submenu {
    margin-top: -40%;
    display: flex;
    flex-wrap: wrap;
  }
  .detail-section {
    margin-bottom: 16px;
  }
  .info-box-second {
    width: 95%;
  }
}
</style>
