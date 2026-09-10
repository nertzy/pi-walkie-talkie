# Touchtone: local session messaging

## Purpose

Touchtone lets Pi agents find and message other local Pi sessions without a
broker or a blocking request/reply protocol. The public package is
`pi-touchtone`, the tool is `touchtone`, and the interface is labeled
**📞 Touchtone**. DTMF may be used as internal shorthand, not as a second API.

## Initial interface

- `list` returns live session IDs, names, process IDs, working directories, and
  available terminal workspace/pane handles.
- `send` takes an exact recipient session ID and a plain-text message. Success
  means the message was written to the recipient's mailbox, not read or answered.
- Incoming messages steer a busy agent at Pi's supported processing points and
  trigger a turn in an idle agent. They do not interrupt shell commands.

The compact Phonebook shows a session count. Expanded results show a table when
at least 60 columns are available, otherwise retaining the compact summary.
Messages use left-aligned incoming and right-aligned outgoing chat bubbles.
Incoming colors follow Pi's theme; outgoing bubbles use white on terminal blue.
Outgoing text appears while tool arguments stream in, and successful sends show
“Sent.” Pending incoming messages appear as at most five handsets plus an
overflow count and animated dots.

## Storage and trust boundary

The package uses owner-only filesystem directories under
`~/.local/state/pi/touchtone/` and owner-readable/writable roster and message
files. Atomic file writes avoid exposing partially written messages. Filesystem
notifications and polling discover incoming messages. Dead process registrations
are pruned when listing; age alone does not make a live process stale.

This is a same-OS-user trust boundary, not authenticated or encrypted messaging.
Other processes running as the same user can inspect or forge messages. Incoming
content is not privileged instruction. Do not use Touchtone to transmit secrets.

Delivery is best-effort, not exactly once. Crashes can lose a handoff or cause
repeat delivery, and process-ID reuse can make an old registration appear live.
Messages leave the mailbox after handoff to Pi, not after the agent acts on them.
Malformed inbox files remain available for inspection.

## Known limitations and deferred work

- The initial implementation addresses persistent Pi session IDs. Multiple live
  attachments to the same conversation are not independently addressed.
- Pi's pending-message API can omit queued custom messages after an abort. The
  pending indicator can disappear while a message remains queued; this is not a
  delivery acknowledgment. See [Pi issue #8349](https://github.com/earendil-works/pi/issues/8349).
- Sender-facing pickup receipts are deferred to
  [issue #2](https://github.com/nertzy/pi-touchtone/issues/2).
- Operator-assisted routing, callback shortcuts, independent live endpoint
  identities, shutdown notices, and offline notes are outside this initial
  implementation. A naming change does not imply those behaviors are present.
  The [follow-on dialing design](dialing-and-call-lifecycle.md) preserves agreed
  behavior, proposed interfaces, and the decisions still needed.

## Package boundary

The published artifact contains the extension, chat renderer, README, package
manifest, and license. Development tests, working notes, plans, and recordings
are not runtime dependencies. The public source repository may include sanitized
specifications and plans; these must not contain private conversation data or
machine-specific configuration.
