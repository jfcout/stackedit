<template>
  <modal-inner aria-label="Insert link">
    <div class="modal__content">
      <p>Please provide a <b>URL</b> for your link.</p>
      <form-entry label="URL" error="url">
        <input slot="field" class="textfield" type="text" v-model.trim="url" @keyup.enter="resolve()">
      </form-entry>
    </div>
    <div class="modal__button-bar">
      <button class="button" @click="reject()">Cancel</button>
      <button class="button" @click="resolve()">Ok</button>
    </div>
  </modal-inner>
</template>

<script>
import modalTemplate from './common/modalTemplate';

export default modalTemplate({
  data: () => ({
    url: '',
  }),
  methods: {
    resolve() {
      if (!this.url) {
        this.setError('url');
      } else {
        const callback = this.config.callback;
        this.config.resolve();
        callback(this.url);
      }
    },
    reject() {
      const callback = this.config.callback;
      this.config.reject();
      callback(null);
    },
  },
});
</script>
