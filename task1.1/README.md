#  Lab 04 – Task 1.1:
Nguyen Quang Thai - ITCSIU22227

##  1. Objective
- To build a **sign-up form** that validates user input in real time.
- To apply knowledge of **DOM manipulation**, **Event handling**, and **Regular Expressions (RegEx)** in JavaScript.
- To practice using **classList**, **state objects**, and the **disabled attribute** to dynamically control user interaction.

##  2. Tools & Environment
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

#### Regular Expressions
```js
/^[A-Za-z0-9._-]{4,20}$/          // username
/^[^\s@]+@[^\s@]+\.[^\s@]+$/      // email
/^(?=.*[A-Z])(?=.*\d).{8,}$/      // password
```

#### Error Display Functions
```js
showError(fieldId, message);   // shows red border + error message
clearError(fieldId);           // clears message + turns border green
```

#### Form Validation Logic
```js
const allValid = state.username && state.email && state.password && state.confirm;
submitBtn.disabled = !allValid;
```
Enables the “Sign Up” button only when all fields are valid.

#### Real-Time Validation
```js
input.addEventListener('input', validateForm);
```
Runs validation instantly while the user types.

##  4. Results
| Scenario | Behavior |
|-----------|-----------|
| Invalid input in any field | Red border and visible error message |
| Valid input | Green border, hidden error message |
| All fields valid | “Sign Up” button becomes clickable |
| On submit | Displays `Form submitted!` alert |

The form reacts dynamically, updating its appearance and submit availability based on real-time user input.

##  5. Program Logic Flow
1. User types in any input field → triggers `input` event.
2. `validateForm()` executes and calls each specific validator.
3. If a field fails regex validation → `showError()` updates border & message.
4. If valid → `clearError()` updates the border color to green.
5. When all fields are valid → `submitBtn.disabled = false`.
6. On clicking “Sign Up”, the `submit` event checks one last time and shows an alert.

##  6. Conclusion
- Successfully implemented a fully functional **real-time form validator**.
- Demonstrated understanding of **JavaScript event handling**, **DOM updates**, and **RegEx validation**.
- The solution enhances user experience through immediate feedback and dynamic UI response.

##  7. Additional Notes
- Could be extended with:
  - Password visibility toggle
  - Strength meter for passwords
  - Input icons or success/error animations
- Works fully in all modern browsers without external libraries.
