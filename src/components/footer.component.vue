<template>
  <footer>
    <div class="top">
      <p>
        This project has some limitation like in a day this project can send 500
        emails because I am using  gmail as I am broke to buy a email services.
      </p>
      <p>
        If you need to send more than 500 emails then you can clone this project and use your own email service.
      </p>
      <p>
        And please don't spam the email service as it is free and I am using it
        and I don't want my email to be marked as spam
      </p>
      <p>
        If you have a job then: work.sbrakeshrath@gmail.com (Not kidding, really
        really I need a job)
      </p>
      <div class="links">
        <a
          href="https://github.com/SBRakeshRath/DB-less-OTP-Backend"
          target="_blank"
        >
          <img
            src="https://img.icons8.com/material-outlined/24/000000/github.png"
          />
          Backend
        </a>
        <a
          href="https://github.com/SBRakeshRath/DB-less-OTP-Frontend "
          target="_blank"
        >
          <img
            src="https://img.icons8.com/material-outlined/24/000000/github.png"
          />
          Frontend
        </a>
      </div>
    </div>
    <div class="bottom">This Project is made with ❤️...</div>
  </footer>
</template>

<style lang="scss">
footer {
  background-color: #dadde2;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin-top: 1rem;
  text-align: center;
  .top {
    padding: 1rem;

    p {
      margin-bottom: 1rem;
    }
    .links {
      a {
        display: flex;
        align-items: center;
        gap: 0.5rem;
        margin-bottom: 0.5rem;
      }
    }
  }
  .bottom {
    text-align: center;
    padding: 1rem;
    background-color: #ffa500;
  }
}
</style>
