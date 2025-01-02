<script lang="tsx" setup>
import axios, { AxiosError } from "axios";
import { ref } from "vue";
const otpResponseStatus = ref("");
const otpToken = ref("");
let emailResponseMessage = ref("");
const emailResponseLoading = ref(false);

const backendLink = import.meta.env.VITE_API_URL;
async function onEmailFormSubmit(e: Event) {
  e.preventDefault();

  emailResponseMessage.value = "";
  otpToken.value = "";
  emailResponseLoading.value = true;
  const email = (e.target as HTMLFormElement).email.value;
  try {
    const response = await axios.post(backendLink + "/send-otp-to-email", {
      email,
    });
    otpToken.value = response.data.token;
    emailResponseMessage.value = response.data.message;
  } catch (error) {
    if (
      error instanceof AxiosError &&
      error.response &&
      error.response.data.message
    ) {
      emailResponseMessage.value = error.response?.data.message;
      return;
    }
    emailResponseMessage.value = "An error occurred while sending email";
  } finally {
    emailResponseLoading.value = false;
  }
}

const otpResponseLoading = ref(false);
async function onOtpFormSubmit(e: Event) {
  e.preventDefault();
  const otp = (e.target as HTMLFormElement).otp.value;
  otpResponseStatus.value = "";
  otpResponseLoading.value = true;

  try {
    const response = await axios.post(backendLink + "/verify-otp", {
      otp,
      token: otpToken.value,
    });
    otpResponseStatus.value = response.data.message;
  } catch (error) {
    if (
      error instanceof AxiosError &&
      error.response &&
      error.response.data.message
    ) {
      otpResponseStatus.value = error.response?.data.message;
      return;
    }
    otpResponseStatus.value = "An error occurred while verifying OTP";
  } finally {
    otpResponseLoading.value = false;
  }
}
</script>

<template>
  <div class="bodyComponent">
    <form class="emailComponent" v-on:submit="onEmailFormSubmit">
      <input type="email" name="email" placeholder="Enter your email" />
      <input type="submit" value="Send OTP" :disabled="emailResponseLoading" />
    </form>
    <p class="messageContainer">
      {{ emailResponseMessage }}
    </p>
    <form class="otpComponent" v-on:submit="onOtpFormSubmit">
      <input type="text" name="otp" placeholder="Enter OTP" />
      <input type="submit" value="Verify OTP" 
       :disabled="otpToken === '' || otpResponseLoading"
      />
    </form>

    <div class="otpVerificationStatusComponent">
      <div class="statusLabel">
        <p>OTP verification Status</p>
      </div>
      <div class="status">
        <p>
          {{ otpResponseStatus }}
        </p>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.bodyComponent {
  padding: 30px 0px;
  .messageContainer {
    padding: 10px;
    font-size: 1rem;
    text-align: center;
  }
}

.emailComponent,
.otpComponent {
  display: flex;
  padding: 15px 10px;
  gap: 10px;
  input[type="email"],
  input[type="text"] {
    flex-grow: 1;
    padding: 20px;
    font-size: 1rem;
    outline: none;
    border: 2px solid #ed890e;
    border-radius: 15px;
  }
  input[type="submit"] {
    padding: 20px;
    font-size: 1rem;
    outline: none;
    border: none;
    border-radius: 5px;
    background-color: #ed890e;
    color: white;
    cursor: pointer;
    &:hover {
      background-color: #ffa500;
    }
  }
  input[type="submit"]:disabled {
    background-color: #d3d3d3;
    cursor: not-allowed;
  }
}

.otpVerificationStatusComponent {
  display: flex;
  gap: 10px;
  padding: 15px 10px;

  .statusLabel{
    p {
      font-size: 1rem;
      font-weight: bold;
      padding: 10px;
      background-color: #D9D9D9;
      height: 100%;
      // border-radius: 10px;
    }
  }
  .status{
    flex-grow: 1;
    p {
      font-size: 1rem;
      padding: 10px;
      background-color: #FACF7A;
      text-align: center;
      height: 100%;

      // border-radius: 10px;
    }
  }
}
</style>
