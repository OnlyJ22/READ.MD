# Just random notes

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
