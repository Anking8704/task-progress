# Codex desktop checklist display

The Windows Codex desktop build 26.1029.7803.0 displays the active plan as a compact “Step X / Y” indicator above the composer. Hovering reveals the full checklist. The indicator is shown during an active response and disappears when it ends.

## Verification

In a live test, the user hovered over the progress indicator and confirmed that all three task items appeared. The indicator also advanced as the plan changed. Inspection of the installed application showed that the tooltip is populated from the plan items and that the composer indicator is conditional on an active turn.

A successful tool call by itself does not establish that a user can see the list. UI behavior may differ by version, surface, or configuration. Display a Markdown checklist in chat when users need persistent, immediately visible progress.

## Configuration

Where supported, `[tools.update_plan]` with `enabled = true` in the global Codex configuration enables the tool. Restart and test in a new chat; project or environment settings may affect availability.
