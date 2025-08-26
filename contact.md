---
layout: default
title: Contact
---
<main class="main-content">
  <div class="contact-form-container">
    <div class="text-center">
      <h1>Contact Me</h1>
    </div>
    <form action="https://api.web3forms.com/submit" method="POST" id="form" class="contact-form">
      <input type="hidden" name="access_key" value="b5dbb804-ce2b-404c-8c08-19eef9467f10" />
      <input type="hidden" name="subject" value="New Message On Your Website"/>
      <input type="checkbox" name="botcheck" id="" style="display: none;" />
    <div id="nameInputs">
    <div>
      <label for="first_name">First Name</label>
      <input type="text" name="name" id="first_name" placeholder="Gregory" required />
    </div>
    <div>
      <label for="lname">Last Name</label>
      <input type="text" name="last_name" id="lname" placeholder="House" required />
    </div>
    </div>
      <label for="email">Email Address</label>
      <input type="email" name="email" id="email" placeholder="greghouse@gmail.com" required />
      <label for="message">Your Message</label>
      <textarea rows="5" name="message" id="message" placeholder="Your message here" required></textarea>
      <button type="submit">Send Message</button>
      <p id="result"></p>
    </form>
  </div>
</main>


<script>
    const form = document.getElementById("form");
const result = document.getElementById("result");

form.addEventListener("submit", function (e) {
  e.preventDefault();
  
  const formData = new FormData(form);
  const object = Object.fromEntries(formData);
  const json = JSON.stringify(object);
  
  result.innerHTML = "Please wait...";

  fetch("https://api.web3forms.com/submit", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      Accept: "application/json",
    },
    body: json,
  })
    .then(async (response) => {
      let json = await response.json();
      if (response.status == 200) {
        result.innerHTML = json.message;
        result.classList.remove("text-gray-500");
        result.classList.add("text-green-500");
      } else {
        console.log(response);
        result.innerHTML = json.message;
        result.classList.remove("text-gray-500");
        result.classList.add("text-red-500");
      }
    })
    .catch((error) => {
      console.log(error);
      result.innerHTML = "Something went wrong!";
    })
    .then(function () {
      form.reset();
      setTimeout(() => {
        result.style.display = "none";
      }, 5000);
    });
});
</script>


<!-- <form id="contactForm" action="https://api.web3forms.com/submit" method="POST">

    <input type="hidden" name="access_key" value="b5dbb804-ce2b-404c-8c08-19eef9467f10">
    <input type="hidden" name="subject" value="New Message On Your Website">

    <input type="text" name="name" required>
    <input type="email" name="email" required>
    <textarea name="message" required></textarea>
    

    <button type="submit">Submit Form</button>

</form>



<script>
  window.addEventListener("pageshow", function() {
    document.getElementById("contactForm").reset();
  });
</script>
 -->
