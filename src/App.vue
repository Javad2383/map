<template>
  <div id="app">
    <!-- -------------------- Sidebar ------------------ -->
    <sidebar></sidebar>
    <div class="map-parent">
      <!-- -------------------- Map ------------------ -->
      <mapir :center="center" :apiKey="apiKey">
        <mapNavigationControl position="top-left"/>
        <!-- -------------------- Marked Items ------------------ -->
        <div v-for="item in ShowList" :key="item.id">
          <mapPopup :closeOnClick="false" :coordinates="[item.x, item.y]" anchor="bottom"
                    :showed="true">
            <span>{{ item.title }}</span>
          </mapPopup>
        </div>
      </mapir>
    </div>
  </div>
</template>

<script>
import {mapir, mapNavigationControl, mapPopup} from "mapir-vue";
import sidebar from './components/Sidebar';

export default {
  name: "App",
  components: {
    mapir,
    mapNavigationControl,
    mapPopup,
    sidebar
  },
  data() {
    return {
      apiKey: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6ImU0NmRhOWZhNDE5YTMzOWJiYzdjMzRlMjQ2MDAyMWMzZWYzOWNhNGZmZTQxNjQwYzJkZTQyZjQ3NzdlMWM3ZDQ2ZWUzMDYxNzkxZTM0NTdhIn0.eyJhdWQiOiIxMjY4NyIsImp0aSI6ImU0NmRhOWZhNDE5YTMzOWJiYzdjMzRlMjQ2MDAyMWMzZWYzOWNhNGZmZTQxNjQwYzJkZTQyZjQ3NzdlMWM3ZDQ2ZWUzMDYxNzkxZTM0NTdhIiwiaWF0IjoxNjEyNjMyOTQxLCJuYmYiOjE2MTI2MzI5NDEsImV4cCI6MTYxNTEzODU0MSwic3ViIjoiIiwic2NvcGVzIjpbImJhc2ljIl19.r2f0NQhJTE2oIeJ3l_8BDCmampTb09BTWsyHTo1c-8gg7eEd1k7xT5hl5PoGoEaeg2USNIVi5y9nrgomy9omIDjpAj4qR40SdRDSf_-KwKcgzZr184skhw5rt1KcK6SSzf-2-jW-QIR03Y964lIafEAk8qp_rHwO31RryjZUwJQ7V3MpgXPqg9_I-4e2vrlBiSGeKpmLUvvcuwqYVMJYiYw6iiSo1nCfLFzSA02tG3yfLILjaFte9vrWRUBKzH9H1FPgoKQp8SApWi5riDtHzRfUFHryo8pTjv9531HDfzN1LNjP51nq97R62ACcekPCesJyOXFNTJwW1shfHTz0EQ',
      center: [59.3645, 36.1700],
      ShowList: this.$store.state.ShowList,
    };
  }
};
</script>
<style>
body {
  direction: rtl !important;
  overflow: hidden;
}

::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  background: #fafafa;
}

::-webkit-scrollbar-thumb {
  background: #c8c8c8;
}

::-webkit-scrollbar-thumb:hover {
  background: #8f8f8f;
}

.form-control:focus, .btn:focus, .btn {
  box-shadow: none !important;
  outline: none !important;
}

.map-parent {
  width: 100%;
  height: 100vh;
}
</style>