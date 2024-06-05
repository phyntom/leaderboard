# Context

You are a member of a customer-facing Leaderboard team. Your team has designed a Leaderboard service
that has been used to render in-game Leaderboards for a multiplayer online game for quite a while. 
The team is now looking for your expertise in architecting the Leaderboard application for the web.

Leaderboards are based on the total number of eliminations across all games played by a player. For
example, if a player has 10 eliminations across 10 games they will be ranked lower than a player
that has 11 eliminations across any number of games.

Leaderboards are aggregated by each of the following:
1. Game Mode - solos, duos, trios, squads
2. Period - daily, weekly, and all-time

Additionally, the Identity team provides an OAuth2 compliant Authorization Server that provides 
access tokens in JWT format for both clients (for service-to-service requests) and users 
(for client-to-server requests).

Your task is to use the provided [API specification](api/openapi.yaml) and document how you would architect
the application using the included [Technical Design Document Template](TDD_TEMPLATE.md). 

A [wireframe](assets/Leaderboard.png) of the new user interface is provided. 

The story might be written as follows:

---

## Story

### User Stories
As a player, I would like to be able to view leaderboards on the web, so I can share my placement
with people outside the game.

As a player, I would like to be able to view the top 10 players for each game mode.

### Acceptance Criteria

* Must allow filtering by:
  - player
  - game mode (solos, duos, trios, squads)
  - period (daily, weekly, all-time)
* Must be able to handle up to 10 million concurrent players and an average of 10,000 game matches ending every minute.
* Must be able to handle periodic spikes up to 10x requests.
* Must assume the leaderboard is viewed after every match.
* If necessary, must make change recommendations to the Leaderboard service API to support the proposed design.

---

## What We Provide
* [Technical Design Document template](TDD_TEMPLATE.md) to be copied and completed in response to the Story above.
* [API Specification](api/openapi.yaml) for the Leaderboard service that provides data to populate the new frontend application.
* [Wireframe](assets/Leaderboard.png) of the new Leaderboard application for reference.

## Expectations
* Please copy the [Technical Design Document template](TDD_TEMPLATE.md) to a new file and fill in the relevant information. Note that the template contains helpful comments under each heading. 
* Please link any existing or new assets that should be referred to when reading your Technical Design Document into the main body of the document.
* You may add or remove headings if necessary.
* You may refer to, include, or cite any of the assets provided. 
