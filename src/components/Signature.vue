<template>
  <div class="container">
    <h2>Create a Signature</h2>
    <h3>Use one of the following ways to create your signature.</h3>

    <div class="tabs">
      <button
        @click="handleTab('type')"
        class="tab-item"
        v-bind:class="{ active: isActive('type') }"
      >Type</button>
      <button
        @click="handleTab('upload')"
        class="tab-item"
        v-bind:class="{ active: isActive('upload') }"
      >Upload</button>
      <button
        @click="handleTab('draw')"
        class="tab-item"
        v-bind:class="{ active: isActive('draw') }"
      >Draw</button>
    </div>

    <div class="content">
      <div v-show="isActive('type')" class="tab-content">
        <input
          ref="signatureInput"
          type="text"
          class="signature-input"
          spellCheck="false"
          autoFocus
        />
      </div>
      <div v-show="isActive('upload')" class="tab-content">
        <input
          ref="signatureFile"
          type="file"
          @change="handleFileChange"
          accept="image/x-png,image/gif,image/jpeg"
        />
        <div class="preview" v-if="previewImg">
          <img :src="previewImg" />
        </div>
      </div>
      <div v-show="isActive('draw')" class="tab-content">
        <canvas
          ref="signaturePad"
          width="500"
          height="250"
        />
      </div>
    </div>

    <div class="actions">
      <button
        type="button"
        @click="handleClear()"
      >Clear</button>
      <button
        type="button"
        @click="handleSubmit()"
      >Submit</button>
    </div>
  </div>
</template>

<script>
import SignaturePad from 'signature_pad'

export default {
  name: 'Signature',
  data: function () {
    return {
      currentTab: 'type',
      previewImg: null,
      signaturePad: null,
    }
  },
  async mounted() {
    this.signaturePad = new SignaturePad(this.$refs.signaturePad)
  },
  methods: {
    isActive(tab) {
      return this.currentTab === tab
    },
    handleTab(tab) {
      this.currentTab = tab
    },
    handleFileChange(e) {
      const file = e.target.files[0]
      this.previewImg = URL.createObjectURL(file)
    },
    handleClear() {
      switch (this.currentTab) {
        case 'upload':
          this.$refs.signatureFile.value = ''
          this.previewImg = null
          break;
        case 'draw':
          if (this.signaturePad)
            this.signaturePad.clear()
          break;
        case 'type':
          this.$refs.signatureInput.value = ''
          break;
      }
    },
    handleSubmit() {
      alert('Coming soon')
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Gochi+Hand&display=swap");

.container {
  max-width: 500px;
  margin: 0 auto;
}
h2 {
  color: deepskyblue;
  margin: 5px;
}
h3 {
  color: gray;
  font-weight: 400;
  margin: 0 0 15px;
}
.tab-content {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 250px;
}
.tabs {
  border-bottom: 1px solid deepskyblue;
}
.tab-item {
  display: inline-block;
  background-color: transparent;
  font-family: Times New Roman, sans-serif;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  padding: 10px 16px;
  margin: 0;
  border: none;
  outline: none;
}
.tab-item.active {
  color: deepskyblue;
  border-bottom: 2px solid deepskyblue;
}
.content {
  -webkit-box-shadow: inset 0 -8px 8px -4px rgba(0, 0, 0, 0.2);
  -moz-box-shadow: inset 0 -8px 8px -4px rgba(0, 0, 0, 0.2);
  box-shadow: inset 0 -8px 8px -4px rgba(0, 0, 0, 0.2);
}
.signature-input {
  font-family: 'Gochi Hand', sans-serif;
  line-height: 1.7;
  font-size: 48px;
  outline: none;
  border: none;
  border-bottom: 2px solid lightgrey;
  width: 100%;
  margin: 0 30px;
}
.preview {
  padding: 12px;
}
.preview img {
  max-width: 160px;
}
.actions {
  margin-top: 10px;
}
.actions button {
  margin: 0 5px;
}
</style>
