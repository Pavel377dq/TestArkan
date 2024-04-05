<template>
  <div class="wrap">
    <ul>
      <li v-for="item in innerListTop">{{ item }}</li>
    </ul>

    <div>
      <button @click="upAll">all top</button>
      <button @click="upOneTop">one top</button>
      <button @click="downAll">all down</button>
      <button @click="downOneTop">one down</button>
    </div>
    <ul>
      <li v-for="item in innerListMiddle">{{ item }}</li>
    </ul>
    <div>
      <button @click="upOneBottom">one top</button>
      <button @click="downOneBottom">one bottom</button>
    </div>
    <ul>
      <li v-for="item in innerListBottom">{{ item }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'AgileList',
  data() {
    return {
      innerListTop: [],
      innerListMiddle: [],
      innerListBottom: []
    }
  },
 mounted() {
  fetch('data.json')
    .then(res => res.json())
    .then(data=> {this.innerListTop = data.list});
  
 // console.log(res);
},
  methods: {
    upOneTop() {
      if (this.innerListMiddle.length) {
        this.innerListTop.push(this.innerListMiddle.pop())
      }
    },
    downOneTop() {
      if (this.innerListTop.length) {
        this.innerListMiddle.push(this.innerListTop.pop())
      }
    },
    upAll() {
      if (this.innerListMiddle.length) {

        this.innerListTop = [...this.innerListTop, ...this.innerListMiddle];

        this.innerListMiddle = [];
      }
    },
    downAll() {
      if (this.innerListTop.length) {
        this.innerListMiddle = [...this.innerListMiddle, ...this.innerListTop];
        this.innerListTop = [];
      }
    },
    upOneBottom() {
      if (this.innerListBottom.length) {
        this.innerListMiddle.push(this.innerListBottom.pop());
      }
    },
    downOneBottom() {
      if (this.innerListMiddle.length) {
        this.innerListBottom.push(this.innerListMiddle.pop());
      }
    }
  }
}
</script>
