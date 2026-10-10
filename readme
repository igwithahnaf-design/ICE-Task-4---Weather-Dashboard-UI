# ICE Task 4 – Weather Dashboard & UI Debugging

## 1. Introduction

The Weather Dashboard is a React Native mobile app that shows hardcoded weather data for three South African cities: Johannesburg, Cape Town and Durban. The user selects a city and the dashboard shows the current weather with a background image, extra current details (feels like, humidity, wind, visibility, pressure, UV index), a 24-hour forecast, a five-day forecast, and Sun & Moon information. The supplied `App.tsx` contained several intentional errors, which are documented below.

## 2. Development Environment

- Expo
- React Native
- TypeScript
- Institutional VM
- BlueStacks 5 emulator
- Expo Go

## 3. Error Log

| # | Location | Problem | Error Type | Correction |
|---|----------|---------|------------|------------|
| 1 | Imports | `ImageBackground` was used in the JSX but not imported from `react-native`, so the app crashed with a "Can't find variable: ImageBackground" error. | Import / Runtime | Added `ImageBackground` to the `react-native` import list. |
| 2 | City selector – buttons | The selected state compared against `weather.country` and `onPress` set `weather.country`. Every city has the country "South Africa", so no city matched, the `find` returned `undefined` and the app showed "Weather information unavailable". | Logic / State | Changed both to `weather.city`, so the state holds the city name that `weatherData.find` looks for. |
| 3 | `ImageBackground` `source` | `source` was given the URL string directly. React Native needs an image source object for remote images, so the background did not load (and TypeScript reports a type error). | TypeScript / Component property | Changed to `source={{ uri: selectedWeather.backgroundImage }}`. |
| 4 | Current details – Humidity | The humidity value used `selectedWeather.feelsLike` with a `%` sign, so it showed the feels-like temperature instead of the humidity. | Logic / Incorrect data | Changed to `selectedWeather.humidity`. |
| 5 | `WeatherDetail` component | The value `Text` rendered `{label}` instead of `{value}`, so every detail (Feels Like, Wind, Sunrise and so on) showed its own label rather than its data. | Logic / Component | Changed to `{value}`. |
| 6 | 24-hour forecast – `ScrollView` | `horizontal={false}` made the hourly cards stack vertically instead of scrolling sideways, which also hid the forecast layout. | Layout / Component property | Changed to `horizontal={true}`. |
| 7 | 24-hour forecast – temperature | Each hourly card showed `selectedWeather.temperature` (the current temperature) instead of the hour's own temperature, so all 24 cards showed the same value. | Logic / Incorrect data | Changed to `hour.temperature`. |
| 8 | Five-day forecast – `map` | The callback used braces `{ ... }` with no `return`, and the JSX ended in `;`, so it returned `undefined` and no days were displayed. | Syntax / Array rendering | Changed the braces to parentheses so the JSX is returned: `.map((day) => ( <View>...</View> ))`. |
| 9 | Five-day forecast – temperatures | `highTemperature` displayed `day.low` and `lowTemperature` displayed `day.high`, so the high and low were swapped. | Logic / Incorrect data | Swapped them: high style shows `day.high`, low style shows `day.low`. |
| 10 | Sun & Moon – Sunrise | The Sunrise row used `selectedWeather.sunset`, so sunrise showed the sunset time. | Logic / Incorrect data | Changed to `selectedWeather.sunrise`. |
| 11 | Styles – `dailyCard` | `flexDirection: 'column'` stacked the day, icon, temperatures and condition vertically, although the fixed widths on those items show they are meant to sit in one row. | Layout / Styles | Changed to `flexDirection: 'row'`. |
| 12 | Styles – `detailItem` | `width: '100%'` put every current-weather detail on its own line, so the `flexWrap` and `space-between` styles on the container did nothing and the section was very tall. | Layout / Styles | Changed to `width: '48%'` for a two-column grid. |
| 13 | Styles – `heroOverlay` | The overlay was almost transparent (`rgba(0,0,0,0.05)`), so the white city and weather text was hard to read on a bright background image. | Visual / Styles | Changed to `rgba(0, 0, 0, 0.35)`. |
| 14 | Styles – `weatherHero` | The hero section had `height: 170`, which is too small for the city name, country, icon, temperature and condition. The content overflowed and was clipped, so the city name and weather condition were not visible. | Layout / Dimensions | Increased the height to `270` so all the current-weather information is displayed. |

## 4. Testing

The corrected app was tested in the BlueStacks 5 emulator using Expo Go:

- **Test 1 – Initial application:** the app launches, the dashboard is displayed, the layout is organised and there are no errors.
- **Test 2 – City selection:** Johannesburg, Cape Town and Durban were each selected. The city name, current conditions, background image and forecasts changed to match the selected city.
- **Test 3 – Hourly forecast:** the 24 hourly cards scroll sideways, each showing the correct time, icon and its own temperature.
- **Test 4 – Five-day forecast:** five days are shown for each city with the correct icon, condition, high and low temperatures.
- **Test 5 – Sun & Moon:** sunrise, sunset, moonrise, moonset and moon phase are shown, with sunrise now different from sunset.
- **Test 6 – Complete interface:** I scrolled through the whole app and all sections were visible and usable.

## 5. Screenshot

The completed Weather Dashboard running in the BlueStacks 5 emulator using Expo Go:

![Weather Dashboard running in BlueStacks 5 using Expo Go](screenshot.png)

Screenshots from testing each city (top of the dashboard, then the Sun & Moon section at the bottom):

| Johannesburg – Sun & Moon | Cape Town | Cape Town – Sun & Moon |
|---|---|---|
| ![Johannesburg Sun and Moon](screenshot-johannesburg-sun-moon.png) | ![Cape Town](screenshot-capetown.png) | ![Cape Town Sun and Moon](screenshot-capetown-sun-moon.png) |

| Durban | Durban – Sun & Moon |
|---|---|
| ![Durban](screenshot-durban.png) | ![Durban Sun and Moon](screenshot-durban-sun-moon.png) |

## 6. Conclusion

This task showed me that UI bugs often do not produce compiler errors, and that I need to compare what is displayed with the underlying data. I learned to check imports and component props (such as the `uri` object for images), to return JSX properly from `map`, to pass the right state value when selecting items, and to use layout styles such as `flexDirection` and `horizontal` scrolling correctly. Testing each city and each section made the swapped values and wrong fields easy to spot.
