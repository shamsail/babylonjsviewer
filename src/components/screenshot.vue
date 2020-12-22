<template>
  <v-content
    class="ma-0 pa-0"
    style="width: 100%; height: 100vh; min-height: 100vh; position: relative"
  >
    <babylon
      style="width: 100%; height: 100%; background-color: transparent"
      id="loading-demo"
      :model="file"
      templates.viewer.params.enable-drag-and-drop="true"
      templates.nav-bar.params.hide-logo="true"
      templates.nav-bar.params.hide-hd="false"
      templates.nav-bar.params.hide-vr="false"
      templates.main.params.fill-screen="true"
      templates.loading-screen.params.background-color="#c3c3c3"
      templates.loading-screen.params.loading-image="null"
      templates.loading-screen.params.static-loading-image=""
      camera.behaviors.auto-rotate="0"
      skybox="false"
      ground="false"
      templates.nav-bar.params.disable-on-fullscreen="true"
    >
    </babylon>

    <button @click="seeInspector()">Inspector</button>
    <button @click="screenShot()">ScreenShot</button>

    <!-- <v-btn
      icon
      class="ml-7 mb-3"
      style="position: absolute; left: 0; bottom: 0; z-index: 100000000"
      ><md-icon
        class="md-size-2x"
        md-src="../assets/svg/editorOpen.svg"
      ></md-icon
    ></v-btn>
    <v-btn
      icon
      @click="screenShot()"
      class="ml-13 mb-3"
      style="position: absolute; left: 5%; bottom: 0; z-index: 100000000"
      ><v-icon>mdi-magnify</v-icon></v-btn
    > -->

    <div
      id="mydiv"
      style="
        position: absolute;
        top: 0;
        right: 0;
        z-index: 1000000;
        height: 90%;
      "
    ></div>
  </v-content>
</template>
<script>
import * as BabylonViewer from "@babylonjs/viewer";

import "@babylonjs/loaders/glTF";

import { Tools } from "@babylonjs/core/Misc";

export default {
  name: "editor",
  components: {},

  data: function () {
    return {
      file: "../assets/images/Astronaut.glb",
    };
  },

  mounted() {
    if (localStorage.getItem("reloaded")) {
      localStorage.removeItem("reloaded");
    } else {
      localStorage.setItem("reloaded", "1");
      this.$router.go();
    }
  },
  methods: {
    screenShot() {
      BabylonViewer.viewerManager
        .getViewerPromiseById("loading-demo")
        .then(function (viewer) {
          if (viewer.sceneManager.scene.activeCamera) {
            Tools.CreateScreenshotUsingRenderTarget(
              viewer.sceneManager.scene.getEngine(),
              viewer.sceneManager.scene.activeCamera,
              { width: 600, height: 400 }
            );
          }
        });

      //   BabylonViewer.viewerManager
      //     .getViewerPromiseById("loading-demo")
      //     .then(function (viewer) {
      //       if (viewer.sceneManager.scene.activeCamera) {
      //         Tools.CreateScreenshot(
      //           viewer.sceneManager.scene.getEngine(),
      //           viewer.sceneManager.scene.activeCamera,
      //           { width: 600, height: 400 }
      //         );
      //       }
      //     });
    },

    seeInspector() {
      this.editorDiv = !this.editorDiv;
      if (this.editorDiv === true) {
        BabylonViewer.viewerManager
          .getViewerPromiseById("loading-demo")
          .then(function (viewer) {
            viewer.sceneManager.scene.debugLayer.show({
              overlay: false,
              globalRoot: document.getElementById("mydiv"),
              embedMode: true,
            });
          });
      } else {
        BabylonViewer.viewerManager
          .getViewerPromiseById("loading-demo")
          .then(function (viewer) {
            viewer.sceneManager.scene.debugLayer.hide();
          });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
</style>