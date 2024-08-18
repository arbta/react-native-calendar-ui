# Introduction
A **simple** and **customizable** React Native component for displaying and interacting with **Gregorian calendar** dates.

# Features
- 💡 100% Typescript
- ⚡️ Build with `@shopify/flashlist` for faster list rendering
- 🕑 Works in all timezones
- 🎨 Fully customizable
- 🈲 Supports localization
- 🚀 DX, UX and Performance in one lightweight bundle
- 👨🏽‍💻 Works in every RN project

# Installation
To install the package, use npm or yarn:

```bash
npm install @arbta/calendar-kit
```
or

```bash
yarn add @arbta/calendar-kit
```


# Usage
Here’s a basic example of how to use the `@arbta/calendar-kit` package:

## Calendar
```typescript jsx
import React, { useCallback, useState } from "react";
import { Calendar, toLocaleDateString } from "@arbta/calendar-kit";

const today = new Date();

const todayDateString = toLocaleDateString(today);

const CalendarComponent = () => {
  const [selectedDay, setSelectedDay] = useState<string>();

  const onDayPress = useCallback((dateString) => {
    setSelectedDay(dateString);
  }, []);

  return (
    <Calendar
      date={todayDateString}
      markedDates={[selectedDay]}
      onDayPress={onDayPress}
    />
  );
};
```

## CalendarList
```typescript jsx
import React, { useCallback, useState } from "react";
import {CalendarList, toLocaleDateString} from "@arbta/calendar-kit";

const today = new Date();
const todayDateString = toLocaleDateString(today);

const CalendarListComponent = () => {
    const [selectedDay, setSelectedDay] = useState<string>();
    
    const onDayPress = useCallback((dateString) => {
        setSelectedDay(dateString);
    }, []);

  return (
    <CalendarList
      currentDate={todayDateString}
      estimatedCalendarSize={400}
      markedDates={[selectedDay]}
      futureMonthsCount={12}
      pastMonthsCount={0}
      onDayPress={onDayPress}
    />
  );
};
```

# API Reference

## Calendar Props
Our `Calendar` component has a list of props that make it easy to plug and play UI for your calendars.

| Prop                    | Type                                                                                                                                                                                      | Description                                                                                                                                                                                                                                                                                                   | Default     |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------|
| `contentContainerStyle` | <small>`ViewStyle?`</small>                                                                                                                                                               | ViewStyle` for calendar's parent view component                                                                                                                                                                                                                                                               | `undefined` |
| `customStateCreator`    | <small>`((stateInputParams: StateInputParams, defaultState?: DayState) => object)?`</small>                                                                                               | `Function` for extending/customizing calendar day state <br/><small>_⚠️Caution: Always use a pure named function for optimal performance. See example [here](https://github.com/arbta/calendar-kit/blob/22259522e87e177c255369a872165063514b7868/example/src/examples/airbnb/airbnb.stories.tsx#L19)</small>_ | `undefined` |
| `date`                  | <small>`string`</small>                                                                                                                                                                   | Any date in the month you want to show in the calendar; example: `2024-08-16` for month of `August, 2024`<br/> <small>**Format** `YYYY-MM-DD`</small>                                                                                                                                                         | `required`  |
| `firstDayOfWeek`        | <small>`DayIndex?`</small>                                                                                                                                                                | `DayIndex` which is used to determine the first day of the week for this `date` according to local time, where 0 represents Sunday                                                                                                                                                                            | `0`         |
| `locale`                | <small>`string?`</small>                                                                                                                                                                  | Locale string used to localize calendar content                                                                                                                                                                                                                                                               | `en-US`     |
| `markedDates`           | <small>`string[]`</small>                                                                                                                                                                 | Selected day(s) on the calendar to be highlighted<br/><small>**Format** `[YYYY-MM-DD,...]`</small>                                                                                                                                                                                                            | `[]`        |
| `maxDate`               | <small>`string?`</small>                                                                                                                                                                  | Maximum selectable date on the calendar example: `2024-12-31`<br/><small>**Format** `YYYY-MM-DD`                                                                                                                                                                                                              | `undefined` |
| `minDate`               | <small>`string?`</small>                                                                                                                                                                  | Minimum selectable date on the calendar example: `2024-01-01`<br/><small>**Format** `YYYY-MM-DD`                                                                                                                                                                                                              | `undefined` |
| `MonthNameComponent`    | <small>`React.ComponentType<{ month: Date; locale?: string }>`</small>                                                                                                                    | Custom component to render calendar's `month` title; example: `August, 2024`                                                                                                                                                                                                                                  | `undefined` |
| `onDayPress`            | <small>`((dateString: string) => void)?`</small>                                                                                                                                          | `Function` for adding press listener to calendar day <br/><small>_⚠️ Caution: Always use a pure named function for optimal performance. See example [here](https://github.com/arbta/calendar-kit/blob/22259522e87e177c255369a872165063514b7868/example/src/hooks/useMultiSelectCalendar.ts#L29)_</small>      | `undefined` |
| `showDayNames`          | <small>`boolean?`</small>                                                                                                                                                                 | Show week day names on the calendar                                                                                                                                                                                                                                                                           | `true       |
| `showExtraDays`         | <small>`boolean?`</small>                                                                                                                                                                 | Show extra days from previous and next month in the current month's calendar                                                                                                                                                                                                                                  | `true`      |
| `showMonthName`         | <small>`boolean?`</small>                                                                                                                                                                 | Show calendar's month title                                                                                                                                                                                                                                                                                   | `true`      |
| `weekContainerStyle`    | <small>`ViewStyle?`</small>                                                                                                                                                               | `ViewStyle` for each week `row` on the calendar                                                                                                                                                                                                                                                               | `undefined` |
| `WeekDayNameComponent`  | <small>`React.ComponentType<{ weekDays:string[] }>`</small>                                                                                                                               | Custom component to render calendar's week day names                                                                                                                                                                                                                                                          | `undefined` |
| `weekdaysFormat`        | <small>`"long","short","narrow"`><br/><br/>```short = ['Mon', 'Tue', ..., 'Sun']```<br/>```long = ['Monday', 'Tuesday', ..., 'Sunday']```<br/>```narrow = ['M', 'T', ..., 'S']```</small> | Format option for week day names                                                                                                                                                                                                                                                                              | `undefined` |
| `weekdaysShort`         | <small>`string[]?`</small>                                                                                                                                                                | Custom names for week days<br/> <small>_⚠️Caution: This overrides the default localized week day names_</small>                                                                                                                                                                                               | `undefined` |
| `weeksContainerStyle`   | <small>`ViewStyle?`</small>                                                                                                                                                               | `ViewStyle` for parent view component of all week `columns` on the calendar. Useful when you need to apply styling to all weeks in the calendar                                                                                                                                                               | `undefined` |

<br/>
<br/>

## CalendarList Props
`CalendarList` inherits all props of `Calendar` except `contentContainerStyle` & `date` props. It also comes with unique props to help you build performant list of calendars whiles using `@shopify/flashlist` under the hood.

| Prop                            | Type                                                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | Default                                        |
|---------------------------------|-------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| `calendarContentContainerStyle` | <small>`ViewStyle?`</small>                           | `ViewStyle` for each calendar's parent view component. This is same as `contentContentContainerStyle` prop for  `Calendar` component                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | `undefined`                                    |
| `CalendarSeparator`             | <small>`React.ComponentType?`</small>                 | A component rendered between calendars in the list<br/><small>_⚠️ Caution: This overrides `calendarVerticalGap` prop when defined_                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `undefined`                                    |
| `calendarSize`                  | <small>`{width?:number, height?: number}?`</small>    | Visible width and height of the CalendarList. This is not the scroll content size.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `{ width, height } = Dimensions.get("window")` |
| `calendarVerticalGap`           | <small>`number?`</small>                              | Space (px) between calendars in the list                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `32`                                           |
| `currentDate`                   | <small>`string?`</small>                              | Initial date to focus or scroll to when the `CalendarList` mounts<br/><small>_⚠️Caution: This prop is not reactive, changing it will not trigger re-render_<br/><br/>**Format** `YYYY-MM-DD`</small>                                                                                                                                                                                                                                                                                                                                                                                                     | `undefined`                                    |
| `estimatedCalendarSize`         | <small>`number`</small>                               | Estimated height or width (px) of each calendar when using `vertical` or `horizontal` calendar lists respectively.<br/><br/><small>_💡 `FlashList` uses this information to decide how many calendar months it needs to draw on the screen before initial load and while scrolling. Since some calendar months have 5 and 6 weeks, you need to find the average or median value and if most calendars are of the same size, just use that number. A quick look at `Element Inspector` can help you determine this. If you're confused between two values, the smaller value is a better choice._</small> | `required`                                     |
| `futureMonthsCount`             | <small>`number?`</small>                              | Number of months to render after `minDate`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | `12`                                           |
| `horizontal`                    | <small>`boolean?`</small>                             | Toggle horizontal scrollable list                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `false`                                        |
| `minDate`                       | <small>`string?`</small>                              | Date in your `starred` month on the calendar. A `starred` month is the month in calendar list used to determined `past` and `future` months of the list.<br/><small>Example: If you need to render daily events 6 months `before` and `after` date `2024-02-10`. Then `2024-02` becomes the `starred` month<br/><br/>**Format** `YYYY-MM-DD`</small>                                                                                                                                                                                                                                                     | `today's date`                                 |
| `onScroll`                      | <small>`((visibleMonths: string[]) => void)?`</small> | Callback for calendar list scroll events; returns array of visible months on the list ordered according to appearance on the list.<br/><small>**Format** `[YYYY-MM-DD,...]`                                                                                                                                                                                                                                                                                                                                                                                                                              | `undefined`                                    |
| `pastMonthsCount`               | <small>`number?`</small>                              | Number of months to render before `minDate`                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | `0`                                            |
| `showDayNamesOnTop`             | <small>`boolean?`</small>                             | Show week day names on top of list instead of in each calendar                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | `false`                                        |
| `showScrollIndicator`           | <small>`boolean?`</small>                             | Toggle on scroll indicators for `vertical` calendar list                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | `true`                                         |


## Contributing
Contributions are welcome! Please see the [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.