# Google Meet GraphQL Schema

This directory contains a conceptual GraphQL schema for the Google Meet API, derived from the [Google Meet REST API v2](https://developers.google.com/meet/api/reference/rest/v2).

## Overview

The Google Meet API provides programmatic access to video conferencing functionality, including creating and managing meeting spaces, retrieving conference records, accessing participant data, and working with recordings and transcripts.

## Schema File

- `google-meet-schema.graphql` — Full GraphQL type definitions (55+ named types)

## Type Summary

### Space Management
| Type | Description |
|------|-------------|
| `Space` | A Google Meet meeting space that hosts video conferences |
| `SpaceConfig` | Configuration settings for a Meet space (access, entry, guest policy) |
| `SpaceUri` | URI and meeting code information for joining a space |
| `MeetingCode` | Alphanumeric meeting code used to join a space |
| `ActiveConference` | Reference to an in-progress conference in a space |
| `ModerationRestrictions` | Moderator-applied restrictions on chat, screen share, reactions |

### Conference Records
| Type | Description |
|------|-------------|
| `ConferenceRecord` | Immutable record of a completed or ongoing conference |
| `Meeting` | A meeting held within a space (includes participants, recordings, transcripts) |
| `Conference` | A single conference session |

### Participants
| Type | Description |
|------|-------------|
| `Participant` | A participant in a Google Meet conference |
| `ParticipantSession` | A single connection/session by a participant |
| `SignedinUser` | A signed-in Google user participant |
| `AnonymousUser` | An anonymous (unauthenticated) participant |
| `PhoneUser` | A participant who joined via phone dial-in |
| `PhoneParticipant` | Phone participant detail type |
| `BotParticipant` | An automated bot participant |
| `JoinTime` | Timestamp when a participant joined |
| `LeaveTime` | Timestamp when a participant left |

### Devices
| Type | Description |
|------|-------------|
| `Device` | A participant's device (type, camera, mic, screen share status) |
| `DeviceStatus` | Connection status of a device |
| `CameraStatus` | Camera on/off state |
| `MicrophoneStatus` | Microphone on/off state |
| `ScreenShare` | Screen sharing active/inactive state |

### Recordings
| Type | Description |
|------|-------------|
| `Recording` | A recording artifact from a conference |
| `RecordingState` | Enum: STARTED, PAUSED, ENDED, FILE_GENERATED |
| `RecordingDestination` | Target Drive folder configuration for a recording |
| `DriveDestination` | Drive file reference and export URI for a saved recording |

### Transcripts
| Type | Description |
|------|-------------|
| `Transcript` | A transcript artifact from a conference |
| `TranscriptState` | Enum: STARTED, PAUSED, ENDED, FILE_GENERATED |
| `TranscriptDestination` | Target Drive folder configuration for a transcript |
| `TranscriptEntry` | A single timestamped speech entry in a transcript |
| `DocsDestination` | Google Docs reference for a saved transcript |
| `Speaker` | A speaker reference within a transcript |
| `Caption` | An individual caption segment with speaker and timing |

### Layout & View
| Type | Description |
|------|-------------|
| `LayoutConfig` | Layout configuration for the meeting view |
| `Pinned` | Configuration for pinning a participant's video |
| `Spotlight` | Configuration for spotlighting a participant |
| `AutoLayout` | Auto layout enabled/disabled |
| `ActiveSpeaker` | Active speaker highlighting configuration |

### Artifacts & Config
| Type | Description |
|------|-------------|
| `MeetArtifact` | A Meet artifact (recording or transcript) reference |
| `ArtifactType` | Enum: RECORDING, TRANSCRIPT |
| `UserMeetingConfig` | Per-user meeting preferences (mute, camera, layout) |
| `MeetReservation` | A reservation for a future Meet session |
| `Reservation` | General reservation object |
| `GuestPolicy` | Enum: ALLOW_ALL, ALLOW_INVITED, DENY_ALL |

### Requests & Mutations
| Type | Description |
|------|-------------|
| `CreateSpaceRequest` | Input for creating a new meeting space |
| `UpdateSpaceRequest` | Input for updating an existing meeting space |
| `EndActiveConferenceRequest` | Input for ending the active conference in a space |
| `SpaceConfigInput` | Input configuration for a space |

### Auth & API
| Type | Description |
|------|-------------|
| `Operation` | A long-running API operation |
| `Token` | An OAuth 2.0 access token |
| `APIKey` | An API key credential |

### Pagination
| Type | Description |
|------|-------------|
| `SpaceConnection` | Paginated list of spaces |
| `ConferenceRecordConnection` | Paginated list of conference records |
| `ParticipantConnection` | Paginated list of participants |
| `ParticipantSessionConnection` | Paginated list of participant sessions |
| `RecordingConnection` | Paginated list of recordings |
| `TranscriptConnection` | Paginated list of transcripts |
| `TranscriptEntryConnection` | Paginated list of transcript entries |

## Enums

| Enum | Values |
|------|--------|
| `AccessType` | OPEN, TRUSTED, RESTRICTED |
| `EntryPointAccess` | ALL, CREATOR_APP_ONLY |
| `RecordingState` | STARTED, PAUSED, ENDED, FILE_GENERATED |
| `TranscriptState` | STARTED, PAUSED, ENDED, FILE_GENERATED |
| `SessionStatus` | ACTIVE, INACTIVE |
| `ArtifactType` | RECORDING, TRANSCRIPT |
| `LayoutType` | SPOTLIGHT, TILED, SIDEBAR, AUTO |
| `DeviceType` | DESKTOP, MOBILE, WEB, PHONE, CHROMEBOX, CAST |
| `CameraState` | TURNED_ON, TURNED_OFF |
| `MicrophoneState` | TURNED_ON, TURNED_OFF |
| `ScreenShareState` | ACTIVE, INACTIVE |
| `GuestPolicy` | ALLOW_ALL, ALLOW_INVITED, DENY_ALL |
| `ReservationStatus` | ACTIVE, EXPIRED, CANCELLED |
| `OperationStatus` | PENDING, RUNNING, DONE, FAILED |

## Root Operations

### Queries
- `space(name)` — Get a space by resource name
- `spaceByMeetingCode(meetingCode)` — Get a space by meeting code
- `conferenceRecords(filter, pageSize, pageToken)` — List conference records
- `conferenceRecord(name)` — Get a single conference record
- `participants(parent, filter, ...)` — List participants for a conference record
- `participant(name)` — Get a single participant
- `participantSessions(parent, ...)` — List sessions for a participant
- `participantSession(name)` — Get a single session
- `recordings(parent, ...)` — List recordings for a conference record
- `recording(name)` — Get a single recording
- `transcripts(parent, ...)` — List transcripts for a conference record
- `transcript(name)` — Get a single transcript
- `transcriptEntries(parent, ...)` — List entries for a transcript
- `transcriptEntry(name)` — Get a single transcript entry

### Mutations
- `createSpace(input)` — Create a new meeting space
- `updateSpace(input)` — Update an existing meeting space
- `endActiveConference(input)` — End the active conference in a space

## References

- [Google Meet REST API v2 Reference](https://developers.google.com/meet/api/reference/rest/v2)
- [Google Meet API Guides](https://developers.google.com/workspace/meet/api/guides/overview)
- [google-cloud-node SDK](https://github.com/googleapis/google-cloud-node/tree/main/packages/google-apps-meet)
