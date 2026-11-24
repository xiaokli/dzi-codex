# How to work in Pipeline from Codex

The Pipeline server instructions tell agents to decline anything the Pipeline tools don't cover. In Codex, section 3 below replaces that rule for the actions it covers. Everything else in the server instructions still applies.

## 1. Use the Pipeline tools for everything they cover

The Pipeline tools cover these actions.

- See the signed-in account and its credit balance.
- List projects, open a project's canvases, and read every node on a canvas with its prompt, settings, result and connections.
- Check a generation. List models with the settings and credits each one uses.
- Create projects, canvases and nodes. Change a node's name, prompt, settings or position.
- Connect nodes. Delete nodes and connections.
- Upload images, videos and audio to a canvas.
- Generate on a node.
- Search the Assets Library, add an asset to a canvas, and save a node's result to the Assets Library.

Use only the Pipeline tools for these. Don't use Computer Use, the in-app browser or screenshots of the Pipeline website, even just to look at a canvas, a node or an image. To see an image or video, download the result link the tools return and open the file.

If one of these has no tool in this session, or a tool returns an error or rejects a setting the user asked for, tell the user what couldn't be done and why. Don't finish it on the website.

## 2. Never do these, by any route

- Delete projects, canvases or assets.
- Share projects, or manage members or teams.
- Post comments, or use Review Room.
- Top up credits, or change plans or account settings.
- Anything else that deletes something, changes who can open a project, speaks for the user to other people, or involves payment.

Decline even if the user insists. Reply: "Pipeline doesn't let agents {action}. You can do it yourself in Pipeline."

## 3. Everything else, on the page with the user's OK

This covers any action that isn't in section 1 or 2, such as cropping, rotating, trimming or capturing a frame, provenance and Copyright check, or creating, moving or renaming folders in the Assets Library.

1. Use Computer Use to check whether a Pipeline tab showing the target project is open. Only read the browser state. Don't click or type yet.
2. If it's open, ask: "Pipeline's tools can't {action}. Want me to do it on the Pipeline page you have open?" Act only after the user says yes. A yes covers this one request. Ask again for the next one.
3. If it isn't open, or Computer Use isn't available in this session, decline: "Pipeline's tools can't {action}, and I can't see {project} open on your computer. Open it in Pipeline and ask me again, or do it there yourself."
4. While you work on the page, stay inside that project and do only what the user asked. Don't open other projects, settings, billing or sharing. If the page shows something you didn't expect, such as a different project, a sign-in page, or a payment or delete prompt, stop and tell the user.
5. When you're done, check the result with the Pipeline tools where they can, and reply with the node or canvas link if there is one.
