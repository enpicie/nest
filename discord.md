---
layout: default
title: Discord
---

# Discord Template

FGC Netplay Event Server Template (**FNEST**) is a Discord server template that sets you up with these features:
- Default set of roles to use with [Adomin](adomin) features
- Channels to manage check-in, score reporting, and other tournament ongoings
- Private channels for Commentary and Organizers
- Announcement, Info, and other channels for community

Create a server with this template: **[FGC Netplay Event Server Template](https://discord.new/8CDDhHHSxdtR)**

This template is based on Midweek Mashers where MBAACC events like [Midweek Melting](https://www.start.gg/hub/midweek-melting-1) run.

![Midweek Screenshot](./assets/Midweek%20screenshot.png)

## Roles

Roles in FNEST are set up for the following:
- Enable private Commentator and Organizer channels
- Setup for event announcements
- Default participant roles for use with Adomin

Adomin works with different roles to simplify notifying your community of events, managing channel access, and restricting privileged commands. `@Organizer` can be used as the organizer role when setting up Adomin, and the `@*Participant` roles can be used when setting up Check-in role assignment or League role assignment.

Apps such as [Carl-bot](https://carl.gg/) can be used to enable reaction-roles in `#roles` channel to set up `@Event Announcements` people can pick up to be notified of events.

<img src="./assets/FNEST roles.png" style="width: 70%; display: block; margin: auto;">

## Using Adomin

### Setup

`#bot-commands` channel comes with FNEST as an `@Organizer` limited channel where you can quietly run Adomin or other bot commands as needed. It is also recommended to setup this channel as your notifications channel if you use `/setup-notifications` for Adomin alerts.

### Reminder Announcements

`/setup-event-reminders` lets you configure default server settings for reminding your community of upcoming events. When reminders are turned on, Adomin will periodically scan and message the configured channel with a reminder message roughly 24-hours ahead of an upcoming event. She will ping a role like `@Event Announcements` if one is set.

`#announcements` is meant to be used as your announcements channel to centralize notifications for your community. **You will need to add permissions for Adomin to send messages in this channel.** By default it is limited to `@Organizer` so Adomin's role when she is added will need explicit access to send messages here.

## Community Recommendations

### Channel Usage

MBAACC community has seen significant growth and activity through consistent events and positive encouragement around event performance. FNEST is based on Midweek Mashers, which has supported this development.

`#event-schedule` is where your community can always check and see what events are coming up. Adomin's schedule commands like `/schedule-post` can automatically show your upcoming events here. Before building these features, Midweek Mashers would list all events for the upcoming month ahead of time and remove embeds so the list of events is always clearly readable.

`#top-8s` rewards good performance by being the place where top 8 images can be shared for posterity. Only `@Organizer` can post in this channel so you can build positivity around strong play by keeping a record of those who have placed well in your events. Midweek Mashers has a *"Hall of Fame"* channel category like this where [Top8ers](https://www.top8er.com/) for event series are posted.

`#organizer-chat` and `#comms-chat` are limited to `@Organizer` and `@Commentator` to ensure clear communication to help events run smooth. These are great places to bounce ideas off others and seek feedback from trusted people who are also supporting your community.

### Rules

Midweek Mashers' foundation is treating the online event space as you would an offline event space: your community is like your local, but online. Here are the foundational rules of Midweek server that you can use for starting your own set of server rules:

```md
## Treat this space like your local venue: if you wouldn't say it to a stranger at locals, don't say it here

1.** Be a decent human being. We are here to have fun. Treat people well and keep it chill.**
2. No forms of hate speech, slurs, NSFW content, bigotry, or discrimination of any kind will be tolerated.
3. Aggressive or inflammatory speech is not allowed. Tournaments can be frustrating and everyone has off days. Outbursts may receive warnings leading to eventual removal/ban. Keep it chill.
4. Inappropriate usernames in this server, start.gg, or in game may result in a DQ or removal. Please use your best judgement. If anyone has issues or questions, please DM [organizer].
5. This server/brackets respect bans from [main community server] in the interest of keeping things comfortable for players. If anyone has an issue with someone participating, please DM [organizer].
6. Please remember to ask before offering unsolicited advice. Brackets can be stressful experiences, so please be mindful of how people will feel after a loss.
```

### Midweek Mashers

**If you want to run events for FPan games:**
> I am building Midweek Mashers community as a hub to simplify running Netplay events for FPan games. My goal is to give our community more events of high quality by setting up roles so Organizers can easily set up to run events while sharing work of promotion, commentary, and streaming across a growing team.
>
> Contact **@enpicie** on Discord if you are interested in helping out with netplay events in this space. Feel free to [join Midweek Mashers](https://discord.gg/EnSsXwqS2k) and browse as well.

