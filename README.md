# Notes
RecurrenceData
        const repeatInstances = repeatInstancesNode && parseInt(repeatInstancesNode.textContent);
        const repeatForever = !!repeatForeverNode;
        //const windowEnd = windowEndNode && moment(windowEndNode.textContent);
        const windowEnd = windowEndNode && moment.tz(windowEndNode.textContent, "America/New_York");
        const { until } = recurrence;
        if (repeatForever) {
            until.type = RecurUntilType.forever;
        } else if (repeatInstances) {
            until.type = RecurUntilType.count;
            until.count = repeatInstances;
        } else if (windowEnd) {
            until.type = RecurUntilType.date;
            // until.date = windowEnd.clone();
            until.date = windowEnd ? windowEnd.format('YYYY-MM-DDTHH:mm:ssZ') : null;
        }
OR for local time 
const windowEnd = windowEndNode && moment.tz(windowEndNode.textContent, moment.tz.guess());
EventOccurence
        constructor(
            public readonly event: Event,
            public readonly start: Moment = moment.tz(event.start, "America/New_York"),
            public readonly end: Moment = moment.tz(event.end, "America/New_York")
        ) { }

OR for local time
public readonly start: Moment = moment.tz(event.start, moment.tz.guess()),
public readonly end: Moment = moment.tz(event.end, moment.tz.guess())
