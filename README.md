https://my-food-ranking.netlify.app/

https://www.thecsharpacademy.com

https://learn.microsoft.com/en-us/training/courses/az-140t00

https://algomap.io

sample pc build 
https://pcpartpicker.com/list/cNLjRV

<field name="XMLTZone">
    <![CDATA[
        <timeZoneRule>
            <standardBias>480</standardBias>
            <additionalDaylightBias>-60</additionalDaylightBias>
            <standardDate>
                <transitionRule month="11" day="su" weekdayOfMonth="first"/>
                <transitionTime>02:00:00</transitionTime>
            </standardDate>
            <daylightDate>
                <transitionRule month="3" day="su" weekdayOfMonth="second"/>
                <transitionTime>02:00:00</transitionTime>
            </daylightDate>
        </timeZoneRule>
    ]]>
</field>

Event.ts line 88

    public XMLTZone: string = '';  // Add this line

    constructor(author?: User, editor?: User, created?: Moment, modified?: Moment, id?: number, uniqueId?: Guid, etag?: number) {
        super(author, editor, created, modified, id, uniqueId, etag);

        this.XMLTZone = ''; // Initialize XMLTZone field
onlineEventServies line 85 

public track(event: Event): void;
public track(refiner: Refiner): void;
public track(refinerValue: RefinerValue): void;
public track(approvers: Approvers): void;
public track(entity: Event | Refiner | RefinerValue | Approvers): void {
    if (entity instanceof Event) {
        entity.XMLTZone = entity.XMLTZone || '';  // Ensure XMLTZone is set before persisting
        this._eventLoader.track(entity);
    } else if (entity instanceof Refiner) {
        this._refinerLoader.track(entity);
        entity.values.forEach(value => this.track(value));
    } else if (entity instanceof RefinerValue) {
        this._refinerValueLoader.track(entity);
    } else if (entity instanceof Approvers) {
        this._approversLoader.track(entity);
    }
}

onlineEventServices line 403

 createSampleEvents: async () => {
                console.log(`Starting 'createSampleEvents()'`);

                const refiners = await this._refinerLoader.all();

                const { currentUser } = this._directory;

                const events: Event[] = [];

                const timeZoneXML = `<![CDATA[
                    <timeZoneRule>
                        <standardBias>480</standardBias>
                        <additionalDaylightBias>-60</additionalDaylightBias>
                        <standardDate>
                            <transitionRule month="11" day="su" weekdayOfMonth="first"/>
                            <transitionTime>02:00:00</transitionTime>
                        </standardDate>
                        <daylightDate>
                            <transitionRule month="3" day="su" weekdayOfMonth="second"/>
                            <transitionTime>02:00:00</transitionTime>
                        </daylightDate>
                    </timeZoneRule>
                ]]>`;

                {
                    const event = new Event();
                    event.snapshot();
                    event.title = "North America East Quarterly Connect - Broadcast";
                    event.start = now().add(2, 'days').startOf('day').add(10, 'hours');
                    event.end = event.start.clone().add(2, 'hours');
                    event.location = "Online Teams Meeting";

                    for (const refiner of refiners)
                        event.refinerValues.add(refiner.values.get()[0]);

                    event.moderator = currentUser;
                    event.moderationTimestamp = now();
                    event.moderationStatus = EventModerationStatus.Approved;

                    // ADDING XMLTZone FIELD
                    event.XMLTZone = timeZoneXML; 

                    events.push(event);
                    this.track(event);
                    
