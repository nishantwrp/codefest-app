<template>
  <div :class="$style.root">
    <AppBar/>
    <main :class="$style.wrapper">
      <div :class="$style.authContainer">
        <TabLayout :tabs="tabs">
          <div :class="$style.formContainer" slot="Forgot Password">
            <form :class="$style.form" @submit.prevent="forgot_password">
              <div :class="$style.fieldContainer">
                <label for="email" :class="$style.label">Email</label>
                <input type="email" :class="$style.field" v-model="email">
                <div id="message">
                  {{message}}
                </div>

              </div>
              <div :class="$style.btnStyle">
                <button value="<" :class="$style.submit">
                  <i class="fas fa-arrow-circle-left"></i>
                </button>
                <button value=">" :class="$style.submit">
                  <i class="fas fa-arrow-circle-right"></i>
                </button>
              </div>
            </form>
          </div>
        </TabLayout>
      </div>
    </main>
    <Footer/>
  </div>
</template>

<script>
import AppBar from "@components/Menu/AppBar";
import Footer from "@components/Footer";
import TabLayout from "@components/layouts/TabLayout";
import firebase from "firebase";

export default {
  components: {
    AppBar,
    Footer,
    TabLayout
  },
  data() {
    return {
      email: "",
      password: "",
      message:null,
      tabs: [
        {
          name: "Forgot Password",
          title: "Forgot Password"
        }
      ]
    };
  },
  methods: {
    forgot_password() {
      firebase
        .auth()
        .sendPasswordResetEmail(this.email)
        .then(user => {
          this.message="The reset password link has been sent to your email.Please check the inbox!!."          
        })
        .catch(err => {
          this.message="There is no user with such an user-name."
        });
    }
  }
};
</script>
<style module lang="stylus">
@require '~@styles/theme';
@require '~@styles/anims';

.authContainer {
  font-size: 16px;
  font-family: courier, monospace;
  max-width: 800px;
  margin: auto;
  width: 100%;
}

.wrapper {
  width: 80%;
  margin: 0 auto;
  padding: 200px 0;
  position: relative;
  top: 0;
  z-index: 1;
  font-family: 'Roboto Mono';
  font-size: 18px;
}

.root {
  height: 100vh;
}

.form {
  margin: 50px;
}

.fieldContainer {
  width: 100%;
  margin-bottom: 20px;
  text-align: right;
}

.field {
  clear: both;
  height: 30px;
  color: white;
  border: 0;
  outline: 0;
  max-width: 600px;
  width: 100%;
  font-size: 16px;
  background: #fff2;
  border-radius: 5px;
  padding-left: 5px;
  margin-bottom: 20px;
}

.label {
  float: left;
  color: white;
  text-align: right;
  height: 30px;
}

.forgotPasswd {
  width: 100%;
  text-align: right;

  a {
    color: $chartreuse;
  }
}

.btnStyle {
  text-align: center;
  display: flex;
  justify-content: space-between;
}
 
.submit {
  border: 0;
  background: transparent;
  color: $white;
  border-radius: 100%;
  font-size: 40px;
  height: 40px;
  width: 40px;
  justify-content: space-between;
  cursor: pointer;
  text-align: right;

  &:hover {
    color: $chartreuse;
  }
}


.social {
  width: 100%;
  max-width: 600px;
  margin: auto;
  text-align: center;
  padding: 5px;
  margin-top: 20px;
  border: 0;
  border-top: 1px solid $chartreuse;

  .socialButton {
    background-color: Transparent;
    background-repeat: no-repeat;
    border: none;
    cursor: pointer;
    overflow: hidden;
    outline: none;

    img {
      margin: 10px;
      width: 40px;
      height: 40px;
    }
  }
}

@media screen and (max-width: 769px) {
  .wrapper {
    width: 90%;
  }
}
</style>
