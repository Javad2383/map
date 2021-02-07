<template>
  <div id="sidebar">
    <!-- -------------------- Toggle Button ------------------ -->
    <button v-on:click="SidebarMethod" class="btn btn-sidebar">&rightleftarrows;</button>
    <!-- -------------------- Location List ------------------ -->
    <div class="location-list">
      <div class="location-list-item" v-for="item in LocationList" :key="item.id">
        <h2 class="text-center">{{ item.title }}</h2>
        <button class="btn btn-info mt-3 w-100" v-on:click="ShowInMap(item)">mark in map</button>
      </div>
    </div>
    <!-- -------------------- Add Section ------------------ -->
    <div class="add-section">
      <!-- ------ Title ------ -->
      <label for="Sidebar_add_title">Title</label>
      <input type="text" class="form-control" id="Sidebar_add_title" placeholder="title" v-model="Location.title">
      <!-- ------ X ------ -->
      <label for="Sidebar_add_x" class="mt-2">X</label>
      <input type="number" class="form-control" id="Sidebar_add_x" placeholder="x" v-model="Location.x">
      <!-- ------ Y ------ -->
      <label for="Sidebar_add_y" class="mt-2">Y</label>
      <input type="number" class="form-control" id="Sidebar_add_y" placeholder="y" v-model="Location.y">
      <!-- ------ Submit ------ -->
      <button class="btn btn-success w-100 mt-4" v-on:click="AddLocationItem">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Sidebar",
  data() {
    return {
      isOpenSidebar: false,
      Location: {id: 1, title: '', x: 0, y: 0},
      LocationList: this.$store.state.LocationList,
    }
  },
  methods: {
    // Open & Close Sidebar Method
    SidebarMethod() {
      if (this.isOpenSidebar === true) {
        this.isOpenSidebar = false;
        document.getElementById("sidebar").style.transform = "translateX(100%)";
      } else {
        this.isOpenSidebar = true;
        document.getElementById("sidebar").style.transform = "translateX(0)";
      }
    },
    // Add a Item to Location List
    AddLocationItem() {
      let LastId = this.Location.id;
      this.$store.state.LocationList.push(this.Location);
      this.Location = {id: LastId + 1, title: '', x: 0, y: 0};
    },
    // Add a Item to Location List For Show In Map
    ShowInMap(item) {
      return this.$store.state.ShowList.push(item);
    }
  }
}
</script>

<style scoped>
#sidebar {
  position: fixed;
  height: 100%;
  width: 30%;
  z-index: 3;
  background: #ffffff;
  top: 0;
  right: 0;
  transition: all .3s;
  -webkit-transition: all .3s;
  -moz-transition: all .3s;
  -o-transition: all .3s;
  transform: translateX(100%);
  -webkit-transform: translateX(100%);
  -moz-transform: translateX(100%);
  -o-transform: translateX(100%);
}

.btn-sidebar {
  position: absolute;
  background: #ffffff;
  width: 40px;
  top: 20px;
  left: -30px;
}

.add-section {
  padding: 20px;
  position: fixed;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 300px;
  border-top: 1px solid rgba(0, 0, 0, .2);
  z-index: 23;
  box-shadow: 5px 0 20px rgba(0, 0, 0, .07);
}

.location-list {
  overflow-x: hidden;
  overflow-y: scroll;
  height: calc(100% - 300px);
  width: 100%;
  position: fixed;
  top: 0;
  right: 0;
  padding: 20px;
  text-align: left;
}

.location-list-item {
  width: 100%;
  padding: 20px;
  border-bottom: 1px solid rgba(0, 0, 0, .2);
}

@media (max-width: 766px) {
  #sidebar {
    width: 70%;
  }
}
</style>