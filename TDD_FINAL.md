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
experience and boost their engagement with gamers community by sharing their achievements
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
The keywords "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this specification are to be interpreted as described in [RFC2119](https://www.rfc-editor.org/rfc/rfc2119).
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
- Pagination for displayed leaderboard data. This will only be provided as an optional feature in case the data to display may increase according to the requirements
## Architecture/Design
<!---
Description of the architecture and diagrams. Feel free to add additional subheadings as needed, such as Alternatives
--->
### UI Design
<!---
Include any description or wireframe of the solution UI design.
--->
### Initial wireframe
![image](assets/Leaderboard.png)
### Improved wireframe
![image](assets/Leaderboard-Imp.png)
### UI components breakdown
![image](assets/Components.png)
### Empty data component
![image](assets/EmptyData.png)

The UI design will follow the provided wireframe [Leaderboard](assets/Leaderboard.png) and components can be extracted from the provided wireframe like this from top to bottom:
- Main App Component which represent the whole application in the tree
- A header component that contains the application title and profile component
- A profile component that contains the player profile picture or avatar
- A SearchBox component to search for a specific player by name
- Mode filter component to filter the leaderboard data based on game mode
- Period filter component to filter the leaderboard data based on period
- A leaderboard component or datatable component that displays the leaderboard data
- A pagination component to navigate through the leaderboard data ( Optional)
- A component to display a message indicating that no data is available (Provide separate component for this)
- A page display component indicating the current page number and total number of pages (Optional)


### Architecture design
<!---
Include any diagrams and discussion of solution architecture.
--->
Here is a simple representation of the UI components tree:
```
├── main-app component
│   ├── header component
│   │   ├── title
│   │   └── profile component
│   ├── searchbox component
│   └── mode filter component
│   └── period filter component
│   └── leaderboard component
│   └── no data component
├── └── pagination component (Optional)
```

##### **Frontend (Web Application)**

  * A React.js application that interacts with backend services. 
  * Provides the UI for filtering and displaying leaderboard data. 
  * Uses WebSockets to handle real-time updates.

##### **Styling & UI component:**
* The app will be styled using tailwindcss and [shadcn](https://ui.shadcn.com) UI library to provide a consistent and responsive design across different devices. 

##### State Management 
* The components will be connected to a state management library such as Redux or React Context API to manage the application state and data flow.

##### **API Integration:** 
* Axios or Fetch API to communicate with the backend services to fetch leaderboard data

##### **React Time Update** 
For this type of architecture, we have two options to update the leaderboard data in real-time assuming that the server support socket event broadcasting
- Option **#1**
  - Client-Side Setup:
    - Install the Socket.IO client library in your React.js. 
    - Use the useEffect hook to establish a connection to the Socket.IO server upon component mount. 
    - Listen for socket events that broadcast leaderboard updates. 
    - Upon receiving updates, update your component's state and trigger a re-render to reflect the changes in the UI.
1. Option **#2**

### Sequence diagrams
<!---
Include any diagrams of flows through the solution such as decision trees or data flow.
--->
**General Flow**
1. User accesses the leaderboard webpage. 
2. Leaderboard web application perform authentication and authorization using the Identity team OAuth2 compliant Authorization Server to get JWT token L
3. Leaderboard web application fetches the leaderboard data from the Leaderboard Service
4. Leaderboard Service returns the data to the Leaderboard web application
5. Leaderboard web application displays the leaderboard data to the user
6. Leaderboard web application establishes a socket connection to the server to listen for leaderboard updates
7. Leaderboard Service broadcasts leaderboard updates to the connected clients
8. Leaderboard web application receives the update and updates the leaderboard data in real-time 
9. User selects filters (game mode, period, player). 
10. Web application requests filtered data from the Leaderboard Service 
11. Leaderboard Service fetches and returns filtered data. 
12. Web application displays filtered data.

Here is the sequence diagram that illustrates the flow of the leaderboard web application
![image](assets/SequenceDiagram.png)
### Data models
<!---
Include any data modeling or schemas, including relationships between different data models
--->
The frontend will handle data models corresponding to the API response provided in the API specification
From the given API specification, we can define the following initial data models that can be broken down into interfaces or types in the codebase

**Player data model**
```json
{
  "id": "string",
  "name": "string",
  "profilePicture": "string"
}
```
**Leaderboard data model**
```json
{
  "leaderboard": {
    "gameMode": "string",
    "period": "string",
    "start": "datetime",
    "end": "datetime",
    "entries": [
      {
        "player": "Player",
        "rank": "number",
        "eliminations": "number"
      }
    ]
  }
}
```

**PlayerLeaderBoard data model**
```json
{
  "player": "Player",
  "leaderboards": [
    {
      "leaderboard": "Leaderboard",
      "rank": "number",
      "eliminations": "number"
    }
  ]
}
```


If we consider that we will use Typescript the data models will be defined as interfaces
```typescript

type Period = 'DAILY' | 'WEEKLY' | 'ALL_TIME';

type GameMode = "SOLOS" | "DUOS" | "TRIOS" | "SQUADS"

interface Player {
    id: string;
    displayName: string;
    profilePicture?: string;
}

interface Entry {
    player: Player;
    rank: number;
    elims: number;
}

interface Leaderboard {
    gameMode: GameMode;
    period: Period;
    start: string;
    end: string;
}

interface PlayerLeaderBoard {
    player: Player;
    leaderboards: {
        leaderboard: Leaderboard;
        rank: number;
        elims: number;
    }[];
}
interface LeaderboardData {
    leaderboard: Leaderboard;
    entries: Entry[];
}
```
## Implementation Details
<!---
Detailed description of how to achieve the design, additional diagrams, and analysis can go here. Feel free to add additional subheadings as needed, such as Dependencies and Risks.
--->
### Technology recommendations
<!---
List and explain any proposed technology choices such as languages, frameworks, database technologies, or cloud solutions. 
--->
* **Frontend**: React.js is strong choice for building interactive and responsive user interface. 
* **Backend**: Node.js with Express for building scalable service that will offer different API to be consumed by the Fronted. 
* **Database**: PostgreSQL or MongoDB for high performance and scalability. 
* **Authentication**: OAuth2 with JWT for secure access. 
* **Real-time Updates**: WebSockets for real-time communication.
  There are some cloud service that can help to implement this feature easily like Firebase Realtime Database, Supabase, or Convex
    * Firebase Realtime Database: This is a NoSQL database from Google that is specifically designed for real-time applications. 
    It allows you to store and retrieve data with low latency, making it a good choice for applications that need to update data 
    frequently and see those changes reflected immediately by all users
    * Supabase: Supabase is an open-source alternative to Firebase that provides a suite of tools for building real-time applications.
      Supabase offers real-time capabilities through their Realtime server containers. You'll need to spin up and manage these containers alongside your main Supabase installation
    * Convex : Convex is a real-time database that allows you to build real-time applications without writing any backend code. 
      Convex provides a simple API that you can use to store and retrieve data in real-time, making it easy to build applications that update in real-time
### Dependencies
<!---
List any external dependencies of your solution (ie a service with authentication may have dependency on an identity provider)
--->
* OAuth2 compliant Authorization Server for authentication.
* Reliable and scalable database service.
* API Gateway for routing and security ( optional but may be recommended in future)
* WebSocket server for managing real-time connections.
### Monitoring
<!---
Document any metrics or alerting cases to monitor the health of the application.  
--->

### Key metrics
<!---
Document key metrics to capture to evaluate user engagement and inform future product development.
--->
* **Number of active users**: This metric will help us to know how may users are actively using our leaderboard services.
* **API response time**: This is a critical metric to capture since it directly impact the user experience.
* **User engagement metrics**: This includes the number of searches, filters, and interactions with the leaderboard data.
* **WebSocket connection metrics**: We would like to monitor the number of active connections, the number of messages sent and received, and the latency of the WebSocket connections.

## Alternative Solutions
<!---
Document any other solutions considered, why they are not preferred, and whether certain conditions may warrant their reconsideration.
--->
* **HTTP Polling**: This is a common approach to real-time updates where the client makes periodic requests to the server to check for updates.The reason it may not be
the preferred solution is that it is inefficient and resource intensive compared to WebSocket
* **Server Sent Event (SSE)**: This is a strong contender but has some disadvantages like it is unidirectional and does not support full-duplex communication like WebSocket

## Open Questions
<!---
List any “known unknowns” that exist in the context of this proposed technical design.
--->
