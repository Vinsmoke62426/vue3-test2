<template>
  <div class="test-one">
    <div class="content">
      <div class="grandparent">
        <div class="parent">
          <div class="child" @click="startEvevt(false)">事件冒泡</div>
        </div>
      </div>
    </div>
    <div class="content">
      <div class="grandparent">
        <div class="parent">
          <div class="child" @click="startEvevt(true)">事件捕获</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { computed } from 'vue'
export default {
  setup() {

    const addEvent = (el: any, event: any, callback: any, isCapture: boolean = false) => {
      if (!el || !event || !callback || typeof callback !== "function") {
        return
      }
      if (typeof el === "string") {
        el = document.querySelector(el)
      }
      el.addEventListener(event, callback, isCapture)
    }

    const startEvevt = (isCapture: boolean = false) => {
      console.log(isCapture)
      const child = document.querySelector(".child");
      const parent = document.querySelector(".parent");
      const grandparent = document.querySelector(".grandparent");

      addEvent(
        child, 
        "click", 
        (e: any) => {
          console.log("child")
        },
        isCapture
      );

      addEvent(parent, "click", (e: any) => {
        console.log("parent");
      }, isCapture);

      addEvent(grandparent, "click", (e: any) => {
        console.log("grandparent");
      }, isCapture);

      addEvent(document, "click", (e: any) => {
        console.log("document");
      }, isCapture);

      addEvent("html", "click", (e: any) => {
        console.log("html");
      }, isCapture);

      addEvent(window, "click", (e: any) => {
        console.log("window");
      }, isCapture);
    }
    return {
      startEvevt
    }
  }
}
</script>

<style scoped lang="scss">
.test-one {
  display: flex;
  justify-content: center;
  .content{
    width: 20%;
    .child{
      cursor: pointer;
    }
  }
}
</style>
