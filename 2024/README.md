# Canvas 2024 Data files
## canvas-2024-fixed-sql.sql
There was an error with the fediverse-auth on the Canvas site where after a certain point new logins started being logged as all lower case which created duplicates of 59 users and were treated as separate users. I have merged all of the duplicate accounts and rebuilt the database. 

The SQL file has 4 tables:
* users (user_id, username, ranking, total_pixels_placed)
* colors (color_id, color_name, color_hex)
* pixels (log_id, user_id, x_cord, y_cord, color_id, time_placed, is_mod_action, is_top, time_deleted)
* top_cord (top_cord_id, user_id, x_cord, y_cord, count_placed)

The users table includes the rank and total pixels placed for each user. Deleted pixels are not counted. There are 13 users who deleted every pixel the placed. They are still ranked, but their total pixel count is 0.

The only data not included here is the pixel color counts for each user. You an find the pixel color counts for a user by selecting:

``SELECT color_name, count(color_name)
FROM public.pixels
JOIN users on users.user_id = pixels.user_id
JOIN colors on colors.color_id = pixels.color_id
WHERE username = <username> AND time_deleted IS NULL
GROUP BY color_name``

## users_2024.csv
This is the csv file used to serve the user data to Canvas Stats. The columns are username, ranking, total pixels placed, x coordinate of top coordinte, y coordinate of top coordinate, and the number of pixels placed on top coordinate.

## color_count_2024.csv
This is the csv file used to serve the color counts for each user to Canvas Stats. The columns are username, black, dark grey, deep grey, medium grey, white, beige, peach, brown, chocolate, rust, orange, yellow,pastel yellow, lime, green, dark green, forest, dark teal, light teal, aqua, azure, blue, navy, purple, mauve, magenta, pink, watermelon, red, rose, maroon, dark chocolate, dark purple

## pixels.csv
This is the csv file used to draw the images of user's pixels on the canvas. The columns are username, x coordinate, y coordinate, color hex