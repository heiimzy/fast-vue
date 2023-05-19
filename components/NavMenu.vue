<template>
  <nav>
    <ul>
      <li v-for="(subMenu, menuItem) in data" :key="menuItem">
        <div 
          class="parent-item"
          @click="toggleSubMenu(menuItem)"
        >
          {{ menuItem }}
          <span v-if="Object.keys(subMenu).length > 0">
            <i :class="[{'fa-angle-up': subMenuVisible[menuItem], 'fa-angle-down': !subMenuVisible[menuItem]}, 'fa', 'icon']"></i>
          </span>
        </div>
        <ul v-show="subMenuVisible[menuItem]">
          <li v-for="option in subMenu" :key="option">{{ option }}</li>
        </ul>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: "NavMenu",
  props: {
    data: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      subMenuVisible: {}
    };
  },
  methods: {
    toggleSubMenu(menuItem) {
      this.subMenuVisible = {
        ...this.subMenuVisible,
        [menuItem]: !this.subMenuVisible[menuItem]
      };
    }
  }
};
</script>

<style>
.parent-item {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.icon {
  margin-left: auto;
}

.fa {
  font-size: 18px;
}

.fa-angle-down {
  transform: rotate(-90deg);
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

li {
  margin-top: 5px;
}
</style>