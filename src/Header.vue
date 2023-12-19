<template>
  <div class="sc-header"
  :class="[{'sc-header-full':fullWin}]"
   :style="{background: colors.header.bg, color: colors.header.text}">
    <slot>
      <img v-if="titleImageUrl" class="sc-header--img" :src="titleImageUrl" alt="" />
      <div v-if="!disableUserListToggle" class="sc-header--title enabled" @click="toggleUserList">
        {{ title }}
      </div>
      <div v-else class="sc-header--title">{{ title }}</div>
    </slot>
    <div v-if="showfullButton && !isMobile" class="sc-header--close-button" @click="$emit('full')">
      <img :src="icons.maxIcon.img" v-if="!fullWin" :alt="icons.maxIcon.name" />
      <img :src="icons.minIcon.img" v-else :alt="icons.minIcon.name" />
    </div>
    <div v-if="showCloseButton" class="sc-header--close-button m-r-14" @click="$emit('close')">
      <img :src="icons.close.img" class="close" :alt="icons.close.name" />
    </div>
  </div>
</template>

<script>
import {mapState} from './store/'
import CloseIcon from './assets/ic_close.svg'
import maxIcon from './assets/ic_max.svg'
import minIcon from './assets/ic_min.svg'

export default {
  props: {
    icons: {
      type: Object,
      default: function () {
        return {
          close: {
            img: CloseIcon,
            name: 'default'
          },
          maxIcon:{

            img: maxIcon,
            name: 'maxIcon'
          },
          minIcon:{
            img: minIcon,
            name: 'minIcon'
          }
        }
      }
    },
    title: {
      type: String,
      required: true
    },
    colors: {
      type: Object,
      required: true
    },
    fullWin: {
      type: Boolean,
      default:false,
      required: true
    },
  },
  data() {
    return {
      inUserList: false
    }
  },
  computed: {
    ...mapState(['disableUserListToggle', 'titleImageUrl', 'showCloseButton', 'showfullButton']),
    isMobile(){
       const userAgent = navigator.userAgent;

    // 正则表达式测试是否为移动设备
    if (/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(userAgent)) {
        return true;
    }

    // 否则，认为是PC端
    return false;
    }
  },
  methods: {
    toggleUserList() {
      this.inUserList = !this.inUserList
      this.$emit('userList', this.inUserList)
    }
  }
}
</script>

<style scoped>
.sc-header {
  min-height: 60px;
  padding: 0;
  border-top-left-radius: 9px;
  border-top-right-radius: 9px;
  box-shadow: 0 1px 4px rgba(0, 0, 0, 0.2);
  position: relative;
  box-sizing: border-box;
  display: flex;
}
.sc-header-full{
  border-top-left-radius: 0px;
  border-top-right-radius: 0px;
}
.m-r-14{
  margin-right: 14px;
}
.sc-header--img {
  border-radius: 50%;
  align-self: center;
  padding: 10px;
}

.sc-header--title {
  align-self: center;
  padding: 10px;
  flex: 1;
  user-select: none;
  font-size: 20px;
}

.sc-header--title.enabled {
  cursor: pointer;
  border-radius: 5px;
}

.sc-header--title.enabled:hover {
  box-shadow: 0px 2px 5px rgba(0.2, 0.2, 0.5, 0.1);
}

.sc-header--close-button {
  width: 30px;
  align-self: center;
  height: 30px;
  box-sizing: border-box;
  cursor: pointer;
  border-radius: 5px;
  margin-left: auto;
  margin-right: 10px;
}

.sc-header--close-button:hover {
  box-shadow: 0px 2px 5px rgba(0.2, 0.2, 0.5, 0.1);
}

.sc-header--close-button img {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  font-weight: bold;
    padding: 5px;
}


@media (max-width: 450px) {
  .sc-header {
    border-radius: 0px;
  }
}
</style>
