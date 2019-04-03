To return current and next 4hour time stapmp: in format: "yy-mm-dd hh:mm:ss

```
getCurrentDateTime = () => {
        var now = new Date(),
            month = '' + (now.getMonth() + 1),
            day = '' + now.getDate(),
            year = now.getFullYear(),
            hours = '' + now.getHours(),
            minutes = '' + now.getMinutes(),
            seconds = '' + now.getSeconds();

        var time_after_4hours = new Date(now)
        time_after_4hours.setHours(now.getHours() + 12)
        
        var time_after_4hours_month = '' + (time_after_4hours.getMonth() + 1),
        time_after_4hours_day = '' + time_after_4hours.getDate(),
        time_after_4hours_year = time_after_4hours.getFullYear(),
        time_after_4hours_hours = '' + time_after_4hours.getHours(),
        time_after_4hours_minutes = '' + time_after_4hours.getMinutes(),
        time_after_4hours_seconds = '' + time_after_4hours.getSeconds();


        if (month.length < 2) month = '0' + month;
        if (day.length < 2) day = '0' + day;
        if (hours.length < 2) hours = '0' + hours;
        if (minutes.length < 2) minutes = '0' + minutes;
        if (seconds.length < 2) seconds = '0' + seconds;

        if (time_after_4hours_month.length < 2) time_after_4hours_month = '0' + time_after_4hours_month;
        if (time_after_4hours_day.length < 2) time_after_4hours_day = '0' + time_after_4hours_day;
        if (time_after_4hours_hours.length < 2) time_after_4hours_hours = '0' + time_after_4hours_hours;
        if (time_after_4hours_minutes.length < 2) time_after_4hours_minutes = '0' + time_after_4hours_minutes;
        if (time_after_4hours_seconds.length < 2) time_after_4hours_seconds = '0' + time_after_4hours_seconds;

        var currentDate = [year, month, day].join('-');
        var currentTime = [hours, minutes, seconds].join(':');
        var dateTime = currentDate + ' ' + currentTime;

        var dateAfter4Hours = [time_after_4hours_year, time_after_4hours_month, time_after_4hours_day].join('-');
        var timeAfter4Hours = [time_after_4hours_hours, time_after_4hours_minutes, time_after_4hours_seconds].join(':');
        var timeStampAfter4Hours = dateAfter4Hours + ' ' + timeAfter4Hours;

        let dict = {}
        dict['currentTimeStamp'] = dateTime
        dict['timeStampAfter4Hours'] = timeStampAfter4Hours

        return dict;
    }    ```
