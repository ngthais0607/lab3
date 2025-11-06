
#  Lab 04 – Task 2.1: Weather Dashboard

##  1. Objective
- Build a **Weather Dashboard** that allows the user to search for a city and view both the **current weather** and the **5-day forecast**.
- Apply **asynchronous JavaScript** using `async/await` and the **Fetch API** to retrieve live data from the **OpenWeather API**.
- Implement **real-time DOM updates**, **error handling**, and **localStorage** to store recent searches.

---

##  2. Tools & Environment
| Component | Description |
|------------|-------------|
| Languages | HTML · CSS · JavaScript |
| External API | [OpenWeather Current & Forecast APIs](https://openweathermap.org/api) |
| Key Used | 1 API key for both `/weather` and `/forecast` endpoints |
| IDE | Visual Studio Code |
| Browser | Google Chrome / Microsoft Edge |
| Execution | Open `index.html` in Live Server or browser |

---

##  3. Implementation Details

### 3.1 Page Layout
- **Search box** – input + Search button + recent search tags.
- **Current Weather Card** – city name, temperature, description, humidity, wind.
- **5-Day Forecast Grid** – five cards filtered by 12:00 pm data points.
- **Error/Loading** states – handled gracefully with user feedback.

---

### 3.2 Core Functions & Explanations

####  1. fetchWeather(city)
Fetches **current weather** data (temperature, humidity, wind, description).

#### 🌤 2. fetchForecast(city)
Retrieves **5-day / 3-hour forecast**; used to generate daily cards.

####  3. displayWeather(data)
Renders a stylized current weather card with emoji icons.

####  4. displayForecast(data)
Shows five forecast cards (one per day at 12 PM).

####  5. searchWeather()
Handles input, loading, error, and updates UI after fetching data.

####  6. Recent Search Functions
Stores up to 5 cities in `localStorage` and renders them as clickable tags.

####  7. Error Handling
Displays friendly messages for invalid cities or network errors.

####  8. iconFor(weatherMain)
Maps weather conditions to emoji icons for visual feedback:
☀️ clear ⛈️ thunderstorm 🌧️ rain 🌦️ drizzle ☁️ clouds ❄️ snow 🌫️ mist/fog

---

##  4. Results
| Scenario | Behavior |
|-----------|-----------|
| Valid city | Displays current weather and forecast cards |
| Invalid city | Shows red error message |
| Typing new city + Enter | Auto-fetches new data |
| Click recent tag | Loads saved city instantly |
| Empty input | “Please enter a city” message |

---

##  5. Program Flow
1. User types a city and presses Enter or Search.
2. `searchWeather()` runs → calls `fetchWeather()` + `fetchForecast()`.
3. Data received → `displayWeather()` and `displayForecast()` render cards.
4. City name saved to `localStorage` and displayed in Recent Searches.
5. Errors handled with `showError()`.

---

##  6. Conclusion
- Implemented a fully functional Weather Dashboard using live API data.
- Demonstrated knowledge of **fetch**, **async/await**, **JSON parsing**, and **DOM updates**.
- Enhanced user experience through real-time feedback and persistent recent searches.

---

##  7. Additional Notes
- Free API key limit: 60 requests per minute (avoid rapid testing).
- `units=metric` ensures ° Celsius output.
- Could be expanded with:
  - Dark/light mode
  - GPS auto-location
  - Weather icons from OpenWeather’s icon set
