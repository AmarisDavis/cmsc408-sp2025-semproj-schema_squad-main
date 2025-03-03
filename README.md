# cmsc-vcu/cmsc408-sp2025-semproj-template

# Deliverable 5 

## Overview 

- This project involves designing and implementing a database for a social media application where users can review anime episodes. Users will be able to create an account, select a show and an episode, rate it, and write a review that can be viewed by others. The database is designed to store and manage user information, show details, episodes, ratings, and watchlists while ensuring security, efficiency, and scalability.

## Our Database Design 

-  Media/Show Reviewing application
- Social media application where we allow users to review anime episodes
- User’s create an account with an email, password, and username
- A page where users can select a show and an episode, give it a rating, and writing a review for the episode that is shared on a page where users can view other reviews of that episode
- Currently thinking of a Node.js backend
- Still coming to a decision on frontend
- Deciding on whether or not we will take an existing api for anime’s


## Our Diagram 

```{dot}
graph MediaReviewApplication {
    fontname="Helvetica,Arial,sans-serif"
    fontsize=8;  // Reduced font size for the entire graph
    node [fontname="Helvetica,Arial,sans-serif", fontsize=8, width=0.5, height=0.3, style=filled, fillcolor=white] // Default: smaller font size, reduced node size, shaded
    edge [fontname="Helvetica,Arial,sans-serif", fontsize=8] // Reduced font size for edges
    layout=neato
    nodesep=2.0;  // Increased separation between nodes on the same level
    ranksep=1.5;  // Increased separation between nodes on different levels
    size="6,6";   // Specify desired size in inches
    ratio=compress; // Allow Graphviz to compress the layout to fit the size
    dpi=60;  // Set DPI for higher resolution output
    center=false;
    
    //The Entities 
    node[shape = box; style = filled, color = black] 
    Users; Shows; Episodes; Ratings; Watchlist; 
    
    //The Attributes 
    node[shape= ellipse, style = filled, color = black]
    //for User 
    user_id; username; email; password; join_date;
    //for Shows 
    show_id; title; genre; release_year; total_seasons; average_rating;
    //for Episodes 
    episode_id; {node[label = "show_id"] ep_showID;} season_number; episode_number; {node[label = "title"] ep_title;} air_date;
    //for Ratings 
    rating_id; {node[label = "user_id"] rating_userID;} {node[label = "show_id"] rating_showID;} rating; review_text; date_rated; 
    //for Watchlist 
    watchlist_id; {node[label = "user_id"] watchlist_userID;} {node[label = "show_id"] watchlist_showID;} status; 
    
    
    //pairing the attributes  
    Users -- user_id;
    Users -- username;
    Users -- email;
    Users -- password;
    Users -- join_date;
    
    Shows -- show_id;
    Shows -- title;
    Shows -- genre;
    Shows -- release_year;
    Shows -- total_seasons;
    Shows -- average_rating;
    
    Episodes -- episode_id;
    Episodes -- ep_showID;
    Episodes -- season_number;
    Episodes -- episode_number;
    Episodes -- ep_title;
    Episodes -- air_date;
    
    Ratings -- rating_id;
    Ratings -- rating_userID;
    Ratings -- rating_showID; 
    Ratings -- rating;
    Ratings -- review_text;
    Ratings -- date_rated;
    
    Watchlist -- watchlist_id;
    Watchlist -- watchlist_userID;
    Watchlist -- watchlist_showID;
    Watchlist -- status; 
    
    
    //Relationships 
    node [shape=diamond, style=filled, color=black, fillcolor=white width=0.3, height=0.2, fontsize=6,] 
   {node [label = "has"] has;}  {node [label = "makes"] makes;}  {node [label = "contains"] contains1; contains2;} writes;
   
   Users -- writes;
   writes -- Ratings;
   Users -- makes;
   makes-- Watchlist;
   
   Shows -- contains1;
   contains1 -- Episodes;
   Shows -- has;
   has -- Ratings;
   
   Watchlist -- contains2;
   contains2 -- Shows;
 
}
```

## TimeLine 

The final project is due on April 29, and the development phases include database implementation, UI development, integration, testing, and documentation.

``` {mermaid}
gantt
    title Media Review Application - Project Schedule
    dateFormat  YYYY-MM-DD
    section Research & Planning
    Finalize ERD and relational schema        :done, 2024-03-02, 2024-03-05
    Define functional dependencies & normalization :done, 2024-03-03, 2024-03-08
    Review ethical considerations              :2024-03-05, 2024-03-10

    section Database Development
    Implement database schema                  :2024-03-10, 2024-03-20
    Set up authentication & access control     :2024-03-21, 2024-03-27
    Implement encryption & security features   :2024-03-28, 2024-04-05

    section Application Development
    Develop user interface                     :2024-03-15, 2024-04-10
    Integrate database with front-end          :2024-04-01, 2024-04-15
    Implement review submission & display      :2024-04-05, 2024-04-18
    Testing & debugging                        :2024-04-10, 2024-04-22

    section Documentation & Submission
    Write final project report                 :2024-04-15, 2024-04-25
    Review & refine project                    :2024-04-20, 2024-04-27
    Submit final project                       :milestone, 2024-04-29
``
