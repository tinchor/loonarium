<template>
<modal name="register-modal" transition="pop-out" :width="modalWidth" :height="400">
  <div class="box">
    <div class="box-part" id="bp-left">
      <div class="partition" id="partition-register">
        <div class="partition-title">Register to leave notes!</div>
        <div class="partition-form">
          <form autocomplete="false">

            <div class="autocomplete-fix">
              <input type="password">
            </div>

            <input id="n-username" v-model="username" type="text" placeholder="Username">
            <input id="n-password" v-model="password" type="password" placeholder="Password (8+ chars)">
            <input id="n-password2" v-model="password2" type="password" placeholder="Password again">
            <div style="margin-top: 42px">
            </div>

            <div class="button-set">
              <button class="center-block btn" type="submit" id="goto-signin-btn" @click.prevent="register">Register</button>
            </div>
          </form>
        </div>
        <div class="partition-text">
          <p>15 characters or less</p>
          <p>Fields accept alphanumeric and underscore characters only: A~Z a~z 0~9 _</p>
        </div>
      </div>
    </div>
    <div class="box-part" id="bp-right">
      <div class="box-messages">
      </div>
    </div>
  </div>
</modal>
</template>
<script>
// from https://github.com/euvl/vue-js-modal/blob/master/demo/client_side_rendering/src/components/modals/DemoLoginModal.vue
const MODAL_WIDTH = 320
export default {
  name: 'RegisterModal',
  data () {
    return {
      modalWidth: MODAL_WIDTH,
      username: '',
      password: '',
      password2: ''
    }
  },
  methods: {
    register () {
      const data = {
        username: this.username,
        password: this.password,
        passwordVerif: this.password2,
        hideFn: this.$modal.hide,
        onError: this.onError,
        onSuccess: this.onSuccess
      }
      this.$store.dispatch('auth/register', data)
    },
    onError (title, text) {
      this.$notify({
        group: 'base',
        type: 'error',
        title,
        text,
      })
    },
    onSuccess (title, text) {
      this.$notify({
        group: 'base',
        type: 'success',
        title,
        text,
      })
    }
  },
  created () {
    this.modalWidth = Math.min(window.innerWidth, MODAL_WIDTH)
  }
}
</script>
<style lang="scss">
$background_color: #404142;
.box {
  background: white;
  overflow: hidden;
  width: 656px;
  height: 400px;
  border-radius: 2px;
  box-sizing: border-box;
  box-shadow: 0 0 40px black;
  color: #8b8c8d;
  font-size: 0;
  .box-part {
    display: inline-block;
    position: relative;
    vertical-align: top;
    box-sizing: border-box;
    height: 100%;
    width: 50%;
    &#bp-right {
      background: url("/static/panorama.jpg") no-repeat top left;
      border-left: 1px solid #eee;
    }
  }
  .box-messages {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
  }
  .box-error-message {
    position: relative;
    overflow: hidden;
    box-sizing: border-box;
    height: 0;
    line-height: 32px;
    padding: 0 12px;
    text-align: center;
    width: 100%;
    font-size: 11px;
    color: white;
    background: #F38181;
  }
  .partition {
    width: 100%;
    height: 100%;
    .partition-title {
      box-sizing: border-box;
      padding: 30px;
      width: 100%;
      text-align: center;
      letter-spacing: 1px;
      font-size: 20px;
      font-weight: 300;
    }
    .partition-form {
      padding: 0 20px;
      box-sizing: border-box;
    }
    .partition-text {
      box-sizing: border-box;
      padding: 5px 20px;
      width: 100%;
      text-align: center;
      font-size: 14px;
    }
  }
  input[type=password],
  input[type=text] {
    display: block;
    box-sizing: border-box;
    margin-bottom: 4px;
    width: 100%;
    font-size: 12px;
    line-height: 2;
    border: 0;
    border-bottom: 1px solid #DDDEDF;
    padding: 4px 8px;
    font-family: inherit;
    transition: 0.5s all;
    outline: none;
  }
  button {
    background: white;
    border-radius: 4px;
    box-sizing: border-box;
    padding: 10px;
    letter-spacing: 1px;
    font-family: "Open Sans", sans-serif;
    font-weight: 400;
    min-width: 140px;
    margin-top: 8px;
    color: #8b8c8d;
    cursor: pointer;
    border: 1px solid #DDDEDF;
    text-transform: uppercase;
    transition: 0.1s all;
    font-size: 10px;
    outline: none;
    &:hover {
      border-color: mix(#DDDEDF, black, 90%);
      color: mix(#8b8c8d, black, 80%);
    }
  }
  .large-btn {
    width: 100%;
    background: white;
    span {
      font-weight: 600;
    }
    &:hover {
      color: white !important;
    }
  }
  .button-set {
    margin-bottom: 8px;
  }
  #register-btn,
  #signin-btn {
    margin-left: 8px;
  }
  .autocomplete-fix {
    position: absolute;
    visibility: hidden;
    overflow: hidden;
    opacity: 0;
    width: 0;
    height: 0;
    left: 0;
    top: 0;
  }
}
.pop-out-enter-active,
.pop-out-leave-active {
  transition: all 0.5s;
}
.pop-out-enter,
.pop-out-leave-active {
  opacity: 0;
  transform: translateY(24px);
}
</style>