```

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h2>Sign Up Form</h2>
    <form onsubmit="handleSubmit(event)">
      <div>
        <label for="name">Enter full name</label>
        <input name="fullName" id="name" />
      </div>
      <!-- <span style="font-size: 10px; color: red;">*This field is required</span> -->
      <!-- <br/> -->
      <div>
        <label for="email">Enter email</label>
        <input name="email" id="email" />
      </div>
      <!-- <br/> -->
      <div>
        <label for="password">Enter password</label>
        <input name="password" id="password" />
      </div>
      <button type="submit">Submit</button>
    </form>
    <script>
      function showError(name, message) {
        const inputField = document.getElementById(name);
        let spanField = inputField.nextElementSibling;

        // console.log({name:name,inputField , spanField:spanField});

        if (!spanField) {
          spanField = document.createElement("span");
          inputField.after(spanField);
        }
        spanField.textContent = "*" + message;
        spanField.style.color = "red";
        spanField.style.fontSize = "10px";
      }

      function removeError(inputId) {
        // Check span field is just after input field,if it is present then remove it
        const inputField = document.getElementById(inputId);
        const spanField = inputField.nextElementSibling;
        if (spanField) {
          inputField.nextElementSibling.remove();
        }
      }

      const handleSubmit = (e) => {
        e.preventDefault();

        const fullName = e.target.fullName.value?.trim();
        const email = e.target.email.value?.trim();
        const password = e.target.password.value?.trim();

        if (!fullName) {
          showError("name", "Fullname is required");
          return;
        } else {
          removeError("name");
        }

        if (!email) {
          showError("email", "Email is required");
          return;
        } else {
          removeError("email");
        }

        if (!password) {
          showError("password", "password is required");
          return;
        } else {
          removeError("password");
        }

        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(email)) {
          showError("email", "Enter a valid email address.");
          return;
        } else {
          removeError("email");
        }

        if (password.length < 6) {
          showError("password", "Password must be at least 6 characters long.");
          return;
        } else {
          removeError("password");
        }

        //FormData is a special type of javascript object which is used to handle form Data.
        const formData = new FormData(e.target);

        // formData.entries return all value in key-value pairs.
        const entries = formData.entries();

        //it converts all key-value pair in object.
        const data = Object.fromEntries(entries);
        console.log(":: >>>> data", data?.fullName);
      };
    </script>
  </body>
</html>


```
