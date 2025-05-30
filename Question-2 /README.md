# Task - 2 
**1) Design ER-Diagram for Music Streaming Platform.** 
**2) Write query based on it.** 

## Music Streaming Plateform DB design
follwing queries are bassed on the database design of Music Streaming Plateform provided in the ER-Diagram (image).

### 1. Geting All Active Users with Valid Subscriptions

    WITH CTE as (SELECT user_id FROM User_Subscription us
    WHERE CURRENT_DATE BETWEEN us.start_date AND us.end_date
    GROUP BY us.user_id)
    
    SELECT user.user_id, user.name from CTE 
    JOIN User ON CTE.user_id = User.user_id

### 2. Listing Top 10 Most Played Track in jan

    SELECT lh.track_id, t.title, COUNT(*) AS play_count
    FROM Listening_History lh
    JOIN Track t ON lh.track_id = t.track_id
    GROUP BY lh.track_id
    ORDER BY play_count DESC
    LIMIT 10;


### 3. Geting Tracks in a Given Playlist

    SELECT t.track_id, t.title
    FROM Playlist p
    JOIN has h ON p.playlist_id = h.playlist_id
    JOIN Track t ON h.track_id = t.track_id
    WHERE p.playlist_id = 'YOUR_PLAYLIST_ID';

### 4. Get All Users Whose Subscription Will Expire in 10 Days

    SELECT user_id, end_date
    FROM User_Subscription
    WHERE end_date BETWEEN CURRENT_DATE AND CURRENT_DATE + INTERVAL '10' DAY;

### 5. Listing All Albums by a Specific Artist


    SELECT a.album_id, a.title
    FROM Album a
    JOIN Album_Artist aa ON a.album_id = aa.album_id
    WHERE aa.artist_id = 'YOUR_ARTIST_ID';

### 6. finding Top 5 Users by Listening Time

    SELECT lh.user_id, SUM(lh.play_duration) AS total_time
    FROM Listening_History lh
    GROUP BY lh.user_id
    ORDER BY total_time DESC
    LIMIT 5;

### 7. geting Most Popular Genre Based on Plays

    SELECT t.genre, COUNT(*) AS play_count
    FROM Listening_History lh
    JOIN Track t ON lh.track_id = t.track_id
    GROUP BY t.genre
    ORDER BY play_count DESC
    LIMIT 1;

### 8. inspecting Which Plans Have the Most Subscribers

    SELECT sp.name, COUNT(us.user_id) AS total_subscribers
    FROM Subscription_Plan sp
    JOIN User_Subscription us ON sp.sp_id = us.plan_id
    GROUP BY sp.name
    ORDER BY total_subscribers DESC;

### 9. Find All Tracks Released in the Last 30 Days

    SELECT track_id, title, release_date
    FROM Track
    WHERE release_date >= CURRENT_DATE - INTERVAL '30' DAY;

