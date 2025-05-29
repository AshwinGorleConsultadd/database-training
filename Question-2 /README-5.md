
## Music Streaming Plateform DB design
follwing queries are bassed on the database design provided in the ER-Diagram.

### 1. Get All Active Users with Valid Subscriptions

    SELECT u.user_id, u.name, us.plan_id, us.end_date
    FROM User u
    JOIN User_Subscription us ON u.user_id = us.user_id
    WHERE CURRENT_DATE BETWEEN us.start_date AND us.end_date;

### 2. List Top 10 Most Played Tracks

    SELECT lh.track_id, t.title, COUNT(*) AS play_count
    FROM Listening_History lh
    JOIN Track t ON lh.track_id = t.track_id
    GROUP BY lh.track_id, t.title
    ORDER BY play_count DESC
    LIMIT 10;

### 3. Find Tracks in a Given Playlist

    SELECT t.track_id, t.title
    FROM Playlist p
    JOIN has h ON p.playlist_id = h.playlist_id
    JOIN Track t ON h.track_id = t.track_id
    WHERE p.playlist_id = 'YOUR_PLAYLIST_ID';

### 4. Get All Users Whose Subscription Will Expire in 10 Days

    SELECT user_id, end_date
    FROM User_Subscription
    WHERE end_date BETWEEN CURRENT_DATE AND CURRENT_DATE + INTERVAL '10' DAY;

### 5. List All Albums by a Specific Artist

(Assumes you have or will add Album_Artist)

    SELECT a.album_id, a.title
    FROM Album a
    JOIN Album_Artist aa ON a.album_id = aa.album_id
    WHERE aa.artist_id = 'YOUR_ARTIST_ID';

### 6. Top 5 Users by Listening Time

    SELECT lh.user_id, SUM(lh.play_duration) AS total_time
    FROM Listening_History lh
    GROUP BY lh.user_id
    ORDER BY total_time DESC
    LIMIT 5;

### 7. Most Popular Genre Based on Plays

    SELECT t.genre, COUNT(*) AS play_count
    FROM Listening_History lh
    JOIN Track t ON lh.track_id = t.track_id
    GROUP BY t.genre
    ORDER BY play_count DESC
    LIMIT 1;

### 8. Which Plans Have the Most Subscribers

    SELECT sp.name, COUNT(us.user_id) AS total_subscribers
    FROM Subscription_Plan sp
    JOIN User_Subscription us ON sp.sp_id = us.plan_id
    GROUP BY sp.name
    ORDER BY total_subscribers DESC;

### 9. Find All Tracks Released in the Last 30 Days

    SELECT track_id, title, release_date
    FROM Track
    WHERE release_date >= CURRENT_DATE - INTERVAL '30' DAY;

### 10. List of Follow Relationships (Who Follows Whom)

    SELECT f.follow_id AS follower, u.name AS follower_name, f.user_id AS followed, u2.name AS followed_name, f.date
    FROM follow f
    JOIN User u ON f.follow_id = u.user_id
    JOIN User u2 ON f.user_id = u2.user_id;
