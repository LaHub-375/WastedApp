#WastedApp (workshopping the name)

an app for getting drunk people home safe

Problem:

Intoxicated people (partygoers, university students etc) can end up drunk at 4am with nowhere safe to go, 
this situation is pretty common and unsafe.

Solution:

A "buddy" app designed specifically for impaired users with a UI/UX built around a drunk person 
(poor motor control, memory, decision making etc.) that makes it simple to get an impaired person home safe.

Features:

UX

Easy to use impaired mode UI: 3-4 giant buttons (Call Someone, Get Home, I'm Not Safe, Share Location)
Voice capability ("call (contact)"), (might be hard to implement bc would have to account for slurred speech)

Getting Home

Pre-set safe addresses (set while sober) labeled by nickname ("mom's house"), ideally end-to-end encrypted client-side
"Get Home" opens Uber/Lyft etc with the saved address auto-copied to clipboard, user pastes it in

Safety Session (separate from Party Mode toggle)

Low interaction fallback: upon ride ending, if there's no activity within X minutes, auto-calls emergency contact, speaks location aloud
"I'm home" confirmation button, tapped by the user upon arrival
Confirmed = session closes, data hard-deleted
Not confirmed = escalates to emergency contact, data retained until resolved

Standard mode
Where you set up and adjust privacy settings before heading out.
Ads on during standard mode <3

Party Mode

Freezes privacy settings from being changed mid-use
Easy to exit (no PIN needed to turn off)
Prototype version: manual toggle (future version would have geofencing do it automatically once near a club frat etc)
Ads off during Party Mode/active session

Privacy & Security

PIN gates only setting changes, never the emergency flow
Field-level or full E2E encryption for saved addresses/contacts
TLS in transit (supabase), encryption at rest (supabase), least-privilege access, audit logging, rate limiting

Monetization

Free with ads outside Party Mode/session
Subscription: always ad-free + extras (multiple addresses, group tracking, priority rideshare)
B2B licensing to universities

Stack
Mobile App: React Native TypeScript
Backend & Database: Supabase (managed Postgres)

Postgres database
Built-in Auth
Row-Level Security (RLS) policies — written in SQL

Field-level/E2E encryption: implemented in your own app code (TypeScript, can use libsodium), client-side, keyed off the user's PIN
Push notifications: FCM + APNs, or OneSignal
Infra: Supabase hosts backend/DB; AWS for v2
Admin/B2B dashboard: Next.js (also TypeScript), separate app, connects to the same Supabase backend
