Streams are the fundamental unit of storage in the Qi Service.  Each stream represents an ordered series of events or observations for a particular item of interest, e.g., the temperature of a given room.  Each stream must have a Qi Type associated with it, and each event sent to the stream must conform to this type or it will be rejected.  Streams may optionally have a Stream Behavior to control how data is returned.

## Qi Stream Object

```
  string Id
  string Name
  string Description
  string TypeId
  string BehaviorId
```

A Qi Stream object must include:
- an ‘Id’ field (unique)
- a ‘TypeId’ field with the Id of an existing Type.

## Naming Rules for Stream Identifiers
1.	Case sensitive
2.	Allows spaces.

## Stream Methods
*GetStream*
```
QiStream GetStream(string streamId);
Task<QiStream> GetStreamAsync (string streamId);
```

*REST*
```
Qi/Streams/{streamId}
```

HTTP GET

*Parameters*

`streamId` -- string identifying the stream

Returns a QiStream object.

*GetStreams*
```
IEnumerable<QiStream> GetStreams ();
Task<IEnumerable<QiStream>> GetStreamsAsync ();
```

*REST*
```
Qi/Streams
```

HTTP GET

Returns IEnumerable of all streams for the tenant. 

*GetOrCreateStream*
```
QiStream GetOrCreateStream (QiStream entity);
Task<QiStream> GetOrCreateStreamAsync (QiStream entity);
```

*REST*
```
Qi/Streams
```

HTTP POST
Body is serialized QiStream entity

*Parameters*

`entity` -- Qi Stream object
  
If `BehaviorId` is not specified, the stream will have the default behavior of `Mode=‘Continuous’` and `ExtrapolationMode=‘All’`. If entity already exists on the server by `Id`, that existing stream is returned to the caller unchanged.

*UpdateStream*
```
void UpdateStream(string streamId, QiStream entity);
Task UpdateStreamAsync(string streamId, QiStream entity);
```

*REST*
```
Qi/Streams/{streamId}
```

HTTP PUT
Body is serialized QiStream entity

*Parameters*

`streamId` -- identifier of the stream to modify
`entity` -- updated stream object

Permitted changes:

•	Name
•	BehaviorId
•	Description

Throws exception on unpermitted change attempt (and stream is left unchanged).
The `UpdateStream` method applies the entire entity. Optional fields left out of the entity will remove the field from the Stream if they had been set previously in the stream. 

*DeleteStream*
```
void DeleteStream(string streamId);
Task DeleteStreamAsync(string streamId);
```

*REST*
```
Qi/Streams/{streamId}
```

HTTP DELETE

*Parameters*

`streamId` -- identifier of the stream to delete

Delete stream using its stream id.
