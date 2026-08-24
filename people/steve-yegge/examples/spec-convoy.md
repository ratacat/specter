<!-- source: https://github.com/gastownhall/gastown/blob/main/docs/design/convoy/spec.md -->
# Convoy Manager Specification

A destination-plus-architecture spec. Status: implementation complete. Different from plan-to-beads (graph conversion).

## Problem

Convoys group work but don't drive it. Completion hangs on one poll cycle. Work finishes; the loop never lands.

Needed: event-driven completion, stranded recovery, redundant observation.

## Architecture

Daemon-resident `ConvoyManager`: event poll (5s) and stranded scan (30s). Shared observer `CheckConvoysForIssue`. Design decisions: SDK polling not CLI streaming; high-water mark; one issue fed per convoy per scan; stranded scan as safety net.

## Success

Quality gates for every story: `go test ./...`, `golangci-lint run`.

## Work units

S-01 event-driven completion detection. S-02 periodic stranded convoy scan. (Both marked DONE in the source.)
