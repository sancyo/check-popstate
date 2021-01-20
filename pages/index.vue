<template>
  <div class="container">
    <div class="button-1" @click="openModal()">open modal</div>
    <div v-if="isActive" class="modal">
      <div class="close-btn" @click="closeModal()">閉じる</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isActive: false,
    }
  },
  beforeMount() {
    window.addEventListener(
      'popstate',
      (e) => {
        console.log(e.state)
      },
      { once: true }
    )
  },
  methods: {
    back() {
      history.back()
    },
    openModal() {
      history.pushState('open', null, `/page1`)
      this.isActive = true
    },
    closeModal() {
      history.replaceState('close', null, `/`)
      this.isActive = false
    },
  },
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.button-1 {
  display: inline-block;
  padding: 0.4em 1.6em;
  font-size: 0.8em;
  color: #00b5ad;
  text-decoration: none;
  user-select: none;
  border: 1px #00b5ad solid;
  border-radius: 3px;
  transition: 0.2s ease;
  cursor: pointer;
  background: #fff;
  margin: 0 30px;
}

.button-1:hover {
  color: #fff;
  background: #00b5ad;
}
.modal {
  position: fixed;
  top: 0;
  left: 0;
  background: #323232;
  color: #fff;
  width: 100vw;
  height: 100vh;
  text-align: center;
  line-height: 100px;
  border-radius: 8px;
  opacity: 0.5;
}

.close-btn {
  cursor: pointer;
}
</style>
