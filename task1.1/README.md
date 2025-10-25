# 🧾 Lab 04 – Task 1.1: Interactive Form Validator

##  1. Objective
- To build a **sign-up form** that validates user input in real time.
- To apply knowledge of **DOM manipulation**, **Event handling**, and **Regular Expressions (RegEx)** in JavaScript.
- To practice using **classList**, **state objects**, and the **disabled attribute** to dynamically control user interaction.

## 2. Tools & Environment
| Component | Description |
|------------|-------------|
| Languages | HTML, CSS, JavaScript |
| Browser for testing | Google Chrome / Microsoft Edge |
| Recommended IDE | Visual Studio Code |
| Execution | Run the `.html` file directly in the browser |

##  3. Implementation Details

### Form Structure
| Field | Input Type | Validation Rule |
|--------|-------------|----------------|
| **Username** | text | 4–20 characters, only letters, digits, `_`, `.`, `-` |
| **Email** | email | Must follow a valid email format `name@domain.com` |
| **Password** | password | At least 8 characters, includes one uppercase and one number |
| **Confirm Password** | password | Must match the password field |

### Core Components in Code

#### Validation State Object
```js
const state = { username: false, email: false, password: false, confirm: false };
```
Tracks validation status for each input field.

#### Regular Expressions
```js
/^[A-Za-z0-9._-]{4,20}$/          // username
/^[^\s@]+@[^\s@]+\.[^\s@]+$/      // email
/^(?=.*[A-Z])(?=.*\d).{8,}$/      // password
```
Define patterns for allowed characters and structure of valid input.

#### Error Display Functions
```js
function showError(fieldId, message) {
  const err = document.getElementById(fieldId + "Error");
  const input = document.getElementById(fieldId);
  err.textContent = message;
  err.classList.add("show");
  input.classList.add("invalid");
  input.classList.remove("valid");
}

function clearError(fieldId) {
  const err = document.getElementById(fieldId + "Error");
  const input = document.getElementById(fieldId);
  err.textContent = "";
  err.classList.remove("show");
  input.classList.remove("invalid");
  input.classList.add("valid");
}
```
- `showError()` highlights an invalid field with a red border and message.  
- `clearError()` removes the message and changes the border to green.

#### Validation Functions
```js
function validateUsername(username) {
  return /^[A-Za-z0-9._-]{4,20}$/.test(username);
}

function validateEmail(email) {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}

function validatePassword(password) {
  const regex = /^(?=.*[A-Z])(?=.*\d).{8,}$/;
  return regex.test(password);
}

function validatePasswordMatch(pass1, pass2) {
  return pass1.length > 0 && pass1 === pass2;
}
```
- `validateUsername()` → ensures correct characters and length  
- `validateEmail()` → verifies correct email structure  
- `validatePassword()` → enforces security pattern  
- `validatePasswordMatch()` → confirms both password fields match  

#### Form Validation Logic
```js
function validateForm() {
  if (!validateUsername(usernameEl.value.trim())) {
    showError("username", "Username must be 4–20 chars (letters/digits/._-).");
    state.username = false;
  } else {
    clearError("username");
    state.username = true;
  }

  if (!validateEmail(emailEl.value.trim())) {
    showError("email", "Invalid email (e.g., name@domain.com).");
    state.email = false;
  } else {
    clearError("email");
    state.email = true;
  }

  if (!validatePassword(passwordEl.value)) {
    showError("password", "Min 8 chars, 1 uppercase, 1 number.");
    state.password = false;
  } else {
    clearError("password");
    state.password = true;
  }

  if (!validatePasswordMatch(passwordEl.value, confirmEl.value)) {
    showError("confirm", "Passwords must match.");
    state.confirm = false;
  } else {
    clearError("confirm");
    state.confirm = true;
  }

  const allValid = state.username && state.email && state.password && state.confirm;
  submitBtn.disabled = !allValid;
  return allValid;
}
```
Checks all input fields, updates the `state` object, and toggles the submit button’s disabled status.

#### Real-Time Validation
```js
[usernameEl, emailEl, passwordEl, confirmEl].forEach((el) => {
  el.addEventListener("input", validateForm);
});
```
Triggers validation on every keystroke for instant feedback.

#### Submit Event
```js
form.addEventListener("submit", function (e) {
  e.preventDefault();
  if (validateForm()) {
    alert("Form submitted!");
  }
});
```
Prevents page reload and displays an alert once the form passes all checks.

##  4. Results
| Scenario | Behavior |
|-----------|-----------|
| Invalid input | Red border and visible error message |
| Valid input | Green border, hidden error message |
| All valid | “Sign Up” button becomes clickable |
| On submit | Displays `Form submitted!` alert |

##  5. Program Flow
1. User types → triggers `input` event.  
2. `validateForm()` runs to check all inputs.  
3. Invalid fields are shown in red with error messages.  
4. Valid fields turn green.  
5. When all inputs are valid, the submit button activates.  
6. Clicking “Sign Up” triggers final validation and success alert.

##  6. Conclusion
- The form dynamically validates user input in real-time.  
- Uses RegEx for validation and DOM manipulation for instant visual feedback.  
- Enhances user experience with clear, responsive form behavior.


