# Leaderboard Application
> Technical Design Doc

## Summary
The aim of this document is to provide architecture design guidance on how to build the leaderboard web application. The goal is to be
able to provide a web application that display a comprehensive player ranking based on total number of eliminations across various game mode.
### Background
<!---
Provide a brief summary to set context for this document
--->
The Leaderboard web application is a web application for showcasing player rankings based on total number of eliminations across various game modes [solos, duos, trios, squads].
This web application will display real-time leaderboard data to users,ensuring that user can get their ranking compared to other users. This will enhance player
experience and boost their engagment with gamers community by sharing their achievements
### Problem statement
<!---
Provide a brief statement of the features of this solution and the primary challenges being addressed by the design
--->
The developed web application must be able to effectively display ranking bases on player eliminations across all the games played,handle easily real time leaderboard data updates
and provide and engaging user experience.
The primary challenges includes:
- Ensuring the UI is responsive and user-friendly
- Managing state and data consistency across different game mode and periods
- Providing a search feature that is efficient, fast, and accurate

## Keywords
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this specification are to be interpreted as described in [RFC2119](https://www.rfc-editor.org/rfc/rfc2119).
<!---
Additional keywords should be defined here.
--->

## Requirements
<!---
Brief list of enumerated requirements this solution must deliver
--->
### Functional requirements
<!---
Briefly list functional behaviors and attributes of this new system.
--->
1. The leaderboard web application should be able to display the following information containing following data:
    - Player name
    - Player rank 
    - Player eliminations 
    - Game mode 
    - Profile picture or avatar
2. The leaderboard web application MUST be able to filter the leaderboard data based on following game modes: solo, duos, trios, squads 
3. The leaderboard web application MUST support filtering data based on following periods:daily, weekly,all-time 
4. The leaderboard web application MUST be able to search for a specific player by name
5. The leaderboard web application SHOULD be able to display the top 10 players for each game mode per page by default
6. In case of no data available, the leaderboard web application MUST display a message indicating that no data is available
7. The leaderboard web application SHOULD update the leaderboard data in real-time without requiring the user to refresh the page
8. The application MUST be accessible and provide responsive design to support various device types
### Non-functional requirements
<!---
Briefly list other performance characteristics and requirements of the new system
--->
1. The leaderboard application MUST provide fast and responsive user experience by ensuring the following
2. The application SHOULD be scalable to handle a large number of concurrent users
3. The application MUST ensure secure communication and data handling, especially regarding user authentication by using Identity team OAuth2 compliant Authorization Server
4. The application MUST be able to handle periodic spikes up to 10x requests
5. The application SHOULD be maintainable and easy to extend with new features such as pagination, additional filters, and sorting options
## Out of Scope
<!---
Things that are not intended to be defined by this document.
--->
- Backend service such as REST API or GRAPHQL for data retrieval, processing and aggregating leaderboard data.
- Game logic or in-game features unrelated to the leaderboard data display.
- Authentication,Authorization and token generation services handled by identity team
- Data storage and management of leaderboard data
## Architecture/Design
<!---
Description of the architecture and diagrams. Feel free to add additional subheadings as needed, such as Alternatives
--->
### UI Design
<!---
Include any description or wireframe of the solution UI design.
--->
The UI design will follow the provided wireframe [Leaderboard](assets/Leaderboard.png) and will include the following components
- A search bar to search for a specific player by name
### Architecture design
<!---
Include any diagrams and discussion of solution architecture.
--->
### Sequence diagrams
<!---
Include any diagrams of flows through the solution such as decision trees or data flow.
--->
### Data models
<!---
Include any data modeling or schemas, including relationships between different data models
--->

## Implementation Details
<!---
Detailed description of how to achieve the design, additional diagrams, and analysis can go here. Feel free to add additional subheadings as needed, such as Dependencies and Risks.
--->
### Technology recommendations
<!---
List and explain any proposed technology choices such as languages, frameworks, database technologies, or cloud solutions. 
--->
### Dependencies
<!---
List any external dependencies of your solution (ie a service with authentication may have dependency on an identity provider)
--->
### Monitoring
<!---
Document any metrics or alerting cases to monitor the health of the application.  
--->
### Key metrics
<!---
Document key metrics to capture to evaluate user engagement and inform future product development.
--->

## Alternative Solutions
<!---
Document any other solutions considered, why they are not preferred, and whether certain conditions may warrant their reconsideration.
--->

## Open Questions
<!---
List any “known unknowns” that exist in the context of this proposed technical design.
--->
