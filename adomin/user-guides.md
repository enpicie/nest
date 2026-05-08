---
layout: default
title: Adomin
---

<style>
.guide-toc a { display: flex; align-items: center; padding: 0.45rem 0.75rem; border-radius: 0.5rem; color: #c7d2fe; text-decoration: none; font-size: 0.875rem; font-weight: 500; transition: background 0.15s, color 0.15s, box-shadow 0.15s; }
.guide-toc a::before { content: "•"; color: #6366f1; margin-right: 0.5rem; }
.guide-toc a::after { content: "›"; color: #818cf8; font-size: 1.2rem; line-height: 1; margin-left: 0.4rem; transition: color 0.15s, transform 0.15s; }
.guide-toc a:hover { background: #334155; color: #fff; box-shadow: inset 3px 0 0 #6366f1; }
.guide-toc a:hover::after { color: #a5b4fc; transform: translateX(3px); }
</style>

# User Guides

<div class="guide-toc not-prose">
  <a href="#first-time-server-setup">First-Time Server Setup</a>
  <a href="#running-a-startgg-tournament">Running a start.gg Tournament</a>
  <a href="#running-an-event-eg-exhibition-other-non-tournament-event">Running an Event (Exhibition, etc.)</a>
  <a href="#running-a-league">Running a League</a>
</div>

## First-Time Server Setup

These steps only need to be done once per server.

1. Create a Discord role for event organizers. Users with this role can run privileged commands. Organizers should be anyone you want to be allowed to manage events in your server.
2. Run `/setup-server` and provide that role as `organizer_role`.
3. _(Optional)_ Run `/set-default-participant-role` to set a role that gets assigned to users when they check in. This can be used to ping active participants mid-event.
4. _(Optional)_ Run `/setup-notifications` to configure a channel for notifications such as automated event cleanup or startgg connection notifications.
5. _(Optional)_ Run `/setup-event-reminders` to setup automatic reminders for events. These can be configured per-event too, but this command sets up the defaults for your server.

## Running a start.gg Tournament

### Creating the Event

Run `/event-create-startgg` with your bracket link, `end_time`, and `timezone`. Adomi-san will create the event and automatically load all registered entrants into the registration list.

> Example link: `https://www.start.gg/tournament/midweek-melting-1/event/mbaacc-double-elim`

If new entrants sign up after creation, use `/event-refresh-startgg` to re-sync. Data for the event will be cleaned up and the participant role will be removed from all users after the given end time passes.

### On Event Day

1. Open check-in with `/check-in-toggle` (state: **Start**).
2. Participants run `/check-in` — this marks them as present and assigns the participant role if one is configured.

- Note that this does not check the user in on start.gg itself

3. Use `/check-in-list-absent` (with `ping_users: True`) to ping anyone who hasn't checked in yet.

- Recommended to run `/event-refresh-startgg` before this if your registration is open and you may have new entrants to sync.

4. When check-in is over, run `/check-in-toggle` (state: **End**).
5. Players can report scores with `/startgg-report-score` (this requires players to have Discord properly linked to start.gg to function correctly).

- Score reporting currently does not work for Teams and only works for individual players as it must connect the user in Discord to their connected start.gg account

> Recommend setting a check-in start time 30-min before your event start time and running `/check-in-list-absent` pinging users roughly 10-min before start time as a last call reminder, finally turning check-ins at event start time. After check-ins are turned off, that is a good time to remove attendees who did not check-in or DQ them.

\*_Score reporting requires authorization via `/startgg-connect` command where a user with permissions to report scores for the event must authorize Adomin to report scores._

### After the Event

Adomi-san automatically detects when the Discord scheduled event ends and will...

- Remove the participant role from all attendees
- Delete the event data
- Post a notification to your configured notifications channel

You can also manually clean up with `/check-in-clear`, `/register-clear`, and `/event-delete`.

## Running an Event (e.g. Exhibition, other non-tournament event)

### Creating the Event

Run `/event-create` and fill in the required fields: `event_name`, `event_location`, `start_time`, `end_time`, and `timezone`. Optionally add a description and specified Participant Role.

### Before the Event

_Registration is only used to determine who is expected to check-in at event time._ If you have a set of expected participants you want to register, you can run `/register` as an organizer and pass in specific users to register.

To allow users to register themselves:

1. Open registration with `/register-toggle` (state: **Start**) so participants can sign up.
2. Participants run `/register` to add themselves to the list.
3. Organizers can check the list any time with `/register-list`.

### Check-in Management

Check-in affirms participants are present for the event and assigns a Participant role to users as they check in.

1. Open check-in with `/check-in-toggle` (state: **Start**).
2. Participants run `/check-in` — this marks them as present and assigns the participant role if one is configured.
3. Use `/check-in-list-absent` (with `ping_users: True`) to ping anyone who hasn't checked in yet.
4. When check-in is over, run `/check-in-toggle` (state: **End**).

> One of the main benefits of the Participant role is managing channel access. If you want to use a specific role-gated channel to help plan or run your event, you can make it accessible specifically to users with the Participant role. Participants will then be able to access your channel after checking in.

### After the Event

Adomi-san automatically detects when the Discord scheduled event ends and will:

- Remove the participant role from all attendees
- Delete the event data
- Post a notification to your configured notifications channel

You can also manually clean up with `/check-in-clear`, `/register-clear`, and `/event-delete`.

## Running a League

The "League" format is a long-term event structure where players compete in groups over a longer period of time to climb ranks. See the "LeagueFormat" tab in [FGC League Template](https://docs.google.com/spreadsheets/d/1FojOkjQJD1dtr29fwH8bgabIdfxd-Yp72V0-pqbIqcc/edit?usp=sharing) Google Sheet for a full description.

Adomin works with [fgc-league-sheets](https://github.com/enpicie/fgc-league-sheets), a Google Sheets extension that handles the actual league automation: distributing players into groups, generating score matrices, and calculating tier promotions and demotions at the end of each rotation. The bot handles everything Discord-side — player sign-ups, score reporting, and keeping Discord roles in sync with the sheet.

**Adomi-san talks to the Google Sheet directly.** The fgc-league-sheets extension runs separately within Google Sheets itself, managing rotation cycles. Organizers interact with both.

Your Google Sheet file is the source of truth for league data so you can make manual adjustments as needed.

> Note: League functionality is still actively undergoing testing primarily via DMF Duel League for MBAACC. Contact **@enpicie** for any questions or issues experienced.

### First-Time League Setup

These steps only need to be done once per league.

1. Copy the [FGC League Template](https://docs.google.com/spreadsheets/d/1FojOkjQJD1dtr29fwH8bgabIdfxd-Yp72V0-pqbIqcc/edit?usp=sharing) sheet to get the starter sheet with latest version of the extension.

- Regardless of the stated version number, this sheet always has the latest version of the Google Sheets extension.

2. Share the sheet with the bot's service account. The account email is shown when you run `/league-create`.
3. Run `/league-create` with the league name, a short unique ID (max 4 characters, e.g. `MBAA`), the Google Sheets link, and optionally an `active_participant_role` to assign to active league members.
4. Run `/league-setup` to initialize the Participants sheet in the linked Google Sheet. This creates the roster the bot and the extension both read from.

### Each Rotation

#### Signing Up

1. Open joining with `/league-join-toggle` (state: **Start**).
2. Players run `/league-join` — this adds them to the Participants sheet with a **QUEUED** status, ready to be picked up when the next rotation starts.
3. Close joining with `/league-join-toggle` (state: **End**).

#### Starting the Cycle (in Google Sheets)

4. Open the Google Sheet and run the **Start Cycle** from the fgc-league-sheets extension. This promotes QUEUED players to ACTIVE, distributes all active players into groups by tier, and generates the score matrix for the rotation.
5. Run `/league-sync-participants` — this reads the sheet and assigns or removes the `active_participant_role` based on who is currently ACTIVE.

#### Reporting Scores

During the rotation, players report their match results in Discord:

- Run `/league-report-score` with the league name, `winner`, `loser`, and `score` (e.g. `3-2`, winner's score first). This writes the result to the score matrix in the Google Sheet.

#### Ending the Cycle (in Google Sheets)

6. Open the Google Sheet and run the **End Cycle** from the fgc-league-sheets extension. This analyzes win percentages, flags promotion and demotion candidates, and marks anyone who didn't complete their matches as inactive. Organizers can review and commit or undo the proposed changes before they take effect.
7. Run `/league-sync-participants` again to update Discord roles to match the new state of the sheet.

### Other League Management

| Task                                      | Command                                      |
| ----------------------------------------- | -------------------------------------------- |
| View league details and participant count | `/league-view`                               |
| List all leagues on the server            | `/league-list`                               |
| Mark yourself inactive or DNF             | `/league-deactivate` (optional: `dnf: True`) |
| Deactivate another player (Organizer)     | `/league-deactivate` with `player` set       |
| Update league name, sheet, or role        | `/league-update`                             |
| Delete a league record                    | `/league-delete`                             |
