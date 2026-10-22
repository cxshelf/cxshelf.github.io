# CXShelf chat setup

The Chat tab is wired to the existing cx-games Firebase project. Deploy the rules below in Firebase Console so permissions are enforced by the backend; UI checks alone are not security.

## Firestore rules

The updated firestore.rules preserves the existing private user-save rule and adds:
- chat-1: anyone can read and post, including signed-out visitors.
- chat-2: everyone can read; only signed-in users can post.
- system: everyone can read; only gigasquirreldev@gmail.com and bessa8563@gmail.com can post.
- Message edits/deletes are disabled.

In Firebase Console → Firestore Database → Rules, publish the contents of firestore.rules.

## Photo uploads

The storage.rules file allows public viewing of chat-2 photo attachments and limits uploads to authenticated users' own folders, images only, up to 5 MB. In Firebase Console → Storage → Rules, publish the contents of storage.rules.

## Notes
- Messages use chats/{room}/messages/{messageId} and update live.
- chat-1 asks for a username and optional email; these are user-entered and not verified.
- chat-2 attachments are image-only (JPEG, PNG, WebP, GIF), max 5 MB.
- Public rooms can attract spam; Firebase App Check or rate limiting is recommended before broad public launch.
