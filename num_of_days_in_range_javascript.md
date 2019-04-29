```
/**To return number of days in a range of two dates */
    daysBetween = (date1, date2) => {

        // The number of milliseconds in one day
        var ONE_DAY = 1000 * 60 * 60 * 24;

        // Convert both dates to milliseconds
        var date1_ms = date1.getTime();
        var date2_ms = date2.getTime();

        // Calculate the difference in milliseconds
        var difference_ms = Math.abs(date1_ms - date2_ms);

        // Convert back to days and return
        return Math.round(difference_ms / ONE_DAY);

    }

    /**To return number of weeks in a range of two dates */
    weeksBetween = (date1, date2) => {

        // The number of milliseconds in one week
        var ONE_WEEK = 1000 * 60 * 60 * 24 * 7;

        // Convert both dates to milliseconds
        var date1_ms = date1.getTime();
        var date2_ms = date2.getTime();

        // Calculate the difference in milliseconds
        var difference_ms = Math.abs(date1_ms - date2_ms);

        // Convert back to days and return
        return Math.round(difference_ms / ONE_WEEK);

    }

    /**To return number of months in a range of two dates */
    monthsBetween = (d1, d2) => {

        var months;
        months = (d2.getFullYear() - d1.getFullYear()) * 12;
        months -= d1.getMonth() + 1;
        months += d2.getMonth();
        return months <= 0 ? 0 : months;

        // return months
    }
   ```
