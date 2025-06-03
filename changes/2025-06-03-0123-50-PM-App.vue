<template lang="pug">
#app
  p Drag points (in blue) and see how their Tverberg points (in green) move.
  label r 
  select(v-model.number="r")
    option 2
    option 3
  |  &middot; 
  label mode 
  select(v-model="mode")
    option 3r-2
    option 3r
  #canvas(
    @mousemove="onDrag" @touchmove="onDrag"
    @mouseup="stopDrag" @touchend="stopDrag" @mouseleave="stopDrag"
  )
    point(
      v-for="(point, i) in points"
      v-bind:x="point.x"
      v-bind:y="point.y"
      v-bind:i="i"
      v-bind:key="i"
      v-bind:tverberg="false"
      @startDrag="startDrag($event, i)"
    )
    point(
      v-for="(point, i) in tverbergPoints"
      v-bind:x="point.x"
      v-bind:y="point.y"
      v-bind:i="i"
      v-bind:tverberg="true"
      v-bind:key="i"
    )
    svg
      poly(
        v-for="(polygon, i) in tverbergSet"
        v-bind:coordinates="polygon"
        v-bind:key="i"
      )
    svg
      poly(
        v-for="(polygon, i) in convexHulls"
        v-bind:coordinates="polygon"
        v-bind:outline="true"
        v-bind:key="i"
      )
</template>

<script>
import convexhull from 'convexhull-js';
... (truncated for brevity)