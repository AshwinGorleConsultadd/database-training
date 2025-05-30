
## Question - 3 : MMORPG game.
question description is attatched into task3.pdf

## Step 1 : Setup
Defining table schema for account, account_item and item as per the description provided in pdf.

- **Creating *"accounts"* table**

        CREATE TABLE accounts (
            id INT PRIMARY KEY,
            username VARCHAR(255)
        );

- **Creating *"item_type"* table** (so that we can use it as ENUM)

        CREATE TYPE item_type AS ENUM ('sword', 'shield', 'armor');

- **Creating *"items"* table**

            CREATE TABLE items (
                id INT PRIMARY KEY,
                type item_type,
                name VARCHAR(255)
            );

- **Creating *"item_quality"* table** (so that we can use it as ENUM)

        qCREATE TYPE item_quality AS ENUM ('common', 'rare', 'epic');

- **Creating *"accounts_items "* table** (it shows many to many relation ship between item and  accounts and items table)

        CREATE TABLE accounts_items (
            account_id INT REFERENCES accounts(id),
            item_id INT REFERENCES items(id),
            quality item_quality
        );


## Step - 2 : Inserting data into tables
inserting data into all three tables as per the given question in pdf.

        -- Insert into accounts
        INSERT INTO accounts (id, username) VALUES
        (1, 'cmunns1'),
        (2, 'yworcs0');

        -- Insert into items
        INSERT INTO items (id, type, name) VALUES
        (1, 'sword', 'Sword of Solanaceae'),
        (2, 'shield', 'Shield of Rosaceae'),
        (3, 'shield', 'Shield of Fagaceae'),
        (5, 'shield', 'Shield of Lauraceae'),
        (6, 'sword', 'Sword of Loasaceae'),
        (7, 'armor', 'Armor of Myrtaceae'),
        (8, 'shield', 'Shield of Rosaceae'),
        (10, 'shield', 'Shield of Rosaceae');

        -- Insert into accounts_items
        INSERT INTO accounts_items (account_id, item_id, quality) VALUES
        (1, 10, 'epic'),
        (1, 2, 'rare'),
        (1, 2, 'rare'),
        (1, 7, 'rare'),
        (1, 1, 'common'),
        (1, 2, 'common'),
        (1, 3, 'common'),
        (1, 5, 'common'),
        (1, 8, 'common'),
        (2, 8, 'epic'),
        (2, 5, 'rare'),
        (2, 3, 'common'),
        (2, 6, 'common');

## Step-3: Final Answer Query

**Steps I Performed to compute result**


*Joined the tables*
- I joined accounts, items, and accounts_items to get all needed info like username, item type, quality, and item name in *one table for simplicity.*
Ranked item qualities
- I used RANK() to pick the best quality items for each user and type. "Epic" is best, then "rare", then "common", so I gave them numbers to sort properly.
Filtered top quality only
- After ranking, I kept only the items with the highest quality (rank = 1) for each user and type.
Grouped and combined item names
- I grouped the results and used STRING_AGG() to combine item names if there were multiple best items, and sorted them alphabetically.
Sorted final result as mentioned
- Finally I sorted everything by username and type like the task asked.

        WITH item_data AS (
            SELECT 
                a.username,
                i.type,
                ai.quality,
                i.name
            FROM accounts a
            JOIn accounts_items ai ON a.id = ai.account_id
            JOIN items i ON ai.item_id = i.id
        ),
        ranked_items AS (
            SELECT 
                username,
                type,
                quality,
                name,
                RANK() OVER (
                    PARTITION BY username, type 
                    ORDER BY 
                        CASE quality 
                            WHEN 'epic' THEN 3 
                            WHEN 'rare' THEN 2 
                            WHEN 'common' THEN 1 
                        END DESC
                ) AS quality_rank
            FROM item_data
        ),
        filtered_items AS (
            SELECT 
                username,
                type,
                quality AS advised_quality,
                name
            FROM ranked_items
            WHERE quality_rank = 1
        )
        SELECT 
            username,
            type,
            advised_quality,
            STRING_AGG(name, ', ' ORDER BY name) AS advised_name
        FROM filtered_items
        GROUP BY username, type, advised_quality
        ORDER BY username, type;
