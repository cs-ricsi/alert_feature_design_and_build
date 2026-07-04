# Prompt 001

Now we can move on to 01-scope-and-assumptions

# Prompt 002

This document ended up pretty large, can we go and review it section by section.

# Prompt 003

At the first place it should work for email and Slack, but it should be easy expandable for new cahnnels.

# Prompt 004

Also it says: "We need an admin view too." but we are not sure, what can be done there.

# Prompt 005

The Objective is good, we can move to the next section of the Scope and Assumptions document

# Prompt 006

In the brief it says:
"We want users to be able to set up alerts so they get notified when something important happens in the world — like breaking news, market movements, natural disasters, that kind of thing."
This can be meant by more ways. What I mean by this is the user should be able to set the alert and chose, where should he get notified, but he can not explicitly define what type of alert is it. The alert itself can send a lot of different type of notifications.

# Prompt 007

I would go with "every active alert subscription receive every important event", so this means when a user add an alert, then he can only chose what type of channel he would like to get notified. In the beginning, because we will only have email or Slack options, one user can set up up to two alerts.

# Prompt 008

Do you can any concerns aout this decision, or do you see any drawbacks about this?

# Prompt 009

Later we will be still able to add alert types, but can we make sure this concerns are in the decision log? Are you still this is the better choice for now with all the avaialble information?

# Prompt 010

update the MVP Scope section

# Prompt 011

I think we need to revisit this: "A user can maintain a single alert subscription and configure one or more delivery channels for it." I think it would be better, if a user could only select one channel, for a task. This way, it will be easier to delete an alert for a specific channel, or later it will be easier to link specific alert types to specific channels. It will make easier and cleaner to search for specific channel alert. What are you thoughts?

# Prompt 012

rewrite the docs/decision-log/002-alert-subscription-model.md to align with this decision

# Prompt 013

rewrite the MVP scope

# Prompt 014

In the Event processing part, where it says: "For the MVP, the system is responsible for determining whether an event is important enough to trigger notifications" In my opinion the system should not be responsible to determining what is imortant and what is less important. I think we will need to have some sort of interface or something, which can provide us important news, and we just forward it to the desired channel. The explicit method of getting the news is a different a question.

# Prompt 015

We don't have to recording the result of each notification attempt

# Prompt 016

rewrite the MVP scope section

# Prompt 017

Let's modify the Admin view, but still highlight that the brief is not define the admin responsibilities in detail, so I want to make to much here and give to much effort into this section. Also this is something which has more meaning to it. The first meaning is, we need an admin view, when an Administrator user logs in, and the other is, we need an admin view, where the user can admistrate their alerts.

# Prompt 018

I would go for the "User alert management" meaning of the admin view. Which means where the user can see his alerts listed, he can do basically two things, he can add a new one or switch to admin view, which basically the same page, but he can modify or delete the existing alerts. I would go with this, because I assume users are need to be able to modify existing alerts in the MVP, but I am not too sure about we need an Adminitrator view, specificly for Admin type users, but it is something what will be definitly supplemented in the future. Also this is something wich will reduce the complexity at the beginning

# Prompt 020

create a decision log about this decision

# Prompt 021

one thing I noticed: We don't want users to be able to "enable or disable an alert", they either have an alert or delete them

# Prompt 022

we can continue with the Out of Scope section

# Prompt 023

Switch “Each alert simply represents a subscription to alert-triggering events for a specific notification channel.” sentence to "Users do not define custom alert rules, event categories, thresholds, or filters."

# Prompt 024

I would add one more thing to this. We assume that, for every channel we have an interface to send notification, for example we ha some sort of API for Slack, to notify the user.

# Prompt 025

Also one thing what came to my mind, when we have different channel, we will need different type of settings realted to the type of the channel. For example for slack notifications, we will need a slack user id, I assume, or for an email, we will need an email address from the user.

# Prompt 026

also for the Out of scope section, we can include that, Slack user id or email address validations are out of scope, as notification delivery checks
