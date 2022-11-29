

## Background

To enjoy more stable and reliable services, we recommend you switch to the new supportive route.


## Impact

Because it is necessary to update the bootstrap-server addresses of producers and consumers and restart the service, the switch will cause a momentary interruption in business production and consumption.

## Directions

1. Create a supportive route.
2. Switch the CKafka bootstrap-server addresses of all producers and consumers to the newly created supportive route. The switch order does not matter as long as they are all switched.
3. Restart producers and consumers based on the business conditions. The restart order does not matter.
4. Observe whether the business is stable for at least 3 hours (recommended).
5. Delete the old supportive route.

## Rollback

If an exception occurs during business verification, you need to roll back to the old supportive route in the following steps provided that it has not been deleted.

1. Change back to the old supportive route address on all producers and consumers.
2. Restart all producer and consumer services.
3. Verify the business.
