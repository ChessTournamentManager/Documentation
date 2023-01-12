<h1>Chess Tournament Manager Requirements and Design</h1>

<h2>Table of Contents</h2>

- [Project description](#project-description)
  - [Goals of the application](#goals-of-the-application)
  - [Target Audience](#target-audience)
- [Competitive products ](#competitive-products)
  - [Swips](#swips)
    - [Limitations](#limitations)
    - [Good features](#good-features)
  - [Chessmanager](#chessmanager)
    - [Limitations](#limitations-1)
    - [Good features](#good-features-1)
  - [Coronate](#coronate)
    - [Limitations](#limitations-2)
    - [Good features](#good-features-2)
  - [SwissSys](#swisssys)
    - [Limitations](#limitations-3)
    - [Good features](#good-features-3)
  - [Tornelo](#tornelo)
    - [Limitations](#limitations-4)
    - [Good features](#good-features-4)
- [User Stories](#user-stories)
  - [Must have](#must-have)
  - [Should have](#should-have)
  - [Could have](#could-have)
  - [Won’t have](#wont-have)
- [Architecture](#architecture)
- [Feedback](#feedback)


# Project description

## Goals of the application

The goal of the application is to make (chess) tournament hosting easier for people and to easily show participants information about tournaments they are taking part in. By making tournaments easier to host, more people will want to host tournaments locally for fun, without relying on people who work for an international organization such as FIDE.


## Target Audience

The target audience for this application are various types of people who are familiar with chess: 
- People who are thinking of hosting a local chess tournament, but are intimidated by the effort it takes to host one.
- People who already have experience with hosting chess tournaments.
- People who like to play chess and are invited by a host to play in a local tournament.
- People who are chess enthusiasts and seek local tournaments.

The application in mind has features which are useful to all of these types of people in the target audience. You can host tournaments and view tournaments you’re playing, without getting intimidated by complicated features. You will also be able to use the features you need easily, without having to create an account if you aren’t a host.

# Competitive products 

My project:
- Something simple, yet useful
- Has a normal view, and an admin view (or organizer view or whatever)


## Swips

### Limitations

: limited participants and rounds on free version
	 
	New player information is not private. The website is too eager to link players together
	You cannot input game information (score, opponent, moves)
	You cannot edit pairings manually on the free version

### Good features
	Many pairing system types
•	 
	Score system flexibility
•	 
	Many tiebreak types
•	   
	You can upload pictures

##	Chessmanager

### Limitations

	Not as many options as swips for pairing system types and tiebreakers, etc
•	But it does have the double swiss pairing system
	Too many data fields are visible when inputting a player (although many fields are optional)
	It is hard to find the sharable tournament link
	You cannot see the dates and times for each round easily as a participant or viewer

### Good features
	Each round has a set time (schedule feature)
	It has chief arbiter contact information
	You can easily view both the manager page and the normal page. No need to log out.

## Coronate

### Limitations

	Not a lot of player fields and players cannot be pulled from a db
	You can’t share the tournament with others through a link (this is why accounts are necessary)

### Good features

	Many features you would normally have to pay for are free
	Editing pairings and switching colours is very easy

## SwissSys

### Limitations
	You can’t share results online. You can only print out the results
	You can only host tournaments with max 2 rounds on the free version

### Good features
	You have lots of control over players in the tournament
	You can get information about players by connecting with their database

## Tornelo

### Limitations
	More meant for online play
	Because there are many features, it is sometimes difficult to find the right ones

### Good features
	Lots of hosting options. You can make a tournament a part of a series, you can input your organization and many other things


Each of these competitors has their up and downsides. They are not exactly what I want. Therefore I will be making my own chess tournament service. It is also difficult to get the correct rating information. Not many players are in the FIDE database, and you can’t just edit player ratings as a host. I could just do something with estimated rating, or make a whole new rating system. I could maybe work with the chess.com API to get player information, but not every player is on that website


# User Stories


    - Describe your user stories (just as detailed as tick-documentation)

For this project I have thought of many possible useful features for this website. I have categorized the features based on the MoSCoW method, and have made proper user stories of all of the must-have features.

Later, during the development of the project, I realized that it was unrealistic for me to finish the must-have user stories. It was even difficult to finish the first user story, because of the increased complexity of the project and the technologies that are required for me to use. 

Normally, each user story should have acceptation criteria. Acceptation criteria are descriptions of specific actions that a user can do in an application, and they describe what should happen in the application in detail. Tests in applications are based on the acceptation criteria, because that ensures that all the user-actions are tested and prevents developers from wasting time on testing code that is not relevant for user stories. For more information about how I wrote tests for my acceptation criteria, go [here](Proof/../../Software%20Quality/Acceptation%20Criteria%20Tests.md).

It would be great to describe acceptation criteria for each written user story. However, since it was known to me that I wouldn't be able to finish many user stories, I have only written acceptation criteria for the first user story.

## Must have
- As a tournament host, I want to create tournaments on the site, so that the features related to tournaments can help me when organizing one.
- As a host, I want to add players to my tournament, so that I can include them when using tournament features.
- As a host, I want to be the only one who can access the page where my tournament information can be edited, so that no unexpected changes happen to the tournament information and to prevent cheating.
- As a tournament participant, I want to access the tournament page with a link, so I can easily see information about the tournament I’m participating in.
- As a new user, I want to create an account, so I have the ability to create tournaments on the site.
- As a host, I want a button where the site will generate new match-ups with players I have added in a tournament, so I don’t have to create the match-ups manually, can save time and can prevent human error.
- As a host, I want to input the score of a match, so that people will be informed about how matches went and to update the standings.
- As a host or participant, I want to see the current standings or results of a tournament, so I can be informed about how various players in the tournament have performed.
- As a host or participant, I want to see the results of previous matches and standings on previous rounds, so I can see how players in the tournament have progressed.

## Should have
- Different pairing systems
    - Swiss
    - Round Robin
- Round schedules
- More information about the matches (time for each person per game)
- Ability to edit scores
- Ability to create a series of tournaments and link a tournament to one

## Could have
- A tiebreak system
- More pairing systems
    - Double Swiss
    - Double Round Robin
    - Dubov
- More tiebreak systems
- Host contact information tab
- Ability to link player from different tournaments to an account
- Ability to view a player’s games from different tournaments
- Ability to input the moves from a game (and perhaps show them)
- Ability to change colors
- Ability to share a series of tournaments
- Ability to show all tournaments a person has hosted
- More player fields, such as:
    - Chess.com/lichess.com profile and rating
    - Club
    - Age
- Ability to store player information and choosing whether the info should be private or public.
    - If public is chosen, the information is stored in the public database and the player can be added to tournaments by other people.
    - If private is chosen, the player only exists within that one tournament. However, if an account comes and says that (s)he was that player, that private player can be linked to the account, and the private player will be deleted and merged with the public player information on the account

## Won’t have
- Max player amount
- Invite players with a link and invitation page
- Show chess tournament location on a map (hosting public chess tournaments)
- Notifications when a tournament is being held nearby
- Ability to generate a printable document with the current round standings and matches
- Ability to play the match itself online
- Entrance fee payments
- Ability to upload tournament photos to a tournament page
- Have arbiters in a tournament
- Rating system


# Architecture

- Describe your architecture. Why is everything so distributed? Why does potential match calculation happen in the frontend?

# Feedback

- Describe how the user service is not necessary due to Auth0 and how the round service was changed into the rank service. Why is the round service not needed, and why is the rank service needed?