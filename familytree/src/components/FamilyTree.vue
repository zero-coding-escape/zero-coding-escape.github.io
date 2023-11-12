<template>
  <div id="tree" ref="tree"></div>
</template>

<script>

import FamilyTree from '@balkangraph/familytree.js'
import myFamily from '../assets/myFamily.json'

export default {

  name: 'tree',
  data() {
    return {
      // nodes: [
      //   { id: 1, pids: [2], name: "Amber McKenzie", gender: "female", img: "https://cdn.balkan.app/shared/2.jpg" },
      //   { id: 2, pids: [1], name: "Ava Field", gender: "male", img: "https://cdn.balkan.app/shared/m30/5.jpg" },
      //   { id: 3, mid: 1, fid: 2, name: "Peter Stevens", gender: "male", img: "https://cdn.balkan.app/shared/m10/2.jpg" },
      //   { id: 4, mid: 1, fid: 2, name: "Savin Stevens", gender: "male", img: "https://cdn.balkan.app/shared/m10/1.jpg" },
      //   { id: 5, mid: 1, fid: 2, name: "Emma Stevens", gender: "female", img: "https://cdn.balkan.app/shared/w10/3.jpg" },
      // ]
      nodes: []
    }
  },

  methods: {
    mytree: function (domEl, x) {
      this.family = new FamilyTree(domEl, {
        nodes: x,
        nodeBinding: {
          field_0: "name",
          img_0: "img"
        },
        miniMap: true,
        enableSearch: false,
        mouseScrool: FamilyTree.action.ctrlZoom,
      });
    }
  },

  mounted() {
    for (let i = 50; i < myFamily.length; i++) {
      const id = myFamily[i].ID;
      const name = myFamily[i]['Full name'];
      const pids = [2];
      const gender = myFamily[i].Gender;
      const img = '';
      const fid = myFamily[i]['Father ID'];
      const mid = myFamily[i]['Mother ID'];
      this.nodes.push({ id: id, fid: fid, mid: mid, name: name, pids: pids, gender: gender, img: img })
    }
    console.log("tree: ", this.nodes.length);
    this.mytree(this.$refs.tree, this.nodes)

  }
}
</script>

<style scoped></style>
